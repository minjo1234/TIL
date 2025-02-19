

```java

private final JPAQueryFactory jpaQueryFactory;  
private final QBusinessDirector qBusinessDirector = QBusinessDirector.businessDirector;  
private final QUserEntity qUser = QUserEntity.userEntity;  
private final QUserEntity qUser2 = QUserEntity.userEntity;  
private final QDepartmentEntity qDepartment = QDepartmentEntity.departmentEntity;  
private final QDepartmentEntity qDepartment2 = QDepartmentEntity.departmentEntity;


```


querydsl 에서는 JPA를 기반으로 생성된 Q객체(쿼리 전용 메타모델 객체) 를 이용하여  
싱글톤 정적 객체 (new 를 이용하지 않고 메모리 절약 ) - 애플리케이션이 실행될때만 생성 

왜 싱글톤인지 ?  들어가보면 static final로 설정되어있음


```java
public static final QUserEntity userEntity = new QUserEntity("userEntity");
```

SQL 쿼리를 타입 안전하게 출력하며
컴파일 타임에 오류를 해결 
엔티티의 구조와 필드정보를 담은 쿼리 메타모델 


1.버튼을 누름
2.salesmanagerRecord조회 -> fiscalYear, departmentIds
3.uses테이블과 비교해서 기존에 존재하는 salesmanagerRecord의 userId 값이 user의 id값과 다른것만 insert
4.insert이후에 

---


육현근이사님 ->

data-input
dateContainer