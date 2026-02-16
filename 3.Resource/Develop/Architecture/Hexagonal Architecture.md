
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

