


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

- 