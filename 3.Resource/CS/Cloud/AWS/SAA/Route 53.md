
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

Amazon Route 53

- How you want to route traffic for a domain
- Each Record contains : 
	- Domain/subdomain Name - e.g,example.com
	- RecordType - e,g,.A or AAA 
	- Value - e,g., 123.456.789.123
	- Routing Policy - how route 53 response to queries 
	- TTL 
- Route 53 supports the following DNS Record Types: 
	- (must know) A / AAAA / CNAME / NS 

Record Type

- A - maps a hostname to IPv4
- AAAA - maps a hostname to IPv6
- CNAME - maps a hostname to another hostname 
	- The target is a domain name which must have an A or AAAA record 
	- Can't create a CNAME record for the top node of a DNS namespace (ZONE APEX)
	- Example : you can't create for example.com, but you can create for www.example.com 
- NS - Name Servers for the Hosted Zone 
  
  
Hosted Zones

A container for records that define how to route traffic to a domain and its subdomains 

- Public Hosted Zones - contains records that specify how to route traffic on the internet (public domain names)  - application.mypublicdomain.com
- Private Hosted Zones - contain records that specify how you route traffic within 
  one or more VPCs (private domain names)
  application.company.internal


thin - 4 GB


