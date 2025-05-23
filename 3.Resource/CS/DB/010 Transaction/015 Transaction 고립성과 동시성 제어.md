---
aliases:
  - 015 Transition 고립성과 동시성 제어
tags:
  - DB
  - Transaction
author: Min Jo
created: 2025-05-01
---
# 015 트랜잭션의 고립성과 동시성 제어 - 성능은 어떻게 유지될까?
-----

트랜잭션(Transaction)의 특징 중 하나인 **고립성(Isolation)**에 대해 공부하던 중 한 가지 의문이 들었습니다.

>**"고립성 때문에 트랜잭션이 순차적으로만 실행된다면, DB 성능은 매우 낮아지는 것 아닌가?"**

하지만 실무에서는 수많은 트랜잭션이 동시에 수행되면서도 성능이 잘 나옵니다.  
어떻게 이러한 성능 저하를 방지하고, 동시에 고립성을 보장할 수 있는 걸까요?

---


### 🔐 고립성(Isolation) 개념 다시 보기

Isolation은 하나의 트랜잭션이 수행 중일 때, **다른 트랜잭션이 그 중간 상태를 볼 수 없도록 보장**하는 성질입니다.  
즉, 격리된 상태로 트랜잭션이 동작해야 데이터의 정합성이 보장됩니다.
그렇다고 모든 트랜잭션을 **순차적으로 처리**한다면? → **성능이 심각하게 떨어집니다.**
그래서 필요한 것이 바로 **동시성 제어(Concurrency Control)**입니다.

----

### 👨‍💻 동시성 제어란?   - 읽기 성능을 위한

동시성 제어는 여러 트랜잭션이 동시에 데이터에 접근해도 정합성을 유지하면서 성능도 확보할 수 있게 만드는 기술입니다. DBMS는 내부적으로 다음과 같은 기법 중 하나를 사용합니다.

| 방식                      | 설명                                                             |
| ----------------------- | -------------------------------------------------------------- |
| **락(Lock)**             | 자원을 점유해서 다른 트랜잭션이 접근하지 못하게 함. 대표: 2단계 잠금(2PL)                  |
| **MVCC (다중 버전 동시성 제어)** | 트랜잭션마다 데이터의 스냅샷을 제공하여 락 없이도 읽기 가능 (예: PostgreSQL, Oracle 일부 등) |
| **타임스탬프 기반 제어**         | 트랜잭션 시작 시간을 기준으로 순서를 관리해 충돌 방지                                 |

> 그리고 여기서 한 가지 더 중요한 점은,  
> **개발자 역시 트랜잭션 간의 고립 정도를 선택할 수 있다는 것**이다.
---
### Isolation Level - 논리적인 일관성 수준 

개발자가 선택할 수 있는 고립성 수준은 다음과 같습니다:

| Level            | 설명                               | MariaDB(InnoDB) 처리 방식   | 발생 가능한 문제              |
| ---------------- | -------------------------------- | ----------------------- | ---------------------- |
| READ UNCOMMITTED | 커밋되지 않은 데이터까지 읽을 수 있음 (가장 낮은 수준) | 거의 제약 없음                | Dirty Read 발생 가능       |
| READ COMMITTED   | 커밋된 데이터만 읽음                      | MVCC를 사용하여 Undo 로그 참조   | Non-repeatable Read 가능 |
| REPEATABLE READ  | 트랜잭션 내에서는 동일한 쿼리 결과 보장           | MVCC로 스냅샷 고정, 팬텀 리드도 방지 | **MySQL 기본값**, 균형적     |
| SERIALIZABLE     | 트랜잭션을 직렬 처리 수준으로 강하게 고립          | 공유 락까지 사용               | 가장 안전하지만 **가장 느림**     |

> 📎 **Note**: MySQL(InnoDB)은 REPEATABLE READ에서도 팬텀 리드를 방지하지만, 대부분의 DB는 그렇지 않습니다.

---

##  MariaDB의 동시성 제어 방식

MariaDB(필자는 MariaDB를 사용하고 있기에 ) (InnoDB)는 **읽기와 쓰기에 대해 서로 다른 동시성 제어 방식**을 사용합니다:

