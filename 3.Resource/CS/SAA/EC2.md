
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

## IAM - Password Policy 


user and user groups has two defence mechanisms

- Strong passwords = higher security for your account 
- In AWS, you can setup a password policy 
	- Set a minimum password length
	- Require specific character types: 
		- including uppercase letters 
		- lowercase letters
		- numbers 
		- non-alphanumeric characters 
	-  Allow all IAM users to change their own passwords 
	-  Require users to change their password after some time (password expiration)
	- Prevent password re-use


Multi Factor Authentication - MFA 

- Users have access to your account and can possibly change
configurations or delete resources in your AWS account 
- You want to protect your root Accounts and IAM users
- MFA = password you know + security device you own 

### Main benefit of MFA
 if a password is stolen or hacked, the account is not compromised 


---


## Amazone EC2 

- EC2 is one of the most popular of AWS offering 
- EC2= Elastic Compute Cloud = Infrastructure as a service 
- It mainly consists in the capability of : 
	- Renting virtual machines (EC2)
	- Distributing load across machines (ELB)
	- Scaling the services using an autop-scaling group (ASG)

- Knowing EC2 is fundamental to understand how the Cloud works 


## EC2 sizing & configuration options 

- Operating System (OS): Linux, Windows or Mac OS
- How much compute power & cores (cpu)
- How much random-access memory (RAM)
- How much storage space:
	- Network-attached (EBS & EFS)
	- hardware (EC2 Instance Store)
- Network card speed of the card, Public IP address 
- Firewall rules: security group 
- Bootstrap script (configure at first launch): EC2 User Data 


## EC2 User Data 

- It is possible to bootstrap our instances using an EC2 User data script 
- bootstrapping means launching commands when a machine starts 
- That script is only run once at the instance first start 
- EC2 user data is used to automate boot tasks such as:
	- Installing updates 
	- Installing software 
	- Downloading common files from the internet 
	- Anything you can think o