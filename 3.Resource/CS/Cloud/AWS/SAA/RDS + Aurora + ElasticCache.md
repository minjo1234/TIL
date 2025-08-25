
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
- Replicas can be promoted to the