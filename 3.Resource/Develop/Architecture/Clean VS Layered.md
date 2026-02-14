
### 레이어드 아키텍쳐 

- 장점 : 구현 속도가 빠르다
- 단점 : 결합도, 기술교체, 유지보수 비용이 증가할 수 있다.
- Service —(직접 참조)—> `JpaRepository` (Infrastructure)
- DB 기술을 바꾸거나 테스트할 때 `Service` 코드도 영향을 받습니다. 서비스가 DB의 노예가 된 셈

### 클린 아키텍쳐 : 

- 장점 : 결합도, 기술교체, 서비스 로직만의 테스트가 가능하다.
- 단점 : 클래스 파일이 늘어난다. 
	- Domain 엔티티와 DB 엔티티 (DB 엔티티는 비즈니스 로직처리를 위함, DB 엔티티는 종속되지 않도록 구현)
- Service —(참조)—> `OrderRepository` **[인터페이스]** (Domain/Core 폴더에 위치)
- JpaOrderRepository **[구현체]** —(상속/구현)—> `OrderRepository` (Infrastructure 폴더에 위치)


PrmQL을 활용한 메트릭수집
AZ-120 자격증 보유
CKA까지 있으면 더 좋을듯

테스트 코드 작성에 익숙하신 분 - 테스트 코드를 많이 작성해야겠다.