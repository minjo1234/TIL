 Elastic Block Store 


- They are bound to a specific availability zone 
(Inner AZ , not other AZ )



**network drive (not a physical drive)**
- detach from an EC2 instance and attached to another and quickly

**locked to an availability zone (AZ)**
- An EBS Volume in us-east-la cannot be attached to us-east-lb

Have a provisioned capacity (size in GBS, and IOPS)


---

**EBS - Delete on Termination attribute**  

- Controls the EBS behavior when an EC2 instance terminates 
	- By default, the root EBS volume is deleted (attribute enabled)
	- By default, any other attached EBS volume is not deleted (attribute disabled)

- This can be controlled by the AWS console / AWS CLI
- Use case: preserve root volume when instance is terminated 

---

**EBS Snapshots**

- Mek