읽기 (SELECT)
	- 트랜잭션 시작 시점의 데이터를 Snapshot으로 읽습니다.
	- 다른 트랜잭션의 변경 사항은 **커밋되더라도 반영되지 않음**.
	- 락이 걸리지 않기 때문에 **다른 트랜잭션을 기다릴 필요 없음**.
	- 따라서 **읽기 성능이 매우 우수**합니다.

 쓰기 (INSERT / UPDATE / DELETE)
	- 변경되는 레코드에 대해 **Row-Level Lock**을 사용합니다.
	- 충돌 방지를 위해 **Exclusive Lock**을 걸고,
	- 쓰기 트랜잭션이 많아질수록 **대기, 결함, 데드락**이 발생할 수 있습니다.

---

### 예시로 동시성 이해하기.

```java
-- 트랜잭션 A
START TRANSACTION;
SELECT * FROM user WHERE id = 1; -- 스냅샷 읽기 (MVCC)

-- 트랜잭션 B
START TRANSACTION;
UPDATE us
```

- 트랜잭션 A가 어떤 데이터를 읽고 있어도,
- 트랜잭션 B는 그 데이터를 자유롭게 수정할 수 있습니다.
- 두 트랜잭션은 서로 대기하지 않고 독립적으로 실행됩니다.
- 즉, **읽는 동안 다른 트랜잭션을 기다리지 않기 때문에 동시성이 매우 높다.**

---
### 예시로 고립성레벨 이해하기 

위에서 언급한 **동시성 제어**가 성능에 영향을 미친다면, 이번에는 **고립성 레벨**에 따라 데이터의 **논리적인 일관성**이 달라질 수 있습니다.**

#### 고립성 레벨에 따른 동작

**REPEATABLE READ** (기본 고립성 수준)

- 트랜잭션 A가 데이터를 읽으면, **트랜잭션 A 내에서 해당 데이터는 변경되지 않습니다.**
- 즉, 트랜잭션 B가 데이터를 업데이트해도, 트랜잭션 A는 처음 읽었던 값을 그대로 읽습니다.
- 이 레벨에서는 **Phantom Read**도 방지되며, **Non-repeatable Read**도 발생하지 않습니다.
- 트랜잭션 A가 읽은 데이터는 트랜잭션이 종료될 때까지 **변경되지 않습니다.**

```sql
-- 트랜잭션 A
START TRANSACTION;
SELECT * FROM user WHERE id = 1; -- A가 데이터를 읽음

-- 트랜잭션 B
START TRANSACTION;
UPDATE user SET name = 'Kim' WHERE id = 1; -- B가 데이터를 업데이트

-- 트랜잭션 A
SELECT * FROM user WHERE id = 1; -- A가 다시 데이터를 읽음 (변경된 값은 영향을 미치지 않음)
COMMIT;
```

**READ COMMITTED** (또 다른 고립성 수준)

- 트랜잭션 A가 데이터를 읽을 때, **트랜잭션 B가 데이터를 커밋하기 전까지는 그 값을 읽지 않습니다.**
- 즉, **트랜잭션 A는 다른 트랜잭션의 커밋된 데이터만 볼 수 있습니다.**
- 트랜잭션 B가 커밋되면 트랜잭션 A가 **B가 커밋한 값을 읽을 수 있게** 됩니다. 이는 **Non-repeatable Read**(같은 트랜잭션 내에서 다른 값)를  발생시킬 수 있습니다.

```sql
-- 트랜잭션 A
START TRANSACTION;
SELECT * FROM user WHERE id = 1; -- A가 데이터를 읽음

-- 트랜잭션 B
START TRANSACTION;
UPDATE user SET name = 'Kim' WHERE id = 1; -- B가 데이터를 업데이트
COMMIT; -- B가 커밋을 실행

-- 트랜잭션 A
SELECT * FROM user WHERE id = 1; -- A는 이제 B가 커밋한 변경된 값을 읽음
COMMIT;
```

---
### ✅ 요약: 고립성과 성능은 어떻게 공존하는가?

- 고립성은 트랜잭션 간 간섭을 막아 데이터 정합성을 보장하지만, 성능 저하 요인이 될 수 있음.
- MariaDB(InnoDB)는 **MVCC + Row Lock**을 통해 **읽기/쓰기 분리 전략**으로 이 문제를 해결함.
- 개발자는 **상황에 따라 적절한 Isolation Level**을 선택하여 **정합성과 성능의 균형**을 조절할 수 있다.
- 자바 개발자는 @Transactional의 고립성을 결정하여 사용하면된다 
  
```java
 @Transactional(isolation = Isolation.REPEATABLE_READ) 
 
```

---
