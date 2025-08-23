
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