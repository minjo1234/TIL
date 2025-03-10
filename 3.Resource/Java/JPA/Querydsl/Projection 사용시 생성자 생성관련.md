
querydsl의 Projection을 사용하다보니 쿼리문에 따라서 늘어나는 것에 불편함을 느껴 왜 컬럼에 맞춰 생성자를 사용해줘야 하는지에 대한 궁금증이 생겼음.

### 1.Projection Constructor 를 사용하면, 명확한 생성자가 필요

```java

List<UserDTO> users = queryFactory
	.select(Projections.constructor(UserDTO.class, user.id, user.name, user.email))
	.from(user)
	.fetch();
```


해당 쿼리처럼 작성하게 될 경우 QueryDSL에서 해당 DTO를 찾아서 매핑하려고 합니다.
만약 UserDTO에 Long id, String name, String email을 가진 생성자가 존재하지 않을 경우 오류가 발생함.

----

### 2.Projection 쓰면서 생성자 작성 안하는 법 -> Projection.fields(), Projection.bean() 


> [!Projection 사용 시 추가 생성자 생성 안하는 법] 
> 
> - Projection.fields()
> - Projection.bean() 




#### 2-1 Projection.fields

```
```




------
