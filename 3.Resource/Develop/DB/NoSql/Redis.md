
Full Name : Re(Remote) Di(Directory) S(Server)
사용 목적 : 캐싱, 세션 관리, 실시간 분석, 메시지 브로커, 분산 제어

---

캐싱 (Caching) : 성능 최적화

- **사례:** 자주 조회하는 상품 상세 정보, 공지사항 등.
- 조회를 첫 번째 부터 빠르게 할 건지 재조회부터 빠르게 할 건지에 대한 논의는 필요하다.
- 첫 번째 조회부터 빠르게 하려면 Write-through / Warming up 방식을 사용한다.
	- Write-through : 쓰기작업과 동시에 Redis 에도 데이터를 삽입한다
	- Warming Up : 서버가 뜰 때 레디스에 데이터를 넣어둔다.

세션 및 상태 관리 (Session Management) : 사용자 유지
- **사례:** 로그인했는데 새로고침하니 로그아웃됐어요 같은 상황 방지.
- Active-Standby 라면 문제가 되지않지만, 현대의 대부분은 Active-Active로 설정되어있다.
- 한 서버가 죽었을떄 몇 만명의 데이터를 서버에서 저장한다면 문제가 발생한다.

1.백엔드 서버에서 관리할때랑, Redis에서 관리할 때랑 코드의 규약이 어떻게 달라질까 ?


| 유형 | 대표 DB | 데이터 모델 | 적합한 케이스 |  
|------|---------|------------|-------------|  
| **Key-Value** | Redis, Memcached | `key → value` | 캐싱, 세션, 실시간 카운터 |  
| **Document** | MongoDB, CouchDB | `key → JSON/BSON 문서` | 유연한 스키마, CMS, 카탈로그 |  
| **Column-Family** | Cassandra, HBase | `row → column family` | 시계열 데이터, 대량 쓰기 |  
| **Graph** | Neo4j, Amazon Neptune | `노드-엣지 관계` | 소셜 네트워크, 추천 시스템 |


3.실시간 분석 및 계산 (Real-time Processing) : 즉시성
- **사례:** 실시간 인기 검색어, 게임 랭킹 보드(Leaderboard), 오늘 방문자 수 카운팅.

4.메시지 브로커 (Messaging) : 통신
- **사례:** 실시간 채팅방, 푸시 알림 서비스, 작업 큐(Task Queue).

5.분산 제어 (Distributed Coordination) : 데이터 정합성
- **사례:** **분산 락(Distributed Lock)**을 이용한 중복 결제 방지, 선착순 100명 이벤트 관리.
- 로드 밸런서가 이 서버 저서버로 DB에 접근할텐데 그때의 데이터를 한곳에서 관리하니까 ? 이건 잘 모르겠음.

목적 : 빠른 속도(In-memory)를 유지하면서, 여러 서버가 공유해야 하는 핵심 데이터를 안전하고 정확하게 처리하는 것

---
### Spring - Redis 사용법

 @Cacheable vs RedisTemplate 



Redis 사용목적 

  1. 현재 프로젝트의 Redis 사용 목적은 "캐시 공유"                                                                                                                                                            
  - cache.store=redis|local 프로퍼티 하나로 Caffeine(로컬) ↔ Redis(공유) 전환                                                                                                                               
  - WAS 2대가 같은 Redis를 바라보므로, 한쪽에서 캐시를 갱신하면 다른 쪽도 즉시 반영됨
  - 현재는 RedisStandaloneConfiguration (단일 노드) — 가장 단순한 형태

  2. 대용량 트래픽 시 달라지는 점
  - 토폴로지: Standalone → Sentinel(자동 장애복구) 또는 Cluster(샤딩/수평확장)
  - 활용 범위: 단순 캐시를 넘어서 세션 스토어, 분산 락, Rate Limiting, Pub/Sub, 이벤트 큐로 확장
  - 코드 변경: ConnectionFactory 설정만 교체하면 기존 RedisTemplate 기반 코드는 그대로 동작

  3. 프로젝트 설계의 좋은 점
  - 5가지 Redis 자료구조별 RedisBase*Repository 추상화 → 비즈니스 코드와 Redis 명령이 분리됨
  - @ConditionalOnProperty로 캐시 전략을 완전히 격리 → 로컬 개발은 Caffeine, 운영은 Redis
  ───────────────────────────────────────

  문서에는 NoSQL 기본 개념부터 프로젝트의 실제 코드 분석, 그리고 대용량 트래픽 시나리오별 Redis 활용법(세션, 분산 락, Rate Limiting, Pub/Sub 등)까지 포함했습니다.


---

### 분산시스템으로 변경할 때 만족할 수 없는 CAP 이론을 충족하기 위해 Redis 사용을 결심하였다.

### CAP 이론  
분산 시스템에서 세 가지를 동시에 만족할 수 없다:  
- **C (Consistency)**: 모든 노드가 동일한 데이터를 봄  
- **A (Availability)**: 모든 요청에 응답  
- **P (Partition Tolerance)**: 네트워크 분리에도 동작