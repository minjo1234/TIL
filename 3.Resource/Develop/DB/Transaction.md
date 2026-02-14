
### 트랜잭션의 동작 방식

1.프록시 호출 : 사용자가 메서드를 호출하면, 스프링이 만든 프록시 객체가 요청을 가로챈다.

2.트랜잭션 시작
- 프록시가 실제 로직을 수행하기전에, 데이터베이스 커넥션을 확보하고
- `Auto-commit` false로 설정하여 로직이 완료되기전에 commit 을 방어합니다.

3.비즈니스 로직 실행

4.결과에 따른 분기

- 정상 종료 : DB Commit 
- 예외 발생 : Rollback

5.자원 반납 : DB 커넥션 풀을 다시 반납한다.

---
### Isolation Level


DB type 별로 다르다. 


**MySQL (InnoDB):** `REPEATABLE READ`
**PostgreSQL / Oracle / SQL Server:** `READ COMMITTED`