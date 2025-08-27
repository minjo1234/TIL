
**What is DNS** 

Domain Name System which translates the human friendly hostname into the machine IP Address 

- www.google.com -> 172.17.18.36

---
**DNS Terminologies**

- Domain Register: Amazon Route S3, GoDaddy 
- DNS Records : A, AAAA, CNAME, NS, ...
- Zone File: contains DNS records 
- Name Server: resolves DNS queries (Authoritative or Non-Authoritative)
- Top Level Domain (TLD) com, us, in
- Second Level Domain (SLD) : amazon.com

https://api.www.example.com
			SLD. TLD. ROOT
		Sub Domain 
	Domain Name 

**How DNS Works** 


1.Web Browser -> Local DNS Server -> Root Dns Server (ICANN) - TLD - SLD  - DNS 
2.Web Browser <- IP 
3.Web Browser -> IP


---

Amazon Route S3
