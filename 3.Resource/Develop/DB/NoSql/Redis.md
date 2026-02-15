
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


자료구조 : String,  Hash, List, Set, Sorted Set, TTL


3.실시간 분석 및 계산 (Real-time Processing) : 즉시성
- **사례:** 실시간 인기 검색어, 게임 랭킹 보드(Leaderboard), 오늘 방문자 수 카운팅.

4.메시지 브로커 (Messaging) : 통신
- **사례:** 실시간 채팅방, 푸시 알림 서비스, 작업 큐(Task Queue).

5.분산 제어 (Distributed Coordination) : 데이터 정합성
- **사례:** **분산 락(Distributed Lock)**을 이용한 중복 결제 방지, 선착순 100명 이벤트 관리.
- 로드 밸런서가 이 서버 저서버로 DB에 접근할텐데 그때의 데이터를 한곳에서 관리하니까 ? 이건 잘 모르겠음.

목적 : 빠른 속도(In-memory)를 유지하면서, 여러 서버가 공유해야 하는 핵심 데이터를 안전하고 정확하게 처리하는 것


@ConditionalOnProperty : 설정값에 따라 이 클래스를 빈(Bean)으로 등록할 지 말지를 결정한다.
 
```java
@ConditionalOnProperty(
    name = "cache.store",  // application.properties에서 key가 cache.store로 설정된 것을 찾는다.
    havingValue = "local", // 그 값이 local 인지 확인한다.
    matchIfMissing = true // cache.store 자체의 설정이 없더라도 기본적으로 이 클래스를 사용한다.
)
```

사용이유 : 
- Scale out 시의 데이터 정합성, 멤버 클래스의 HashMap을 사용한다면 한 쪽 서버에는 데이터가 없을 수 있다. -> 어떤 서버에서 접근하든지 데이터가 있도록 설정하는 것이 레디스의 장점이다.


그렇다면 이것은 안티패턴일까 ? 아니다. 전략 패턴으로 스케일 아웃 상황에서는 신경쓰지 않아도된다.
스케일 아웃 상황에서 redis를 사용할때 HashMap 으로 관리중이던.

@PostConstruct로 처리되는 HashMap의 경우에는 신경쓰지 않아도 되지만,
그 값이 운영 상황에서 변할 수 있다면 전략 패턴을 적용해서 Redis로 보내면 된다.
전략 패턴을 사용하면 동적으로 데이터를 처리할 수 있기 때문에 전략 패턴을 이용하면 확장성까지 가질수있다. (Redis가 아닌 `Hazelcast`, `Memcached`의 사용도 가능하다.)

**핵심 포인트**: 두 대 이상의 WAS가 동일한 캐시를 바라보기 위해 Redis를 사용한다.  
- `cache.store=local` → Caffeine (JVM 내부 캐시, 단일 인스턴스용)  
- `cache.store=redis` → Redis (외부 캐시, 다중 인스턴스 공유)
- `cache.ttl.default.minutes=10`

이 패턴 덕분에 **코드 변경 없이 프로퍼티만 바꾸면** 로컬 개발(Caffeine) ↔ 운영 이중화(Redis)를 전환할 수 있다.


### 2.캐싱 설정

`@EnableCaching`은 **"스프링아, 이제부터 내 코드에 캐시 관련 어노테이션(`@Cacheable` 등)이 보이면 캐시 기능을 작동시켜줘"**라고 명령하는 스위치입니다.

`RedisConfig`  를 설정한다.


Lettuce: 레디스 엔진
redisConnectionFactory : 레디스 연결 통로
redisTemplate : redis에 명령어를 날릴 때 사용한다.
RedisStandaloneConfiguration : redis가 한대
clientBuilder.useSsl() : ssl 암호화 설정

redisConnectionFactory : password, ssl, connection timeout setting 
redisTemplate:  어떤 포맷으로 레디스에 저장할지, 직렬화 설정 (기본적으로 byte라서 해줘야한다.)
cacheManager : ttl, 


`@EnableCaching` 기억하시나요? 이 어노테이션이 붙는 순간, 스프링은 전체 프로젝트의 모든 클래스를 훑기 시작합니다.

- **레이더 가동:** "자, 지금부터 `@Cacheable`이나 `@CacheEvict`가 붙은 메서드가 있는지 다 찾아봐!"
- 프록시 객체가 호출을 가로채서 이를 확보한다.
`roleService.getRoleById(1L)`를 호출했을 때의 시나리오입니다.

1. **레디스 먼저 확인:** 스프링이 레디스에 `role:byId::1`이라는 키가 있는지 먼저 봅니다.
2. **데이터 없음 (Cache Miss):** 레디스에 데이터가 없다면, 진짜 메서드(`roleRepository.findById`)를 실행해 DB에서 데이터를 가져옵니다 . - rdbms에서 가져온다.
3. **레디스에 저장:** **이때가 포인트입니다!** 메서드가 리턴한 `Role` 객체를 아까 설정한 `valueSerializer`(JSON)를 이용해 레디스에 **착!** 저장합니다.
4. **다음 호출:** 이제 다시 똑같은 ID로 호출하면 DB에 가지 않고 레디스에서 바로 꺼내옵니다.

