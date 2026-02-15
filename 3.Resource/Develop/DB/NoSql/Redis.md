
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


redisConfig 

redisConnectionFactory : password, ssl, connection timeout setting 
redisTemplate:  어떤 포맷으로 레디스에 저장할지, 직렬화 설정 (기본적으로 byte라서 해줘야한다.)
cacheManager : ttl, 


@Cacheable, @Caching 

**`@EnableCaching`** 기억하시나요? 이 어노테이션이 붙는 순간, 스프링은 전체 프로젝트의 모든 클래스를 훑기 시작합니다.

- **레이더 가동:** "자, 지금부터 `@Cacheable`이나 `@CacheEvict`가 붙은 메서드가 있는지 다 찾아봐!"
- 프록시 객체가 호출을 가로채서 이를 확보한다.
`roleService.getRoleById(1L)`를 호출했을 때의 시나리오입니다.

1. **레디스 먼저 확인:** 스프링이 레디스에 `role:byId::1`이라는 키가 있는지 먼저 봅니다.
2. **데이터 없음 (Cache Miss):** 레디스에 데이터가 없다면, 진짜 메서드(`roleRepository.findById`)를 실행해 DB에서 데이터를 가져옵니다 . - rdbms에서 가져온다.
3. **레디스에 저장:** **이때가 포인트입니다!** 메서드가 리턴한 `Role` 객체를 아까 설정한 `valueSerializer`(JSON)를 이용해 레디스에 **착!** 저장합니다.
4. **다음 호출:** 이제 다시 똑같은 ID로 호출하면 DB에 가지 않고 레디스에서 바로 꺼내옵니다.

### 4. 그럼에도 불구하고 Redis를 DB로 쓰는 경우 (예외)

물론 Redis를 캐시가 아닌 **주 저장소(DB)**로 쓰는 경우도 있습니다. 다만 조건이 있습니다. **"좀 날아가도 괜찮거나, 아주 단순하고 빠른 처리가 생명인 데이터"**일 때입니다.

- **실시간 채팅 메시지:** 아주 빠른 전달이 중요할 때.
- **게임 서버의 실시간 랭킹:** 순위가 잠시 날아가도 다시 계산하면 될 때.
- **오늘 하루 방문자 수:** 통계 데이터.

### 결론: 왜 우리 프로젝트는 Caching으로 쓸까?

지금 보시는 `Role` 데이터(권한, 역할)는 **절대로 사라지면 안 되는 매우 중요한 정보**입니다.

1. 그래서 **원본은 안전한 RDBMS(MySQL 등)**에 영구 보관합니다.
2. 하지만 권한 체크는 사용자가 페이지를 이동할 때마다 수만 번씩 일어나죠.
3. 이때마다 느린 RDBMS를 부르면 서버가 힘들어하니, **Redis라는 초고속 메모리에 "복사본"**을 올려두고 캐싱 방식으로 쓰는 것입니다.

원본은 대부분 RDBMS에 저장하고 캐싱의 목적으로 NoSQL(Redis)를 사용한다.

---


캐싱을 구현하는 방식을 두 가지로 구분한다.


1. **Spring Cache 기반 선언적 캐싱(Annotation-based Caching)**
	- 비즈니스 로직에 집중할 수 있다.
	- 세밀한 조절이 어렵다.
	- 사용법 : 일반적인 조회 메서드 (대부분이 읽기 작업인 경우)

2.  **캐싱 데이터 처리 로직을 직접 구현(캐시 레포지토리 패턴)**
	- 매우 세밀한 조절이 가능하다.
	- 사용법 : 실시간 랭킹 (쓰기, 수정작업이 동반된 경우)

방금 보신 `RoleService`는 **선언적 캐싱**을 썼습니다. 왜냐하면 `Role` 데이터를 가져오는 로직은 "ID로 찾아서 있으면 주고 없으면 DB 간다"는 **정형화된 패턴**이기 때문입니다. 이런 단순 조회는 어노테이션이 훨씬 효율적이죠.

반면, 만약 프로젝트에 **"실시간 접속자 랭킹"**이나 **"5분간 유효한 1회용 인증번호"** 같은 기능이 있다면, 그건 어노테이션보다 **직접 구현 방식**이 훨씬 유리합니다.


- `@Cacheable`
    - 캐시에 값이 있으면 캐시 값을 반환하고, 없으면 메서드를 실행한 뒤 결과를 캐시에 저장한다.
- `@CachePut`
    - 메서드를 항상 실행하고, 반환 결과를 캐시에 저장(갱신)한다. - 성능 안 좋아서 자주 사용 안 할듯
    - 첫 번째 조회조차 무조건 빨라야 할 때
    - @CahcePut등으로 수정작업이 일어나고 해당 데이터를 조회할때는 @Cacheable을 사용하면 데이터 조회속도가 엄청빠르다.
- `@CacheEvict`
    - 캐시를 삭제(무효화)한다.


