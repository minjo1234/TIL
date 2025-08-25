
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


