
- RDS stands for Relational Database Service
- Aurora (AWS Proprietary database)
  
**RDS is a managed service:** 
- Automated provisioning, OS patching 
- Continuous backups, and restore to specific timestamp (Point in time Restore)
- Monitoring dashboards 
- Read replicas for improved read performance 
- Multi AZ setup for DR (Disaster Recovery)
- Maintenance windows for upgrades
- Scaling capacity (vertical and horizontal)
- Storage backed by EBS 
But you can't SSH into your instances 

---

**RDS - Storage Auto Scaling** 

- when RDS detects you are running out of free database storage, it scales automatically 

**RDS Read Replicas for read scalability** 

- Up to 15 Read Replicas 
- Within AZ, Cross AZ or Cross Region 
- Replicas can be promoted to their own DB
- Replication is ASYNC, so read are eventually consistent 

**RDS Read Replicas - Network Cost** 

- In AWS there's network cost when data from one AZ to another 
- **For RDS Read Replicas within the same region, you don't pay that fee**

Same Region, Different AZ 

**RDS Multi AZ (Disaster Recovery)**

- SYNC replication 
- One DNS name 
- Increase availability 

**RDS - From Single-AZ to Multi AZ** 

- Zero downtime operation
- Just click on "modify" for the database 
- The following happens internally 
	- A snapshot is taken 
	- A new DB is restored from the snapshot in a new AZ
	- Synchronization is established between the two database 
 

**RDS Custom**

- RDS : entire database and the OS to be managed by AWS 
- RDS Custom: full admin access to the underlying OS and the database (Oracle, Microsoft SQL)

---

**Amazon Aurora** 

- Aurora is a proprietary technology from AWS (not open sourced)

Aurora High Availability and Read Scaling 
- 6 copies of your data access 3 AZ :
	- 4 copies out of 6