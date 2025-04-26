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


### 원자성(Atomity) - 전체를 실행하거나 어떤 부분도 실행되지 않아야한다.
ex) 스트리밍 데이터 소스가 갑자기 오류를 일으키더라도 데이터 손실과 손상이 방지 

### 일관성(Consistency) - 테이블에 변경 사항을 적용할 때 미리 적용된, 예측할 수 있는 방식만 취득(feat:) 트랜잭션 annotation) 

- DB 자체의 무결성 제약조건(NOT NULL, FOREIGN KEY, UNIQUE 등)
- 스키마 정의(데이터 타입, 제약사항)
- 비즈니스 로직 상의 규칙(Transactional Annotation)


### 고립성

### 영속성





---

### 3.Transaction 특성 요약 

| **Atomity**     | 원장성 |     |
| --------------- | --- | --- |
| **Consistency** | 일관성 |     |
| **Isolation**   | 고립성 |     |
| **Durability**  | 영속성 |     |


https://www.databricks.com/kr/glossary/acid-transactions
