
- Java 진영에서 ORM(Object Relation Mapping) 기술 표준으로 사용하는 인터페이스 모음
- 자바 어플리케이션에서 RDB 사용하는 방식을 정의한 인터페이스 
- 인터페이스이기 때문에 hibernate, OpenJPA 등이 JPA를 구현함


- 궁금증 JPA 가 인터페이스 모음이라고 했는데 어떠한 인터페이스들이 존재하는지

| EntityManager        | 데이터베이스 작업(삽입, 삭제, 수정, 조회)을 관리하는 인터페이스 |
| -------------------- | -------------------------------------- |
| EntityManagerFactory |                                        |
| Query                |                                        |
|                      |                                        |


- hibernate가 구현될것을 코딩으로 예시를 든다면?
- 
