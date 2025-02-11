

```java

private final JPAQueryFactory jpaQueryFactory;  
private final QBusinessDirector qBusinessDirector = QBusinessDirector.businessDirector;  
private final QUserEntity qUser = QUserEntity.userEntity;  
private final QUserEntity qUser2 = QUserEntity.userEntity;  
private final QDepartmentEntity qDepartment = QDepartmentEntity.departmentEntity;  
private final QDepartmentEntity qDepartment2 = QDepartmentEntity.departmentEntity;


```


querydsl 에서는 JPA를 기반으로 생성된 Q객체(쿼리 전용 메타모델 객체) 를 이용하여  
싱글톤 정적

SQL 쿼리를 타입 안전하게 출력하며
컴파일 타임에 오류를 해결 
엔티티의 구조와 필드정보를 담은 쿼리 메타모델 