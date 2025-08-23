


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