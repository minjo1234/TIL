---
aliases:
  - 013 Transaction 특정(ACID)
tags:
  - DB
  - Transaction
author: Min Jo
created: 2025-04-26
---
# Transaction 특성 (ACID) 
---
### [✔️](https://engineerinsight.tistory.com/210#%E2%9C%94%EF%B8%8F%20%EA%B0%9C%EB%85%90-1)  트랜잭션에는 4가지 특성이 존재한다.  

줄임말로 ACID(Atomity, Consistency, Isolation, Durability) 라고하며 해당 특성(규칙)을 
모두 보장하여 데이터베이스 트랜잭션이 안전하게 수행되어야 한다.
데이터베이스 작업에 따라 ACID 속성이 있다면, ACID 트랜잭션이라 부르면 되고, 
이런 작업을 적용하는 데이터 스토리지 시스템을 트랜잭션 시스템이라고 한다.
한 테이블의 읽기, 쓰기 또는 수정 작업이 각각 다음과 같은 속성을 가지고있다.

---

### 원자성(Atomity) - 전체를 실행하거나 어떤 부분도 실행되지 않아야한다.
ex) 스트리밍 데이터 소스가 갑자기 오류를 일으키더라도 데이터 손실과 손상이 방지 

### 일관성(Consistency) - 테이블에 변경 사항을 적용할 때 미리 적용된, 예측할 수 있는 방식만 취득(feat:) 트랜잭션 annotation) 

- DB 자체의 무결성 제약조건(NOT NULL, FOREIGN KEY, UNIQUE 등)
- 스키마 정의(데이터 타입, 제약사항)
- 비즈니스 로직 상의 규칙(Transactional Annotation)

---
### 고립성(Isolation) - 여러 트랜잭션이 동시에 실행될 때, **서로 간섭하지 않도록 보장**하는 성질

- 각 트랜잭션이 독립적으로 실행된 것처럼 보이게 만든다.
- DBMS에서는 이를 위해 **동시성 제어**를 수행한다.

---
### 동시성 제어 

만약 하나의 트랜잭션이 종료된 이후 다음 트랜잭션이 시작된다면 DB의 성능은 바닥으로 향할 것이다.
하지만 동시에 여러 트랜잭션이 실행되더라도 **고립성을 어느 정도 보장하면 성능도 확보**할 수 있을 것이다. 

그리하여 **동시성 제어**라는 것을 방안이 탄생하게 된 것이다.

### 🔧 주요 방식:

DBMS(Oracle, Mariadb, PostgreSQL)에서 동시성 방법을 정해 놓는 방식으로 진행된다. 

|방식|설명|
|---|---|
|**락(Lock)**|자원을 점유해서 다른 트랜잭션이 접근하지 못하게 함. 대표: 2단계 잠금(2PL)|
|**MVCC (다중 버전 동시성 제어)**|트랜잭션마다 데이터의 스냅샷을 제공하여 락 없이도 읽기 가능 (예: PostgreSQL, Oracle 일부 등)|
|**타임스탬프 기반 제어**|트랜잭션 시작 시간을 기준으로 순서를 관리해 충돌 방지|

하지만 이렇게 DBMS에서 미리 선택해 둔 동시성 제어 방식을 사용한다면 1차로 사용자가 현재
사용하는 DBMS에서의 동시성을 제어하는 방식을 이해하고 DB를 사용하면 되지만
특이한 경우로 다르게 트랜잭션을 제어하고 싶다면 개발자가 Isolation Level을 선택하여 
DBMS를 다루면 되는것이다.

## ✅ 상관관계 핵심 요약

> **동시성 제어 방식은 "어떻게" 고립성을 구현할지에 대한 내부 메커니즘이고,  
> Isolation Level은 "얼마나" 고립시킬지를 개발자가 조절하는 외부 설정입니다.**


필자는 현재 MariaDB를 사용하고 있기에 MariaDB를 기준으로 Isolation Level을 정의하고자 한다.
## 🔁 예를 들어 보자 (MariaDB 기준)

| Isolation Level        | 읽기 동작         | InnoDB 내부 처리 방식                    | 발생 가능 현상               |
| ---------------------- | ------------- | ---------------------------------- | ---------------------- |
| **READ UNCOMMITTED**   | 변경 전 값까지 읽음   | 거의 제약 없음, MVCC로 undo 로그도 무시        | Dirty Read 발생 가능       |
| **READ COMMITTED**     | 커밋된 값만 읽음     | MVCC를 사용하여 undo 로그에서 최신 커밋만 반영     | Non-repeatable Read 가능 |
| **REPEATABLE READ** ⭐️ | 트랜잭션 내에서 동일값  | MVCC로 Snapshot 고정, Phantom Read 막음 | 기본값, 성능-일관성 균형         |
| **SERIALIZABLE**       | 트랜잭션 직렬 실행 수준 | Lock을 더 많이 사용 (읽기도 공유락)            | 가장 안전하지만 느림            |

---

#### 2. **Isolation Level (개발자가 선택)**

- Read Uncommitted
- Read Committed
- Repeatable Read
- Serializable


ex) 필자는 MariaDB를 사내에서 사용중인데 

## 🧩 1. 동시성 제어 (Concurrency Control)

동시성 제어는 **여러 트랜잭션이 동시에 실행될 때 데이터의 일관성을 유지**하기 위해 DBMS가 사용하는 기술입니다.

### 대표적인 기법

