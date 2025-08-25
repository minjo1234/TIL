
- On demand : coming and staying in resort 
- Reserved : like planning ahead and if we plan to stay for a long time, we may get a good discount 
- Saving Plans: pay a certain amount per hour for certain period and stay in any room type 
- Spot instances : the hotel allows people to bid for
the empty rooms and the highest bidder keeps the rooms. You can get kicked out at any time 
- Dedicated Hosts
- Capacity Reservations 


---

### Placement Groups 

Cons:
- Limited to 7 instances per AZ per placement group 

---
### ENI(Elastic Network Interfaces)

assistance private ip 


---

### EC2 Hibernate 


- Stop  : the data on disk (EBS) is kept intact in the next start 
- Terminated : any EBS volumes (root) also set-up to be destroyed is lost 

- Hibernate 
	- the instance boot is much faster 

Use-cases 
- Long-running processing 
- Saving the RAM state 
- Services that take time to initialize 

---
### Question 

EC2 fixed IP  - Use Elastic IP 

Cluster Batch Group - When user wants EC2 instances connect each other and have the highest level performance 

Distributed batch group - maximum availability 

ENI - Connect Inner AZ o, Other AZ not connect 

EC2 Hibernate Mode - 
- Instance Root Volume Must have to EBS Volume 
- On Demand and apply reservation instnace 
- RAM under 150 GB
- 



 
