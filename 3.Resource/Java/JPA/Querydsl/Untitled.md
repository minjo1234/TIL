

```java

private final JPAQueryFactory jpaQueryFactory;  
private final QBusinessDirector qBusinessDirector = QBusinessDirector.businessDirector;  
private final QUserEntity qUser = QUserEntity.userEntity;  
private final QUserEntity qUser2 = QUserEntity.userEntity;  
private final QDepartmentEntity qDepartment = QDepartmentEntity.departmentEntity;  
private final QDepartmentEntity qDepartment2 = QDepartmentEntity.departmentEntity;


```


querydsl 에서는 JPA를 기반으로 생성된 Q객체를 이용하여 