사용 목적 : 대규모 캐싱, 실시간 처리, 비정형 데이터 등

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