
## What's an EBS Volume ?

- An **EBS (Elastic Block Store) Volume** is a **network** drive you can attach to your instances while they run
- It allows your instances to persist data, even after their termination 
- They can only be mounted to one instance at a time (at the CCP level)
- They are bound to a specific availability zone 


- Analogy: Think of them as a "network USB stick"
- Free tier: 30 GB of free EBS storage of type General Purpose (SSD) or Magnetic per month 


## EBS Volume 

- It's a network drive (i.e.not a physical drive)
	- it uses the network to communicate the instance, which means there might be a bit of latency 
	- it can be detached from an EC2 instance and attached to another one quickly 

- It's locked to an Availability Zone (AZ)
	- An EBS Volume in us-east a cannot be attached to us-ease | b 
	- To move a volume across, you first need to snapshot it 

- Have a provisioned capacity (size in GBS, and IOPS)
	- You get billed for all the provi
