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

더욱 상세하면 설명하자면
- 코드 상에서 에러(Exception)이 발생하거나 
- DB작업(쿼리)가 실패하면 트랜잭션은 `ROLLBACK` 된다.
- 모든 코드와 DB 쿼리가 정상적으로 작동하여야 트랜잭션이 커밋(Commit) 된다.


#### 🚨  조심할 점

- **런타임 예외(RunTimeException)가** 발생하면 트랜잭션은 자동으로 `ROLLBACK`
- **체크 예외(Exception)은** 자동으로 `ROLLBACK`되지 않음
  → 필요하면 `@Transactional(rollbackFor = Exception.class)` 이렇게 설정
- **DB 레벨 에러**(ex. 제약조건 위반, Deadlock 등)가 발생하면 → 역시 롤백돼.






`rollbackFor`, `propagation`, `isolation` 같은 고급 옵션도 알려줄게. (트랜잭션 진짜 제대로 쓰려면 이것들도 알아야 하거든!)


---



### 2.@Transactional 을 사용해야 하는 상황 

그렇다면 `@Transactional` 을 사용해야 하는 상황은 언제일까 ? 

개념적으로 이해한다면
트랜잭션은 **"어떤 작업을 하나의 논리적 단위로 보고" 성공/실패를 원자적으로 관리**할 때 필요.
작업을 모두 성공시키거나, 모두 취소시켜야 하는가를 기준으로 선택한다.
-> 이것을 3개(쓰기 작업, 복잡한 읽기 작업, 트랜잭션이 필요없는 경우)의 큰 틀로 정의하고자 한다.

1.쓰기 작업("변경 작업")을 할 때 
- insert, update, delete 

---





| insert, update, delete | 쓰기작업 | 무조건 필요                                          |
| ---------------------- | ---- | ----------------------------------------------- |
| 복잡한 select             |      | 상황에 따라 필요(여러 테이블 join, 조회 중간에 상태가 변할 위험이 있는 경우) |
| select                 |      |                                                 |
