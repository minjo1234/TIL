


---

**AMI** 

- AMI = Amazon Machine Image 
- AMI are a customization of an EC2 instance 
	- You add your own software, configuration, operating system, monitoring 
	- Faster boot / configuration time because all your software is pre-packaged
- AMI are built for a specific region ( and can be copied across regions)
- You can launch EC2 instances from 
	- A Public AMI : AWS provided 
	- Your own AMI : you make and maintain them yourself 
	- An AWS Marketplace AMI : an AMI someone else made (and potentially sells)



```
#!/bin/bash
# Use this your user data (script from top to bottom)
# install httpd (Linux 2 version)
echo "<h1>Hello World from ${hostname -f)</h1>"> /var/www/html/index.html
```

---

**EC2 Instance Store** 

- EBS Volumes are network drives with good but "limited" performance 
- If you need a high-performance hardware disk, EC2 instance Store 

- Better I/O performnce 
- EC2 Instance Store lose their storage if they're. stopped (ephemeral)
- Good for buffer / cache / scratch data / temporary content 
- Risk of data loss if hardware fails 
- Backups and Replication are your responsibility 

---

**EBS Volume Types** 

- EBS Volumes come in 6 types 
- memorize differences 6 types 

----

**EBS Multi-Attach - io l/io2 family** 

- Attach the same EBS volume multiple EC2 instances in the same AZ 
- Each instance has full read & write permissions 
to the high-performance volume 
- Use case: 
	- Achieve higher application availability in clustered Linux Applications 
	- Applications must manage concurrent write operations 
- Up to **16 EC2** Instances at a time 
- Must use a file system that's cluster-aware (not XFS, EX4, etc...)

---

**EBS Encryption** 

- When you create an encrypted EBS volume, you get the following 
	- Data at rest is encrypted inside the volume 
	- All the data in flight moving between the instance and the volume is encrypted 
	- All snapshots are encrypted 
	- All volumes created from the snapshot 
- Encryption and decryption are handled transparently (you have nothing to do)
- Encryption has a minimal impact on latency 
- EBS Encryption leverages keys from KMS (AES-256)
- Copying an unencrypted snapshot allows encryption 
- Snapshots of encrypted volumes are encrypted 

---

**Encryption: encrypt an unencrypted EBS volume** 

- Create an EBS snapshot of the volume 
- Encrypt the EBS snapshot ( using copy )
- Create new ebs volume from the snapshot  ( the volume will also be encrypted )
- Now you can attach the encrypted volume to the original instnace 

---

**Amazon EFS - Elastic File System** 

- Managed NFS (network file system) that can be mounted on many EC2 
- EFS works with EC2 instances in multi-AZ
- Highly available, scalable, expensive (3xgp2), pay per use 

- Use cases: content management, web serving, data sharing, Wordpress 
- Uses NFSv4, I protocol
- Uses security group to control access to EFS 
- **Compatible with Linux bases AMI (not Windows)**

- POSIX file system (~Linux) that has a standard file API 
- File system scales automatically, pay-per-use, no capacity planning 

---

**EFS - Performance & Storage Classes** 

- EFS Scale 
	- 1000s of concurrent NFS clients, 10 GB+ /s throughput 
	- Grow to Petabyte -scale network file system, automatically 
- Performance Mode (set at EFS creation time)
	- General Purpose 
	- Max I/O - higher latency, throughput, highly parallel (big data, media processing)
- Throughput Mode 
	- Bursting 1TB = 
	- Provisioned - set your throughput regardless of storage size 

---

**EFS - Storage Classes** 

- Storage Tiers (lifecycle management feature - move file after N days)
	- Standard: for frequently accessed files 
	- Infrequent access (EFS-IA): cost to retrieve files, lower prvie to store 
	- Archive: rarely accessed data (few times each year), 50% cheaper 
	- Implement lifecycle policies to move files between storage tiers 

- Availability and durability 
	- Standard: Multi-AZ, great for prod 
	- One Zone: One AZ, great for dev, backup enabled by default, compatible