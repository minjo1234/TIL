
### 레이어드 아키텍쳐 

- 장점 : 구현 속도가 빠르다
- 단점 : 결합도, 기술교체, 유지보수 비용이 증가할 수 있다.
- Service —(직접 참조)—> `JpaRepository` (Infrastructure)
- DB 기술을 바꾸거나 테스트할 때 `Service` 코드도 영향을 받습니다. 서비스가 DB의 노예가 된 셈

### 클린 아키텍쳐 : 

- 장점 : 결합도, 기술교체, 서비스 로직만의 테스트가 가능하다.
- 단점 : 클래스 파일이 늘어난다. Domain 엔티티와 DB 엔티티
-  Service —(참조)—> `OrderRepository` **[인터페이스]** (Domain/Core 폴더에 위치)
- JpaOrderRepository **[구현체]** —(상속/구현)—> `OrderRepository` (Infrastructure 폴더에 위치)



결합도가 낮아지고 (Decoupling)
기술 교체가 쉬워지며 (Flexibility)
DB 없이도 서비스 로직만 떼어내서 테스트하기가 매우 편해집니다. (Testability)