
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

adap