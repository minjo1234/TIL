---
aliases:
  - 014 Transaction Annotation과 일관성(Consistency)
tags:
  - Transaction
  - DB
author: Min Jo
created: 2025-04-26
---
# Transaction Annotation과 일관성(Consistency)
---

Transaction의 특성중 C(Consistency)를 공부하는 도중 Transactional 어노테이션을 이용하면 
단순히 DB에서뿐만아니라 비즈니스로직과의 연결을 이용하여 하나의 메소드를 트랜잭션의 단위로 본다는 것을 알게되었다.

---
### 1.@Transactional

```java
# 개발자 입장에서 볼때의 Transaction의 단위를 어노테이션을 이용하여 구현하는 것이다.

@Transactional 
public void saveService(MyServiceDTO dto) {
		if(dto.size() < 0) {
			throw new IllegalArgumentException("아무것도 존재하지 않음");
		}
		
		save(dto);
	}


saveService라는 메소드를 하나의 트랜잭션으로 여기며, 

```


---



---



