
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

domain은 순수 도메인
application의 service는 순수 비즈니스 로직
adapter는 application에 들어오는 in과 out으로 분리되며 out에서 어떤 DB에 저장될지 설정된다.

Adpater In -> Application Port In -> Application Service -> Application Port out -> Adpater out 

Adpater In : Rest Controller 
Application Port In : 추상 메서드
Application Service : 메서드 구현체
Application Port out : Repository 인터페이스 
Adpater Out : JPA, Redis 등을 사용하여 


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