---
### Redis 자료구조 

자료구조 :  Value, Hash, List, Set, ZSet

Value  :    Key -> Value 
Hash  :    Key : { Field1: Value, Field2: Value ... }, 객체의 특정 필드만 수정하거나 가져올 때 효과적
List     :    Key : [ Value1, Value2, Value3 ], 데이터 순서보장
Set     :    Key : { Value1, Value2 ... }, 중복 허용, 순서 보장 X
ZSet  :    Key :  {"user:A": 10.5, "user:B": 50.2, "user:C": 30.0}, 실시간 자동 정렬

---
## Redis 도입 및 시스템 고도화 분석 보고서

### 1. 문제 상황 (Problem) : "성장의 병목, 로컬 캐시의 한계"

- **인프라 변화:** 서비스 규모 확대로 인한 서버 **Scale-out**(다중화) 진행. 
	- CAP 원칙을 위배한 데이터의 조회가 이루어졌다. 
- **데이터 불일치:** 기존 CMP 솔루션이 `Local Cache`(멤버 변수)를 사용하여 세션, 토큰, 권한 정보를 관리함에 따라 서버 간 데이터 정합성이 깨지는 문제 발생.
- **가용성 저하:** 특정 서버에서 업데이트된 권한이나 세션이 다른 서버에는 반영되지 않아 사용자 경험에 치명적인 오류 유발

### CAP 이론  
분산 시스템에서 세 가지를 동시에 만족할 수 없다:  
- **C (Consistency)**: 모든 노드가 동일한 데이터를 봄  
- **A (Availability)**: 모든 요청에 응답  
- **P (Partition Tolerance)**: 네트워크 분리에도 동작

---
### 2. 구현 및 해결 방안 (Solution) : "전략적 캐싱 아키텍처 설계"

단순히 레디스를 붙이는 것에 그치지 않고, **데이터의 특성에 따라 접근 방식을 이원화**하여 효율성을 극대화했습니다.

#### **A. 디자인 패턴을 활용한 구조화**

- **전략 패턴 (Strategy):** 설정(`application.yml`)에 따라 `Local`과 `Redis` 구현체를 선택적으로 주입할 수 있도록 설계하여 환경 유연성 확보.
- **템플릿 메서드 패턴 (Template Method):** `RedisBaseRepository` 추상 클래스를 도입. 중복되는 Redis 연결 및 키 생성 로직을 부모가 관리하고, 자식은 `getBaseKey()` 등 식별 정보만 구현하여 생산성 향상.

#### **B. 데이터 특성별 기술 선택**

|**구분**|**적용 기술**|**선정 이유**|
|---|---|---|
|**단순 조회성** (메뉴 등)|**Spring Cache**|`@Cacheable` 어노테이션으로 비즈니스 로직과 캐시 로직을 분리(AOP), 개발 생산성 중점.|
|**가공/수정 빈번** (세션, 권한)|**RedisTemplate**|세밀한 자료구조(Hash, Set 등) 제어가 필요하며, 복잡한 비즈니스 로직과의 결합을 위해 프로그래밍 방식 선택.|

---
### 3. 최적화 및 리팩토링 (Optimization) : "운영 안정성 확보"

구현 이후, Redis의 내부 동작 원리(Single Thread)와 장애 상황을 고려한 **엔지니어링적 개선**을 진행했습니다.

- **성능 최적화 (`KEYS` → `SCAN`):** * Redis는 **Single Thread**로 동작하므로 `KEYS *` 실행 시 전체 서비스가 Blocking(멈춤)될 위험이 있음.
    - 이를 커서 기반의 `SCAN` 방식으로 리팩토링하여 대용량 트래픽 상황에서도 서비스 가용성을 보장함.
- **장애 극복 전략 (Failover):** * 단일 Redis 컨테이너 장애 시 서비스 전체가 마비되는 **SPOF(Single Point of Failure)** 방지.
    - `try-catch` 및 예외 처리를 통해 Redis 연결 실패 시 **Database로 직접 조회(Fallback)**하도록 설계하여 **Graceful Degradation**(우아한 성능 저하) 구현.

---
### 이력서

> **"분산 환경 내 데이터 정합성 해결을 위해 Redis 기반 글로벌 캐시 아키텍처를 설계했습니다. 디자인 패턴(Strategy, Template Method)을 적용해 코드 중복을 80% 이상 제거했으며, Redis의 싱글 스레드 특성을 고려하여 `SCAN` 기반 최적화 및 DB Fallback 로직을 구현함으로써 시스템의 안정성과 고가용성을 동시에 확보했습니다."**

### 추가 정보

전략 패턴 : 인터페이스를 구현하고 실행할 때 실제 구현체를 주입받아 사용합니다.
- 동적으로 구현체를 할당받는다.

템플릿 메서드 패턴 : 부모(추상 클래스)가 실행 순서나 공통 로직을 다 짜놓고, 자식은 구현체만 
- 부모에서 대부분을 정해둔다.


기본적으로 DB에 저장하고, Redis를 이용하여 캐시를  