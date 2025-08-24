

### Application Load Balancer (v2)

- Application load balancers is Layer 7 (HTTP)
- Load balancing to multiple HTTP applications across machines (target groups)
- Load balancing to multiple applications on the same machine (ex: containers)
- Support for HTTP/2 and WebSocket 
- Support redirects (from HTTP to HTTPS for example)


- Routing tables to different target groups 
	- Routing based on path in URL 
	- Routing based on hostname in URL
	- Routing based on Query String, Headers 

- ALB are a great fit for micro services & container-based application 
- Has a port mapping feature to redirect to a dynamic port in ECS
- In comparison, we'd need multiple Classic Load Balancer per application 


**Target Groups** 

- EC2 instances (can be managed by an Auto Scaling Group) - HTTP 
- ECS tasks 
- Lambda functions 
- IP Addresses - must be private IPs 

- ALB can route to multiple target groups 
- Health checks are at the target group level 

- Fixed hostname (XXX.region.elb.amazonaws.com)
- The application servers don't see the IP of the client directly 
	- The true IP of the client is inserted in the header X-Forwarded-For 
- We can also get Port and proto 


```
#!/bin/bash
# Use this for your user data (script from top to bottom)
# install httpd (Linux 2 version)
yum update -y 
yum install -y httpd
systemctl start httpd
systemctl enable httpd
echo "<h1>Hello World from $(hostname -f)</h1>" > /var/www/html/index.html
```


---

### Network Load Balancer (v2)

- Network load balancers (Layer 4) allow to :
	- Forward TCP & UDP traffic to your instances 
	- Handle millions of request per seconds 
	- Ultra-low latency 

- NLB has one static IP per AZ, and supports assigning Elastic IP (helpful for whitelisting specific IP)


**Target Groups**
- EC2 instances 
- IP Addresses - must be private IPS 
- Application Load Balancer 