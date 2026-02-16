
Hexagonal vs Clean Architecture 

```bash
└─ com.example.order
   ├─ domain (핵심 로직: Order 엔티티)
   ├─ application
   │  ├─ port
   │  │  ├─ in (UseCase: 주문하기)
   │  │  └─ out (Repository Port: 주문 저장하기)
   │  └─ service (비즈니스 로직 구현체)
   └─ adapter
      ├─ in (WebAdapter: REST Controller)
      └─ out (PersistenceAdapter: JPA Repository 구현체)
```

domain, application, adapter로 분리한다.

### 실행 흐름

Adpater In : Rest Controller 
Application Port In : 추상 메서드
Application Service : 메서드 구현체
Application Port out : Repository 인터페이스 
Adpater Out : JPA, Redis 등을 사용하여 DB에 저장한다.

### 의존성 흐름

**Adapter In** (Port In을 의존) → **Port In** (Service가 구현) → **Service** (Port Out을 사용) → **Adapter Out** (Port Out을 구현/의존) $\rightarrow$ **Port Out**

포트와 어댑터라는 구체적인 통신 인터페이스를 정의한다.


### 헥사고날 아키텍처 (2단 분리)

단순하게 **안(Inside)**과 **밖(Outside)**으로 나뉩니다.

- **안:** 도메인 모델과 이를 다루는 서비스 로직.
- **밖:** DB, 웹 UI, 외부 API 등 기술적인 구현체.
- **경계:** 포트(인터페이스)가 이 둘을 연결합니다.



```bash
└─ com.example.order
   ├─ entities (순수 비즈니스 객체: 규칙 포함)
   ├─ usecases (애플리케이션 특정 비즈니스 규칙: OrderInteractor 등)
   ├─ interface_adapters (전달받은 데이터를 변환)
   │  ├─ controllers
   │  ├─ presenters
   │  └─ gateways (DB 인터페이스 등)
   └─ frameworks_drivers (가장 바깥쪽)
      ├─ database (JPA, MyBatis)
      └─ ui (Web Framework)
```