**로컬 캐시 (기본):** 별도의 설정이 없으면 스프링은 서버 내부의 메모리(`ConcurrentHashMap`)를 캐시 저장소로 씁니다. (이걸 `Caffeine`이나 `Ehcache`라고 부릅니다.)
**언제 Redis를 쓰나? (분산 캐시):** 서버가 1대일 때는 로컬 캐시로 충분합니다. 하지만 서버가 2대 이상일 때, 1번 서버에서 캐시한 데이터를 2번 서버도 알아야 한다면? 이때는 공용 냉장고인 **Redis**가 필수가 됩니다.

---

## 4. 선택 가이드 (언제 1번을 쓰고, 언제 2번을 쓰는지)

입력 내용 기준으로 판단 가능한 범위에서 정리하면 다음과 같다.

- **Spring Cache 기반 선언적 캐싱(방식 1)**
    
    - 메서드 단위로 캐싱 적용이 가능한 경우
    - `@Cacheable/@CacheEvict/@CachePut` 만으로 요구사항을 충족할 수 있는 경우
        
- **캐시 레포지토리 패턴(방식 2)**
    
    - 캐싱 데이터를 “저장/조회/갱신” 단위로 명시적으로 제어해야 하는 경우
    - 캐싱 데이터 구조 자체를 서비스 로직에서 직접 다뤄야 하는 경우
    - 통째로 저장하는게 아닌 자료구조를 활용하여 효율적인 구현이 필요한 경우




### Spring - Redis 사용법

 @Cacheable vs RedisTemplate 



Redis 사용목적 

  2. 대용량 트래픽 시 달라지는 점
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


---
### Redis 자료구조 


자료구조 : 
- Value, Hash, List, Set, ZSet

Value  ->  Key -> Value 
- 가장 기본적
Hash  ->  Key : { Field1: Value, Field2: Value ... }
- 객체의 특정 필드만 수정하거나 가져올 때 효과적

List     -> Key : [ Value1, Value2, Value3 ]
- 데이터 순서보장
Set     -> Key : { Value1, Value2 ... }
- 중복 허용, 순서 보장 X

ZSet
- Key : { Value1(Score: 10), Value2(Score: 20) ... }
- Set 처럼 중독은 안되지만, 자동 정렬, 실시간 랭킹 시스템 

base_key:rawKey 형식으로 key를 저장하는게 국룰이다.
그럼 내가 Redis를 하면서 겪은 것은
  

서버가 scale out에서 다중으로 늘어나면서 세션, 토큰, Role 등의 관리가 필요해졌고
그를 redis로 도입해서 해결하는데
해줘야하는건

1.redisConfig - redis기본설정
2.redis 자료구조 정의
3.spring cache vs redisTemplate를 이용하여 구현할지 설정하고 적용만해주면되는거였네.

이걸 이력서에 쓰면 이점이 되려나 ? 분석해주고 이 외에도 내가 레디스에서 알아야할 정보가 있나 알아봐줘

- **분산 환경에 대한 이해 증명:** "서버가 Scale-out 되는 환경에서 데이터 정합성 문제를 해결하기 위해 Redis를 분산 캐시/세션 저장소로 도입했다"는 문장은 당신이 **확장 가능한 아키텍처**를 고민하는 개발자임을 보여줍니다.
    
- **전략적 선택 능력:** "데이터의 특성(단순 조회 vs 복잡한 가공)에 따라 **Spring Cache**와 **RedisTemplate**을 적절히 혼용하여 생산성과 제어권을 동시에 잡았다"는 표현은 매우 전문적으로 들립니다.
    
- **자료구조 최적화:** "단순 String 저장이 아닌, 목적에 맞는 자료구조(Hash, ZSet 등)를 선택하여 **메모리 효율과 성능**을 개선했다"는 내용은 실무 역량을 입증하는 킬링 포인트입니다.


---
### 추가적인 정보

1.Redis Single Thread  : 레디스는 한 번에 하나의 명령만 수행한다.
2.캐시 쇄도(Cache Stampede)와 유효기간(TTL)
3.영속성 옵션 (RDB vs AOF)
- **RDB:** 특정 시점의 스냅샷을 찍어 파일로 저장 (백업용).
- **AOF:** 모든 쓰기 명령을 기록해두었다가 다시 실행 (복구용).
4.메모리 한계와 퇴거 정책 (Maxmemory Policy)

Redis가 죽었을 때의 대응법을 고민해봐야할듯..
로컬 캐시와 레디스를 같이 쓰는경우까지 고려해보면될듯


`KEYS *`가

- 이 점원은 엄청나게 발이 빨라서, 간단한 주문(GET, SET)은 1초에 수십만 개도 처리합니다.
- 그런데 만약 한 손님이 **"가게 안에 있는 모든 메뉴판 다 가져와서 읽어줘!(KEYS *)"**라는 복잡한 주문을 하면 어떻게 될까요?
- 점원은 그 일을 끝낼 때까지 **다음 손님의 주문을 아예 받지 못하고 멈춰 서게 됩니다.**