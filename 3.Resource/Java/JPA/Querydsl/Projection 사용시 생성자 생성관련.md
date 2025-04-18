
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

### 2.Projection 쓰면서 생성자 작성 안하는 법 


> [!Projection 사용 시 추가 생성자 생성 안하는 법] 
> 
> - Projection.fields()
> - Projection.bean() 



#### 2-1 Projection.fields()

```java
List<UserDTO> users = queryFactory
	.select(Projections.fields(UserDTO.class, user.id, user.name, user.email))
	.from(user)
	.fetch();
```


**주의점**

- 매핑하는 컬럼명과 이름이 동일해야한다. 
- 필드명과 컬럼명이 다르다면 Expression.as 를 사용하여 별칭사용

---

#### 2-2 Projection.bean() 

```java
List<UserDTO> users = queryFactory
	.select(Projections.bean(UserDTO.class), user.id, user.name, user.email)
	.from(user)
	.fetch()
	
```

- Java Bean의 규칙을 따른다.
- 기본 생성자와 Setter가 필수적으로 필요하다.

------

#### 요약 

| Projections 방식                  | private 필드 접근 가능 여부 | Setter 필요 여부 | 주입 방식                                 |
| ------------------------------- | ------------------- | ------------ | ------------------------------------- |
| **`Projections.fields()`**      | ✅ 가능                | ❌ 필요 없음      | **리플렉션을 사용하여 private 필드에 직접 값 주입**    |
| **`Projections.bean()`**        | ❌ 불가능               | ✅ 필요         | **기본 생성자로 객체 생성 후 Setter를 이용하여 값 주입** |
| **`Projections.constructor()`** | ❌ 불가능               | ❌ 필요 없음      | **생성자를 호출하여 값 주입**                    |



---


### + 리플렉션이란 ?
