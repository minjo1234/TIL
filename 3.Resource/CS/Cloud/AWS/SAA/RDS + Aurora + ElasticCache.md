
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
	- 4 copies out of 6 needed for writes 
	- 3 copies out of 6 need for reads 
	- Self healing with peer-to-peer replication 
	- Storage is stripped across 100s of volumes 
- One Aurora Instance takes writes (master)
- Automated failover for master in less than 30 seconds 
- Master + up. to 15 Aurora Read Replicas serve reads 
- Support for Cross Region Replication 

Aurora DB Cluster 

- Writer endpoint 
- Reader endpoint 

---

**Aurora Replicas - Auto Scaling** 

Writer Endpoint , Read Endpoint 
					- Replicas Auto Scaling 

Aurora - Custom Endpoints 

**Aurora - Custom Endpoints** 

Define a subset of Aurora Instances as a Custom Endpoint 
The Reader Endpoint is generally not used after defining Custom Endpoints 

**Aurora Serverless** 

 Good for infrequent intermittent or unpredictable workload 

**Global Aurora** 

Aurora Cross Region Read Replicas 

Aurora Global Database 
- **Typical cross-region replication takes less than 1 second** 

**Aurora Machine Learning** 

- Supported services 
	- Amazon SageMaker 
	- Amazon Comprehend 
---

**RDS Backupds** 

- Automated backups 
	- Daily full backup of the database 
	- Transaction logs are backed-up by RDS every 5 minutes 
- Manual DB Snapshots 


**Trick: in a stopped RDS database, you will still pay for storage, If you plan to stopping it for a long time, you should snapshot & restore instead** 


---

**Aurora Backups** 

Automated backups 
- 1 to 35 days (cannot be disabled)
- point-in-time recovery in that timeframe 

Manual DB Snapshots 
- Manually triggered by the user 
- Retention of backup for as long as you want 

RDS & Aurora Restore options 

Restoring a RDS / Aurora backup or a snapshot creates a new database

Restoring MySQL RDS database from S3
- Create a backup of your on-premiss database 
- Store it on Amazon S3 (object Storage)

Restoring MySQL Aurora cluster from S3