| 기법                      | 설명                                     | 대표 DBMS                                    |
| ----------------------- | -------------------------------------- | ------------------------------------------ |
| **Lock (잠금)**           | 트랜잭션이 데이터에 접근할 때 락을 걸어 다른 트랜잭션의 접근을 제어 | Oracle, MySQL(InnoDB), MSSQL               |
| **MVCC (다중 버전 동시성 제어)** | 데이터를 수정할 때 새로운 버전을 만들어 읽기와 쓰기를 분리      | PostgreSQL, MySQL(InnoDB), MariaDB(InnoDB) |
| **Timestamp Ordering**  | 각 트랜잭션에 타임스탬프 부여 → 순서 기반으로 충돌 해결       | 일부 고성능 DBMS 또는 이론적 모델                      |

> **MariaDB의 InnoDB 엔진은 MVCC + Lock을 함께 사용합니다.**  
> → 읽기: MVCC (비차단) / 쓰기: Lock 사용 (차단)
> Oracle 
> → 읽기 : MVCC (비차단) / 쓰기 : Lock 사용 (차단)

---

### 영속성(Durability)
- 트랜잭션이 성공적으로 완료되면 결과는 영구적으로 반영되야한다.
- 데이터베이스가 손실되더라도 트랜잭션의 결과는 보존  
- **커밋이 완료된 이후에는 무슨 일이 있어도 결과를 보존한다.**

예: DB 서버가 갑자기 꺼지거나 전원이 나가도, 다시 부팅했을 때 그 트랜잭션 결과는 여전히 DB에 반영되어 있어야 함.

---
### 3.Transaction 특성 요약  

| **Atomity**     | 원자성 | 트랜잭션은 전부 실행되거나 전혀 실행되지 않아야 한다  |
| --------------- | --- | ------------------------------ |
| **Consistency** | 일관성 | 트랜잭션 전후의 데이터는 항상 제약조건을 만족해야 한다 |
| **Isolation**   | 고립성 | 동시에 실행돼도 트랜잭션끼리 서로 간섭하지 않아야 한다 |
| **Durability**  | 영속성 | 커밋된 트랜잭션의 결과는 시스템 장애가 나도 보존된다  |

---

일반적으로 개발자들은 트랜잭션을 직접 제어하기보다는 프레임워크(Spring, JPA) 또는 자동 커밋에 맡기기 때문에 

	개발자 입장에서는 "명시적인 트랜잭션 없이도 MVCC가 어떻게 작동하느냐 ?" 에 집중을 하면 좋을 것 같다.




https://www.databricks.com/kr/glossary/acid-transactions



---

## 💡 시나리오 예시

sql

CopyEdit

`-- 트랜잭션 A (SELECT) SELECT balance FROM account WHERE id = 1;  -- 동시에 트랜잭션 B (UPDATE) UPDATE account SET balance = balance + 1000 WHERE id = 1;`

---

## 📌 관건은?

**트랜잭션 A가 balance를 읽을 때**,  
트랜잭션 B가 **업데이트한 값**을 **읽을 수 있느냐 없느냐**입니다.



---


## 📌 관건은?

**트랜잭션 A가 balance를 읽을 때**,  
트랜잭션 B가 **업데이트한 값**을 **읽을 수 있느냐 없느냐**입니다.

---

## 🔒 1. 동시성 제어 방식 (MariaDB 기준 InnoDB)

|구분|설명|
|---|---|
|**읽기 (SELECT)**|**MVCC** 사용 → 비차단 읽기 (스냅샷 기반)|
|**쓰기 (UPDATE)**|**Lock** 사용 → 해당 row에 쓰기 락 (exclusive lock)|

즉, **읽기에서는 락을 걸지 않고 스냅샷을 이용해 읽고**,  
**쓰기에서는 row-level 락을 걸어 다른 트랜잭션의 수정을 막습니다.**

---

## 🔐 2. Isolation Level에 따른 차이

### 🔸 READ COMMITTED (MariaDB 기본값)

- **항상 커밋된 최신 데이터만 읽음**
    
- 트랜잭션 A가 balance를 조회할 때,  
    **트랜잭션 B가 커밋했다면 변경된 balance를 읽음**
    
- → 커밋 전이라면 읽지 않음 (dirty read 방지)
    

### 🔸 REPEATABLE READ

- **트랜잭션이 시작된 시점의 스냅샷을 계속 사용**
    
- 트랜잭션 A가 트랜잭션 시작 후 한 번이라도 읽었다면,  
    이후 SELECT에서도 **항상 같은 balance값**을 받음
    
- 트랜잭션 B가 나중에 balance를 업데이트하고 커밋해도  
    A는 **그 변경을 절대 못 봄 (phantom read 방지)**
    

---

## 📷 예시 타임라인 (READ COMMITTED 기준)

text

CopyEdit

`시간순서: 1. 트랜잭션 A 시작 2. 트랜잭션 B 시작 3. 트랜잭션 B -> balance = 15000 으로 UPDATE 4. 트랜잭션 B COMMIT 5. 트랜잭션 A -> SELECT balance → 읽은 값: 15000 (커밋된 값)`

---

## 📷 예시 타임라인 (REPEATABLE READ 기준)

text

CopyEdit

`시간순서: 1. 트랜잭션 A 시작 2. 트랜잭션 A -> SELECT balance → 읽은 값: 10000 3. 트랜잭션 B 시작 4. 트랜잭션 B -> balance = 15000 으로 UPDATE 5. 트랜잭션 B COMMIT 6. 트랜잭션 A -> SELECT balance → 여전히 10000`

---

## ✅ 결론

- **동시성 제어는 스냅샷(MVCC)과 락(lock)으로 이루어짐**
    
- **Isolation Level**에 따라 **SELECT가 읽는 데이터가 달라질 수 있음**
    
- 대부분의 경우, **동시성 성능과 일관성 정확도 사이에서 트레이드오프**가 존재함
    

---

혹시 이걸 코드 수준에서 예시로 보여드릴까요?  
Spring JPA 기준이나, 순수 SQL 기준 모두 가능합니다.
