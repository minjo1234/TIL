
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
	- You get billed for all the provisioned capacity 
	- You can increase the capacity of the drive over time 


- what is network drive ?


EC2 has multiple EBS Volume, but EBS Volume have only one EC2


## EBS - Delete on Termination attribute 

### Controls the EBS behaviour when an EC2 instance terminates 
- By default, the root EBS volume is delete ( attribute enabled )
- By default, any other attached EBS Volu,e is not deleted (attribute disabled)
### This can be controlled by the AWS console / AWS CLI
### Use case: preserve root volume when instance is terminated 


text means root EBS volume deleted makes attribute enabled 
but why use case preserver root volume ?

