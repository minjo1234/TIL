
### Elastic Compute Cloud . 

the most important services on AWS ! 
It is the concept of renting a virtual computer from a region where Amazon provides services. . An instance is a unit used to create EC2, which means one computer, and when creating, you can select settings related to virtual servers such as OS (ubuntu, window)


- ECS: EC2 Container Service: EC2를 도커 컨테이너로 관리하도록 나온 서비스
- EB: Elastic Beanstalk: 웹 애플리케이션용 클라우드 플랫폼 서비스. 간단한 서비스 배포 용으로 사용
- AWS Lamda: AWS cloud function service. 서버 없이 작성한 프로그래밍 코드를 실행하는 환경을 제공 (serverless architecture 구현에 사용)


-------

### S3

Simple Stroage Service. 파일 서버

- 정적 요소인 이미지나 동영상을 가지고 있다가 제공한다.
- EC2와 다르게 무제한 저장이 가능해 주로 사용된다.


---

###  RDS

Relational Database Service: RDBMS 클라우드 서비스. 아마존 오로라, mysql, 마리아DB, PostgreSQL, 오라클 서버 등을 지원한다.

- DynamoDB: AWS의 NoSQL 데이터베이스 서비스

---


![[Pasted image 20250728165731.png]]


---

## IAM TemaMFA 


user and user groups has two defence mechanisms

- Strong passwords = higher security for your account 
- In AWS, you can set