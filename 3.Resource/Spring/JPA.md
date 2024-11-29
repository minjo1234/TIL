
- Java 진영에서 ORM(Object Relation Mapping) 기술 표준으로 사용하는 인터페이스 모음
- 자바 어플리케이션에서 RDB 사용하는 방식을 정의한 인터페이스 
- 인터페이스이기 때문에 hibernate, OpenJPA 등이 JPA를 구현함


---

- 궁금증 JPA 가 인터페이스 모음이라고 했는데 어떠한 인터페이스들이 존재하는지

### 주요 JPA 인터페이스

| EntityManager        | 데이터베이스 작업(삽입, 삭제, 수정, 조회)을 관리하는 인터페이스 |
| -------------------- | -------------------------------------- |
| EntityManagerFactory | EntityManager 인스턴스를 생성하는 팩토리 인터페이스     |
| Query                | 쿼리를 실행하는데 사용되는 인터페이스                   |
| CriteriaBuilder      | 타입 세이프하고 동적으로 쿼리를 생성하는데 사용             |
| Transaction          | 데이터베이스 트랜잭션을 관리                        |
| PersistenceUnitInfo  |                                        |
|                      |                                        |
|                      |                                        |
- UserRepository가 인터페이스로 존재해야 하는 이유 
- 클래스는 기본적으로 정적인 구조
- 인터페이스는 기본적으로 동적인 구조이다.
- 만약 UserRepository를 class로 정의하게되면 확장이 불가능하기때문에 findById
```java
public interface UserRepository extends JpaRepositories<User, Long> 
```

