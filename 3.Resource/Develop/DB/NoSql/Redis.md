
Full Name : Re(Remote) Di(Directory) S(Server)
사용 목적 : 캐싱, 세션 관리, 실시간 분석, 메시지 브로커, 분산 제어
- 캐싱 (Caching) : 성능 최적화
- 세션 및 상태 관리 (Session Management) : 사용자 유지
	- 현대의 대부분은 Active-Active로 설정되어있다.
- 실시간 분석 및 계산 (Real-time Processing) : 즉시성
	- 실시간 인기 검색어, 게임 랭킹 보드(Leaderboard), 오늘 방문자 수 카운팅.
- 메시지 브로커 (Messaging) : 통신
	- 시간 채팅방, 푸시 알림 서비스, 작업 큐(Task Queue).
- 분산 제어 (Distributed Coordination) : 데이터 정합성
	- **분산 락(Distributed Lock)**을 이용한 중복 결제 방지, 선착순 100명 이벤트 관리.
	- 분산 락 - 모든 서버에서 Redis 데이터를 본다.

---
### Redis 자료구조 

자료구조 :  Value, Hash, List, Set, ZSet

Value  :    Key -> Value 
Hash  :    Key : { Field1: Value, Field2: Value ... }, 객체의 특정 필드만 수정하거나 가져올 때 효과적
List     :    Key : [ Value1, Value2, Value3 ], 데이터 순서보장
Set     :    Key : { Value1, Value2 ... }, 중복 허용, 순서 보장 X
ZSet  :    Key :  {"user:A": 10.5, "user:B": 50.2, "user:C": 30.0}, 실시간 자동 정렬

---
## Redis 도입 및 시스템 고도화 분석 보고서 (캐싱, 세션,  분산 제어)

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

기본적으로 DB에 저장하고, Redis를 이용하여 캐싱을 처리한다.
PostConstruct로 설정된 HashMap중 데이터의 변화가 일어난다면 Redis로 관리한다.
(각 서버마다 다른 정보를 보여주면 안 되기 때문이다.)

---
### 근거:

1. @EnableRedisHttpSession 미사용 — Spring Session Redis를 활성화하는 어노테이션이 프로젝트 어디에도 없음                                                                                             
2. spring-session-data-redis 의존성 미확인 — Redis 세션 라이브러리가 포함되어 있지 않음
3. request.getSession() 사용 — SessionHandlingInterceptor에서 서블릿 표준 HttpSession에 직접 setAttribute/getAttribute 호출
4. 세션 타임아웃도 서블릿 방식 — request.getSession().setMaxInactiveInterval(sessionTimeoutSec) 로 Tomcat 세션 타임아웃을 직접 설정 (프로퍼티: session.timeout=86400, 24시간)

  현재 세션 흐름:
  로그인 → SessionHandlingInterceptor에서 HttpSession에 User/Role 저장
         → Tomcat JVM 메모리에 세션 보관
         → 24시간 후 자동 만료

  이중화 시 주의할 점:
  - 현재 Redis는 캐시 데이터만 공유하고, 세션은 각 WAS의 Tomcat 메모리에 독립 저장됨
  - WAS 이중화 상태에서 L4/L7 로드밸런서가 Sticky Session(세션 어피니티)을 설정하지 않으면, 사용자가 다른 WAS로 라우팅될 때 로그인이 풀리는 문제가 발생할 수 있음
  - 이를 해결하려면 @EnableRedisHttpSession으로 세션도 Redis에 저장하거나, 로드밸런서에서 Sticky Session을 보장해야 함

로드 밸런서가 고정되어있다면 사용할 필요가없다.

---

2.동일 사용자'가 아닌 '공유 자원'의 문제입니다
- 분산락이 필요한 이유는 **"한 사용자가 보내는 요청"** 때문만이 아니라, **"여러 사용자가 동시에 건드리는 데이터"** 때문입니다.

---
### Session 은 서버에서 관리할 필요가 없는가 ? 

L4의 세션관리 체계가 sticky session 인지에 따라서 다르긴 하지만 사용자 경험을 위해서 관리하는게좋다.

서버가 '죽었을 때' 대책을 생각해야 한다.
- redis 서버가 죽으면 모든 사용자가 로그아웃이 된다.
- sticky session 을 이용할 때 Redis로 세션을 관리하면 하나의 서버가 죽었을 때 로그인 상태가 유지된다. 
- 사용자 경험에 초점

데이터 공유
- redis 에서 데이터를 관리하지 않으면 하나의 서버에서만 데이터를 공유하고 있는데
- 서버가 죽는다는 가정하에도 모든 동일한 최신 데이터를 바라본다.
- 데이터의 무결성 