## my plane :
- [ ] study AWS solution architect
- [ ] deploy mono-repo react application
- [ ] deploy mico-frontend reactjs

# hands-on course 
- https://www.udemy.com/course/aws-certified-solutions-architect-associate-saa-c03/?kw=aws+sol&src=sac&couponCode=2021PM25
- https://explore.skillbuilder.aws/learn/learning_plan/view/1046/solutions-architect-learning-plan-includes-labs
- https://aws.amazon.com/training/learn-about/architect/
- [this is my archeticture](https://aws.amazon.com/architecture/this-is-my-architecture/?tma.sort-by=item.additionalFields.airDate&tma.sort-order=desc&awsf.category=*all&awsf.industry=*all&awsf.language=*all&awsf.show=*all&awsf.product=*all)
- https://aws.amazon.com/education/awseducate/
- https://aws.amazon.com/training/digital/aws-simulearn/

# notes 
- [set of articles](https://chloemcateer.medium.com/aws-solution-architect-associate-exam-study-notes-b6c5884ee500)
- notes for each part of the course https://github.com/Ernyoke/certified-aws-solutions-architect-associate
- https://github.com/saumyap24/aws-solutions-architect-associate-notes?tab=readme-ov-file


# Guid 
- https://rxhl.notion.site/AWS-Solution-Architect-Associate-698442acf94a484caa56477344dafc9d
- https://tutorialsdojo.com/aws-certified-solutions-architect-associate-saa-c03/
- https://aws.amazon.com/training/ramp-up-guides/

# practise exam questions
- https://www.youtube.com/watch?v=Wee_F8_k8s4
- https://github.com/Ditectrev/AWS-Certified-Solutions-Architect-Associate-SAA-C03-Practice-Tests-Exams-Questions-Answers?tab=readme-ov-file#which-set-of-amazon-s3-features-helps-to-prevent-and-recover-from-accidental-data-loss
- https://skillbuilder.aws/search?searchText=exam+prep+solutions+architect&page=1
- ..... search for another courses , video


# Learn by gaming
- https://aws.amazon.com/training/digital/aws-cloud-quest/
- https://explore.skillbuilder.aws/learn/learning_plan/view/1046/solutions-architect-learning-plan-includes-labs

# My-notes 

-> IAM service
==================
![Logo](https://raw.githubusercontent.com/FoushWare/aws-bookmark/master/1_nQuYpC8oelxaqke2VXPw2w.webp?token=GHSAT0AAAAAACUSL73VFTRFIOX7JZNDYHGSZVUVAMA)

### key features to IAM 
 - global not depend on regions
 - user can created and have least permissions and get permissions as needed
 - using roles to grant access is more secure than sharing access keys and secret keys
 - can manage many accounts through I AM Center or other providers based on SAML
 - allow you to set up custom password policy

### IAM Terminology 
- users -> individual users i.e employees
- Groups -> collection of users that have shared permissions
- Roles -> allow one service to access another service
- ARN   -> Amazone resource name , unique identifies any resource in AWS 
- Root Account -> is the main account you signed up with you should put MFA to protect it 
- Power user access -> access all the aws services except  manageing groups and users within IAM
- Billing Alerts -> seting i.e(10$) as your budget and when it exceeds that threshold you will get alert 
- AWS Budgets -> ....
- AWS Resource Access ManageMent (RAM): allow sharing resources between accounts
- AWS SSO (Single Sign On) -> using third party to manage all the accounts or the organizations

### IAM Policy
- set of deny and allow statements
- if the resource has multiple polices AWS joins them
- anything that is not explicity allowed it's implicity denied

### Permission Boundaries
- used to delegate administrations to other users
- used to prevent privilege scalation

## AWS Organizations
- managment service that allows you to manage multiple accounts in your organization in a central place this allow you to handle the billing in one place and get price discount

----------------------------------------------------------------------------------------

EC2 
![Logo](https://raw.githubusercontent.com/FoushWare/aws-bookmark/master/1_joI3hN7W6ZtT-xda7Mp8Bw.webp?token=GHSAT0AAAAAACUSL73UEN5C4I3K675JJSZAZVUU7TA)

====================
- gives you full control of computing resources like [storage,processor,Network, Operating systems]
- increase/decrease capacity in minutes
- the root volume is virtual so it's used for the OS
- we can add EBS volumes ant it is deleted after terminate the instance
- There is a script that can run after boot up it's called userData
- you need to create a key pair [public,private] to access it

- It mainly consists of the following capabilities:
    - Renting virtual machines in the cloud (EC2)
    - Storing data on virtual drives (EBS)
    - Distributing load across multiple machines (ELB)
    - Scaling the services using an auto-scaling group (ASG)


EC2 Pricing
============
1- on-Demand:
fixed rate for compute capacity per hour OR per second with no commitment or up front const . Typically used for short term 

2- reserved:

you have capacity reservation so you have discount compared to on-demond but it requires to have contract 1-3 years -- used for applications which have steady predictable use.However, you can't move between regions 

Types of Reserved Pricing :

- standard: discount of 75%
- convertible: discount 54% change between instances types
- scheduled reserved instances: can launch within time window



3- Spot : when aws has excess capicity it make discount reach 90% but they can take the capicity back -- don't use spot with critical apps that needs to be online all the time 
4- Dedicated Hosts: EC2 dedicated for specific you like oracle 

** spot fleets
- collection of spot instances and optionally on-demand instances .attempt to launch bunch of them to meet a certain capicity
- allocation based on spot fleet request

## spot fleet strategies 
- lowest Price => choose the fleet pool with lowest price.
- Diversified  =>  distributed across all pools.
- Capacity Optimised => choose from pools with optimal capacity

instancePoolsToUseCount=> Distributed across the number of pools you specify __only can be used at lowest price option

## Security Groups
![security group](https://github.com/FoushWare/aws-bookmark/blob/622a37a113c6193f8f21b07097ab1e9b0eb937d9/ec2-security-groups.png)
- virtual firewall for Ec2 instances
- all inbound traffic are blocked by default but all outbound traffic is allowed
- you add rules to security groups to allow traffic in.
- security groups are permitive this means you only use it to allow not to prevent or deny
- you can have more than security groups attached to EC2 instance

- Security Groups are the fundamental of networking security in AWS
- They control how traffic is allowed into or out of EC2 machines
- Basically they are firewalls

## Security Groups Deep Dive

- Security groups regulate:
    - Access to ports
    - Authorized IP ranges - IPv4 and IPv6
    - Control of inbound and outbound network traffic
- Security groups can be attached to multiple instances
- They are locked down to a region/VPC combination
- They do live outside of the EC2 instances - if traffic is blocked the EC2 instance wont be able to see it
- *It is good to maintain one separate security group for SSH access*
- If the request for the application times out, it is most likely a security group issue
- If for the request the response is a "connection refused" error, then it means that it is an application error and the traffic went through the security group
- By default all inbound traffic is **blocked** and all outbound traffic is **authorized**
- A security group can allow traffic from another security group. A security group can reference another security group, meaning that it is no need to reference the IP of the instance to which the security group is attached

 ## Elastic IP

- When an EC2 instance is stopped and restarted, it may change its public IP address
- In case there is a need for a fixed IP for the instance, Elastic IP is the solution
- An Elastic IP is a public IP the user owns as long as the IP is not deleted by the owner
- With Elastic IP address, we can mask the failure of an instance by  rapidly remapping the address to another instance 
- AWS provides a limited number of 5 Elastic IPs (soft limit)
- Overall it is recommended to avoid using Elastic IP, because:
    - They often reflect pool arhcitectural decisions
    - Instead, us e a random public IP and register a DNS name to it

  ## EC2 User Data

- It is possible to bootstrap (run commands for setup) an EC2 instance using EC2 User data script
- The user data script is only run once at the first start of the instance
- EC2 user data is used to automate boot tasks such as:
    - Installing update
    - Installing software
    - Downloading common files from the internet
    - Any other start-up task
- THe EC2 user data scripts run with root user privileges

  ## EC2 Instance Launch Types

- On Demand Instances: short workload, predictable pricing
- Reserved: known amount of time (minimum 1 year). Types of reserved instances:
    - Reserved Instances: recommended long workloads
    - Convertible Reserved Instances: recommended for long workloads with flexible instance types
    - Scheduled Reserved Instances: instances reserved for a longer period used at a certain schedule 
- Spot Instances: for short workloads, they are cheap, but there is a risk of losing the instance while running
- Dedicated Instances: no other customer will share the underlying hardware
- Dedicated Hosts: book an entire physical server, can control the placement of the instance

### EC2 On Demand

- Pay for what we use, billing is done per second after the first minute
- Hast the higher cost but it does not require upfront payment
- Recommended for short-term and uninterrupted workloads, when we can't predict how the application will behave

### EC2 Reserved Instances

- Up to 75% discount compared to On-demand
- Pay upfront for a given time, implies long term commitment
- Reserved period can be 1 or 3 years
- We can reserve a specific instance type
- Recommended for steady state usage applications (example: database)
- **Convertible Reserved Instances**:
    - The instance type can be changed
    - Up to 54% discount
- **Scheduled Reserved Instances**:
    - The instance can be launched within a time window
    - It is recommended when is required for an instance to run at certain times of the day/week/month

### EC2 Spot Instances

- We can get up to 90% discount compared to on-demand instances
- It is recommended for workloads which are resilient to failure since the instance can be stopped by the AWS if our max price is less then the current spot price
- Not recommended for critical jobs or databases
- Great combination: reserved instances for baseline performance + on-demand and spot instances for peak times

### EC2 Dedicated Hosts

- Physical dedicated EC2 server
- Provides full control of the EC2 instance placement
- It provides visibility to the underlying sockets/physical cores of the hardware
- It requires a 3 year period reservation
- Useful for software that have complicated licensing models or for companies that have strong regulatory compliance needs

### EC2 Dedicated Instances

- Instances running on hardware that is dedicated to a single account
- Instances may share hardware with other instances from the same account
- No control over instance placement
- Gives per instance billing

## EC2 Spot Instances - Deep Dive

- With a spot instance we can get a discount up to 90%
- We define a max spot price and get the instance if the current spot price < max spot price
- The hourly spot price varies based on offer and capacity
- If the current spot price goes over the selected max spot price we can choose to stop or terminate the instance within the next 2 minutes
- Spot Block: block a spot instance during a specified time frame (1 to 6 hours) without interruptions. In rare situations an instance may be reclaimed
- Spot request - with a spot request we define:
    - Maximum price
    - Desired number of instances
    - Launch specifications
    - Request type:
        - One time request: as soon as the spot request is fulfilled the instances will be launched an the request will go away
        - Persistence request: we want the desired number of instances to be valid as long as the spot request is active. In case the spot instances are reclaimed, the spot request will try to restart the instances as soon as the price goes down
- Cancel a spot instance: we can cancel spot instance requests if it is in open, active or disabled state (not failed, canceled, closed)
- Canceling a spot request does not terminate the launched instances. If we want to terminate a spot instance for good, first we have to cancel the spot request and the we can terminate the associated instances, otherwise the spot request may relaunch them

### Spot Fleet

- Spot Fleet is a set of spot instances and optional on-demand instances
- The spot fleet will try to meet the target capacity with price constraints
- AWS will launch instances from a launch pool, meaning we have to define the instance type, OS, AZ for a launch pool
- We can have multiple launch pools from within the best one is chosen
- If a spot a fleet reaches capacity or max cost, no more new instances are launched
- Strategies to allocate spot instances in a spot fleet:
    - **lowerPrice**: the instances will be launched from the pool with the lowest price
    - **diversified**: launched instances will be distributed from all the defined pools
    - **capacityOptimized**: launch with the optimal capacity based on the number of instances

## EC2 Instance Types

- R: applications that needs a lot of RAM - in-memory cache
- C: applications that need good CPU -  compute/database
- M: applications that are balanced - general / web app
- I: applications that need good local I/O - databases
- G: applications that need GPU - video rendering / ML
- T2/T3 - burstable instances
- T2/T3 unlimited: unlimited burst


## AMI

- AWS comes with lots of base images
- Images can be customized ar runtime with EC2 User data
- In case of more granular customization AWS allows creating own images - this is called an AMI
- Advantages of a custom AMI:
    - Pre-install packages
    - Faster boot time (on need for the instance to execute the scripts from the user data)
    - Machine configured with monitoring/enterprise software
    - Security concerns - control over the machines in the network
    - Control over maintenance
    - Active Directory out of the box
- An AMI is built for a specific region (NOT GLOBAL!)

### Public AMI

- We can leverage AMIs from other people
- We can also pay for other people's AMI by the hour, basically renting the AMI form the AWS Marketplace
- Warning: do not use AMI which is not trustworthy!

### AMI Storage

- An AMI takes space and they are stored in S3
- AMIs by default are private and locker for account/region
- We can make our AMIs public and share them with other people or sell them on the Marketplace

### Cross Account AMI Sharing

- It is possible the share AMI with another AWS account
- Sharing an AMI does not affect the ownership of the AMI
- If a shared AMI is copied, than the account who did the copy becomes the owner
- To copy an AMI that was shared from another account, the owner of the source AMI must grant read permissions for the storage that backs the AMI, either the associated EBS snapshot or an associated S3 bucket
- Limits:
    - An encrypted AMI can not be copied. Instead, if the underlying snapshot and encryption key where shared, we can copy the snapshot while re-encrypting it with a key of our own. The copied snapshot can be registered as a new AMI
    - We cant copy an AMI with an associated **billingProduct** code that was shared with us from another account. This includes Windows AMIs and AMIs from the AWS Marketplace. To copy a shared AMI with **billingProduct** code, we have to launch an EC2 instance from our account using the shared AMI and then create an AMI from source

## Placement Groups

- Sometimes we want to control how the EC2 instances are placed in the AWS infrastructure
- When we create a placement group, we can specify one of the following placement strategies:
    - **Cluster** - cluster instances into a low-latency group in a single AZ
    - **Spread** - spread instances across underlying hardware (max 7 instances per group per AZ)
    - **Partition** - spread instances across many different partitions (which rely on different sets of racks) within an AZ. Scale to 100s of EC2 instances per group (Hadoop, Cassandra, Kafka)

![clustered](https://github.com/FoushWare/aws-bookmark/blob/0d45f198333c6c3e3f34cd119a2e6fd834ed1c74/Capture.PNG)
![spread](https://github.com/FoushWare/aws-bookmark/blob/0d45f198333c6c3e3f34cd119a2e6fd834ed1c74/Capture2.PNG)
![partioned](https://github.com/FoushWare/aws-bookmark/blob/0d45f198333c6c3e3f34cd119a2e6fd834ed1c74/Capture3.PNG)
### Placement Groups - Cluster

- Pros: Great network (10Gbps bandwidth between instances)
- Cons: if the rack fails, all instances fail at the time
- Use cases:
    - Big data job that needs to complete fast
    - Application that needs extremely low latency and high network throughput

### Placement Groups - Spread

- Pros:
    - Can span across multiple AZs
    - Reduces risk for simultaneous failure
    - EC2 instances are on different hardware
- Cons:
    - Limited to 7 instances per AZ per placement group
- Use case:
    - Application that needs to maximize high availability
    - Critical applications where each instance must be isolated from failure

### Placement Groups - Partitions

- Pros:
    - Up to 7 partitions per AZ
    - Can have hundreds of EC2 instances per AZ
    - The instances in a partition do not share racks with the instances from other partitions
    - A partition failure can effect many instances but they wont affect other partitions
    - Instances get access to the partition information as metadata
- Use cases: HDFS, HBase, Cassandra, Kafka

## Elastic Network Interfaces - ENI

- Logical component in a VPC that represents a virtual network card
- An ENI can have the following attributes:
    - Primary private IPv4 address, one or more secondary IPv4 addresses
    - One Elastic IP (IPv4) per private IPv4
    - One Public IPv4
- ENI instances can be created independently from an EC2 instance
- We can attach them on the fly to an EC2 instances or move them from one to another (useful for failover)
- ENIs are bound to a specific available zone
- ENIs can have security group attached to them
- EC2 instances usually have a primary ENI (eth0). In case we attach a secondary ENI, eth1 interface will be available. The primary ENI can not be detached.

## EC2 Hibernate

- We can stop or terminate EC2 instances:
    - If an instance is stopped: the data on the disk (EBS) is kept intact
    - If an instance is terminated: any root EBS volume will also gets destroyed
- On start, the following happens in case of an EC2 instance:
    - Fist start: the OS boots and EC2 User data script is executed
    - Following starts: the OS boots
    - After the OS boot the applications start, cache gets warmed up, etc. which may take some time
- EC2 Hibernate:
    - All the data from RAM is preserved on shut-down
    - The instance boot is faster
    - Under the hood: the RAM state is written to a file in the root EBS volume
    - The root EBS volume must be encrypted
- Supported instance types for hibernate: C3, C4, C5, M3, M4, M5, R3, R4, R5
- Supported OS types: Amazon Linux 1 and 2, Windows
- Instance RAM size: must be less then 150 GB
- Bare metal instances do not support hibernate
- Root volume: must be EBS, encrypted, not instance store. And it must be large enough
- Hibernate is available for on-demand and reserved instances
- An instance can not hibernate for more than 60 days

## EC2 for Solution Architects

- EC2 instances are billed by the second, t2.micro is free tier
- On Linux/Mac we can use SSH, on Windows Putty or SSH
- SSH is using port 22, the security group must allow our IP to be able to connect
- In cas of a timeout, it is most likely a security group issue
- Permission for SSH key => chmod 0400
- Security groups can reference other security groups instead of IP addresses
- EC2 instance can be customized at boot using EC2 User Data
- 4 EC2 launch modes:
    - On-demand
    - Reserved
    - Spot
    - Dedicated hosts
- We can create AMIs to pre-install software
- An AMI can be copied through accounts and regions
- EC2 instances can be started in placement groups:
    - Cluster
    - Spread
    - Partition










