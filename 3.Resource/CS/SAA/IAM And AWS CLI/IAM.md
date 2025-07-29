
## IAM : Users & Groups

- IAM = Identify and Access Management, Global Service 
- Root account created by default, shouldn't be used or shared 
- Users are people within your organization, and can be grouped 
- Groups only contains users, not other groups 
- Users don't have to belong to a group, and user can belong to multiple groups 


## IAM : Permissions

- Users or Groups can be assigned JSON documents called policies 
- Don't have to select regions 


## IAM Policies inheritance 


## IAM Policies Structure 

### Consists of 

- Version: Policy language version, always include '2012-10-17'
- Id: an identifier for the policy (optional)
- Statement: one or more individual statements (required)

----

### Statements consists of 

- Sid: an identifier for the statement (optional)
- Effect: whether the statement allows or denies access (Allow, Deny)
- Principal: account/user/role to which this policy applied to 
- Action: list of actions this policy allows or denies 


-----

## IAM Password Policy

- Strong passwords = higher security for your account 
- In AWS, you can setup a password policy 
	- Set a minimum password length 
	- Require specific character types:
	- including uppercase letters 
	- lowercase letters 
	- numbers 
	- non-alphanumeric characters 
- Allow all IAM users to change their own passwords 
- Require users to change their password after some time (password expiration)
- Prevent password re-use 


## Multi Factor Authentication - MFA 

- Users have access to your account and can possibly change 
configurations or delete resources in your AWS account 

- You want to protect your Root Accounts and IAM users 
- MFA = password you know + security device you own 

- Main benefit of MFA :
if a password is stolen or hacked, the account is not compromised 


## MFA devices options in AWS 

**virtual MFA device** : Support for multiple tokens on a single device/
**Universal 2nd Factor (U2F) Security Key** : Support for multiple root and IAM users using a single security key 
**Hardware Key Fob MFA Device** : 
**Hardware Key Fob MFA Device for AWS GovCloud (US)** :


---

## IAM Roles for Service 

- Some AWS service will need to  perform actions on your behalf 
- To do so, we will assign permissions to AWS services with IAM Roles 
- Common roles: 
	- EC2 Instance Roles 
	- Lambda Function Roles 
	- Roles for CloudFormation 


## IAM Security Tools 

- IAM Credentials Report (account-level)
	- a report that lists all your account's users and the status of their various crendentials 

- IAM Access Advisor (user-level)
	- Access advisor shows the service permissions granted to a user and when those services were last accessed 

---

## IAM Guidelines & Best Practices 

  - Don't use the root account except for AWS account 
  - On physical user = One AWS usersA
  - Assign users to groups and assign permissions to groups 
  - Create a strong password policy 
  - Use and enforce the use of Multi Factor Authentication (MFA)
  - Create and use Roles for giving permissions to AWS services 
  - Use Access Keys for Programmatic Access (CLI / SDK )
  - Audit permissions of your account using IAM Credentials Report & IAM 
	  Access Advisor 
	Never share IAM users & Access Keys 

---

## IAM Section - Summary 


**Users** : mapped to a physical user, has a password for AWS Console 
**Groups** : contains users only 
**Policies** : JSON document that outlines permissions for users or groups 
**Roles** : for EC2 instances AWS services 
**Security** : MFA + Password Policy 
**AWS CLI**: manage your AWS services using the command-line 
**AWS SDK**: manage your AWS services using a programming language 
**Access Keys**: access AWS using the CLI or SDK 
**Audit**: IAM Credential Reports & IAM Access Advisor 



---


- IAM 사용자들은 자신만의 자격증명 (샤용자 이름, 비밀번호, 엑세스 키)를 통해 AWS 서비스에 엑세스한다.  (관리자 x , root x)
 
- IAM 정책 : AWS 서비스에 요청을 생성하기 위한 일련의 권한을 정의, IAM 사용자, 사용자 그룹 및 IAM 역할에게 사용하게 될 JOSN 문서

- IAM 사용자 그룹은 IAM 사용자만을 포함할 수 있다.