
레이어드 아키텍쳐 
- `Service` —(직접 참조)—> `JpaRepository` (Infrastructure)
- DB 기술을 바꾸거나 테스트할 때 `Service` 코드도 영향을 받습니다. 서비스가 DB의 노예가 된 셈이죠.

클린 아키텍쳐 : 