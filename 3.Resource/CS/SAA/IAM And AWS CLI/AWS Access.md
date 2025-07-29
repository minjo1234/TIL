
## How can users access AWS ? 


- To access AWS, you have three options 
	- AWS Management Console (protected by password + MFA)
	- AWS Command Line Interface (CLI) : protected by access keys 
	- AWS Software Developer Kit (SDK) - for code : protected by access keys 
- Access Keys are generated through the AWS Console 
- Users manage their own access keys 
- Access Keys are secret, just like a password, Don't share them 
- Access Key ID ~= username 
- Secret Access Key ~= password 

## Example (Fake) Access Keys 

 - **Remember: don't share your access keys** 


## What's the AWS SDK ? 

- AWS Software Development Kit (AWS SDK)
- Language-specific APIS (set of libraries)
- Enables you to access and manage AWS services programmatically 
- Embedded within your application 
- Supports 
	- SDKs (Javascript, Python, PHP, NET, Ruby, java, GO, Node.js, C++)
	- Mobile SDKS (Android, iOS)
	- 



------

## AWS CLI Access Key


![[Pasted image 20250729130019.png]]


---

#### **AWS CloudShell: 리전 가용성**


## AWS CloudShell
curl -u "Jomin011208:ATBBDxnpP7WxGhuRCPRpFwYHFuxxC56C6308" \
-X POST "https://api.bitbucket.org/2.0/repositories/goodmit1/posco_deployment/downloads" \
--form files=@clovirone2.0.tar.gz.part_ad