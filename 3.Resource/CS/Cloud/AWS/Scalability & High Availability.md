
- Scalability means that an application / system can handle greater loads by adapting.
- There are two kinds of scalability 
	- Vertical Scalability 
	- Horizontal Scalability (= elasticity)
- Scalability is linked but different to High Availability 

- Let's deep dive into the distinction, using a call center as an example 

### Vertical Scalability 

- Vertically scalability means increasing the size of the instance 
- For example, your application runs on a t2.micro
- Scaling that application vertically means running it on a t2.large 
- Vertical scalability is very common for non distributed systems, such as a database 
- RDS, ElastiCache are services that can scale vertically 
- There's usually a limit to how much you can vertically scale (hardware limit)

### Horizontal Scalability 

- Horizontal Scalability means increasing the number of instances / systems for your application
  
-  Horizontal scaling implies distributed systems. 

- This is very common for web applications / modern applications 

- It's easy to horizontally scale thanks the cloud 
offerings such as Amazon EC2

---

### High Availability 

- High Availability usually goes hand in hand with horizontal scaling 
- High availability means running your application / 
system in at least 2 data centers ( == Availability Zones)
- The goal of high availability is to survive a data center loss 

- The high availability can be passive 
- The high availability can be active 


- **Vertical Scaling**: Increase instance size ( = scale up / down)
	- From: t2.nano - 0.5G of RAM, I vCPU 
	- To: u-l 2tbl.metal - I 2.3TB of RAM, 448 vCPUs 

- **Horizontal Scaling**: Increase number of instances ( = scale out / in a)
	- Auto Scaling Group 
	- Load Balancer 

- **High Availability**: Run instances for the same application across multi AZ 
	- Auto Scaling Group multi AZ
	- Load Balancer multi AZ 

---

### What is load balancing ? 

- Load Balances are servers that forward traffic to multiple servers (e.g., EC2 instances) downstream 
- Spread load across multiple downstream instances 
- Expose a single point of access (DNS) to your application 
- Seamlessly handle failures of downstream instances 
- Do regular health checks to your instances 
- Provide SSL termination (HTTPS) for your websites 
- Enforce stickiness with cookies 
- High availability across zones 
- Separate public traffic from private traffic  


### Why use an Elastic Load Balancer 

- An Elastic Load Balancer is a managed load balancer 
	- AWS guarantees that it will be working 
	- AWS takes care of upgrades, maintenance, high availability 
	- AWS provides only a few configuration knobs 

- It costs less to setup your own load balancer but it will be a lot more effort on your end 

- It is integrated with many AWS offerings / services 
	- EC2, EC2 Auto Scaling Groups, Amazon ECS
	- AWS Certificate Manager (ACM), CloudWatch 
	- R