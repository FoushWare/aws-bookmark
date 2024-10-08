

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

============Load Balancer ======
![load balancer](https://github.com/FoushWare/aws-bookmark/blob/86ba8fa08c65aa2fbd5fd56ed28b349c36409759/1_qclNeMJFxowiCKouU4Dkag.webp)
# Elastic Load Balancers

## Scalability and High Availability

- Scalability means that an a system can handle greater loads by adapting
- We can distinguish two types of scalability strategies:
    - **Vertical Scalability** (scale up/down)
        - Increase the size of the current instance (ex. from a t2.micro instance migrate to a a t2.large one)
        - Vertical scalability is common for non distributed systems, such as databases
        - RDS, ElastiCache are services that can scale vertically
    - **Horizontal Scalability** (scale out/in)
        - Increase the number of instances on which the application runs
        - Horizontal scaling implies having a distributed system
        - It's easy to scale horizontally thanks to could offerings such as EC2
- High Availability means running our application in at least 2 data centers (AZs)
    - The goal of high availability is to survive a data center loss
- High Availability can be:
    - Passive
    - Active
- Load balancers can scale but not instantaneously - contact AWS for a "warm-up"
- Troubleshooting:
    - 4xx errors are client induced errors
    - 5xx errors are application induced errors (server side errors)
    - Error 503 means that the load balancer is at capacity or no registered targets can be found
    - If the load balancer can't connect to the application, it most likely means that the security group blocks the connection
- Monitoring:
    - ELB access logs will log all the access requests to the LB
    - CloudWatch Metrics will give aggregate statistics (example: connections counts)

## Load Balancing Basics

- Load balancers are servers that forward internet traffic to multiple other servers (most likely EC2 instances)
- Why use load balances?
    - Spear load across multiple downstream instances
    - Expose a single point of access (DNS) to the application
    - Seamlessly handle failures of downstream instances (by using health checks)
    - Do regular health checks to registered instances
    - Provide SSL termination (HTTPS) for the website hosted on the downstream instances
    - Enforce stickiness for cookies
    - High availability across availability zones (load balancer can be spread across multiple AZs, not regions!!!)
    - Cleanly separate public traffic from private traffic
- An ELB (Elastic Load Balancer) is a **managed load balancer** which means:
    - AWS guarantees that it will be working
    - AWS takes care of upgrades, maintenance and high availability
    - An ELB provides a few configuration options for us also
    - It costs less to setup our custom load balancer, but it will be a lot more effort to maintain on the long run
    - An ELB is integrated with many AWS offering/services, it will be more flexible than a custom LB

## Health Checks

- They enable for a LB to know if an instance for which traffic is forwarded is available to reply to requests
- The health checks is done using a port and a route (usually /health)
- If the response is not 200, then the instance is considered unhealthy

## Types of Load Balancers on AWS

- AWS provides 4 type of load balancers:
    - Classic Load Balancer (v1 - old generation): supports HTTP, HTTPS and TCP
    - Application Load Balancer (v2 - new generation): supports HTTP, HTTPS and WebSockets
    - Network Load Balancer (v2 - new generation): supports TCP, TLS (secure TCP) and UDP
    - Gateway Load Balancer (new generation - see VPC section of the notes)
- It is recommended to use the new versions
- We can setup **internal** (private) and **external** (public) load balancers on AWS

### Classic Load Balancers (CLB)

- They support 2 types of connections: TCP (layer 4) and HTTP(S) (layer 7)
- Health checks are either TCP or HTTP based
- CLBs provide a fixed hostname: XXX.region.elb.amazonaws.com

### Application Load Balancers (ALB)

- They are a layer 7 type load balancers (only HTTP or HTTPS)
- They allow load balancing to multiple HTTP applications across multiple machines (target groups). Also they allow to load balance to multiple applications on the same EC2 instance (useful in case of containers)
- They have support for HTTP2 and WebSockets.
- They support redirects, example for HTTP to HTTPS
- They provide routing tables to different target groups:
    - Routing based on path in URL
    - Routing based on the hostname
    - Routing based on query strings an headers
- ALBs are great fit for micros-services and container based applications
- ALBs have port mapping features to redirect to dynamic ports in case ECS
- Target groups can contain:
    - EC2 instances (can be managed by an Auto Scaling Group)
    - ECS tasks (managed by ECS itself)
    - Lambda Functions -  HTTP request is translated to a JSON event
    - IP Addresses - must be private IP addresses
- ALBs also provide a fixed hostname (same as CLBs): XXX.region.elb.amazonaws.com
- The application servers behind the LB can not see the IP of the client who accessing them directly, but they can retrieve for **X-Forwarded-For** header. The port can be fetched from **X-Forwarded-Port** and the protocol from **X-Forwarded-Proto**

### Network Load Balancers (NLB)

- Network load balancers (layer 4) allow to:
    - Forward TCP and UDP traffic to the registered instances
    - Handle millions of requests per second
    - Less latency ~100ms (vs 400ms for ALB)
- NLBs have **one static IP per AZ** and supports Elastic IPs (can be used when whitelisting is necessary)
- Use case for NLBs: NLBs are used for extreme performance in case of TCP or UDP traffic (example: video games)
- Instances behind an NLB don't see traffic coming from the load balancer, they see traffic as it was coming from the outside world => no security group is attached to LB => security group attached to the target EC2 instance should be changed to allow traffic from the outside (example: 0.0.0.0/0, on port 80)

## Stickiness

- It is possible to implement stickiness in case of CLB and ALB load balancers
- Stickiness means that the traffic from the same client will be forwarded to the same target instance
- Stickiness works by adding a cookie to the request which has an expiration date for controlling the
stickiness period
- Possible use case for stickiness: we have to make sure that the user does not lose his session data
- Enabling stickiness may bring imbalance to the load over the downstream target instances

## Cross-Zone Load Balancing

- With Cross-Zone Load Balancing enabled each LB instance distributes traffic evenly across multiple AZs
- Otherwise, ech LB node distributes requests evenly only in the AZ where it is registered
- Classic Load Balancer: 
    - Cross-zone load balancing is disabled by default
    - No additional charges for cross zone load balancing if the feature is enabled
- Application Load Balancer: 
    - Cross-zone load balancing is always on, can not be disabled
    - No charges applied for cross zone load balancing
- Network Load Balancer:
    - Cross-zone load balancing is disabled by default
    - Additional charges apply if the feature is enabled

## SSL/TLS Certificates

- An SSL certificate allows traffic to be encrypted between the clients and the load balancers. This ia called encryption in transit or in-flight encryption
- SSL - Secure Socket Layer
- TLS (newer version of SSL) - Transport Layer Security
- Nowadays TLS are mainly used, but we are still referring to it as SSL
- Public SSL certificates are issued by a Certificate Authority
- SSL certificates have an expiration dates and they must be renewed
- SSL termination: client can talk with a LB using HTTPS but internal traffic can be routed to a target using HTTP
- Load balancer can load an X.509 certificate (which is a SSL/TLS server certificate)
- We can manage certificates in AWS using ACM (AWS Certificate Manager)
- HTTPS Listener:
    - We must specify a default certificate
    - We can add an optional list of certificates to support multiple domains
    - Clients can use SNI (Server Name Indication) to specify which hostname want to reach
    - Ability to specify a security policy to support older versions of SSL/TLS (for legacy clients like Internet Explorer 5 lol:) )

### SNI - Server Name Indication

- SNI solves the problem of being able to load multiple SSL certificates onto one web server
- There is a newer protocol which requires the client to indicate the hostname of the target server in the initial SSL handshake
    - In case of AWS this only works for ALB, NLB and CloudFront (no CLB!)

## ELB - Connection Draining

- Feature naming:
    - In case of a CLB is called Connections Draining
    - If we have a target group: (ALB, NLB) it is called Deregistration Delay
- Connection draining is the time to complete in-flight requests while the instance is de-registering or unhealthy. Basically it allows the instance to terminate whatever it was doing
- The LB will stop sending new requests to the target instance which is in progress of de-registering
- The time period of the connection draining can be set between 1 seconds to 3600 seconds
- It also can be disabled (set the period to 0 seconds)


# Load balancers and ASG
# Auto Scaling Groups

- Applications may encounter different amount of load depending on their usage span
- In cloud we can create and get rid of resources (servers) quickly
- The goal of an Auto Scaling Group (ASG) is to:
    - Scale out (add more EC2 instances) to match the increased load
    - Scale in (remote EC2 instances) to match a decreased load
    - Ensure we have a minimum and a maximum number of machines running
    - Automatically register new instances to a load balancer

## ASG Attributes

- Launch configuration - consists of:
    - AMI + Instance Type
    - EC2 User Data
    - EBS Volumes
    - Security Groups
    - SSH Key Pair
- Min size, max size, initial capacity
- Network + subnets information
- Load balancer information
- Scaling policies - what will trigger a scale out/scale in

## Auto Scaling Alarms

- It is possible to scale an ASG based on CloudWatch alarms
- An alarm monitors a metric (such as Average CPU)
- **Metrics are computed for the overall ASG instances**
- Based on alarms we can create:
    - Scale-out policies
    - Scale-in policies

## Auto Scaling New Rules

- It is possible to define "better" auto scaling rules managed directly by EC2 instances, for example:
    - Target Average CPU Usage
    - Number of requests on teh ELB per instance
    - Average Network In/Out
- These rules are easier to set up and to reason about then the previous ones

## Auto Scaling Based on Custom Metrics

- We can scale based on a custom metric (ex: number of connected users to the application)
- In order to do this we have to:
    1. Send a custom metric request to CloudWatch (PutMetric API)
    2. Create a CloudWatch alarm to react to values of the metric
    3. Use the CloudWatch alarm as a scaling policy for ASG

## ASG Summary

- Scaling policies can be on CPU, Network, etc. and can even be based on custom metrics or based on a schedule
- ASGs can use launch configurations or launch templates (newer version)
    - Launch configurations allow to specify one instance type
    - Launch templates allow to use a spot fleet of instances
- To update an ASG, we must provide a new launch configuration/template. The underlying EC2 instances will be replaced over time
- IAM roles attached to an ASG will be assigned to the launched EC2 instances
- ASGs are free. We pay for the underlying resources being launched (EC2 instances, attached EBS volumes, etc.)
- Having instances under an ASG means that if they get terminated for any reason, the ASG will automatically create new ones as a replacement
- ASG can terminate instances marked as unhealthy by a load balancer and obviously replace them
- Health checks - we can have 2 types of health checks:
    - EC2 health checks - instances is recreated if the EC2 instance fails to respond to health checks
    - ELB health checks - instance is recreated if the ELB health checks fail, meaning that the application is down for whatever reason

## ASG Scaling Policies

- **Target Tracking Scaling**
    - Most simple and easy to setup
    - Example: we want the average ASG CPU to stay around 40%
- **Simple/Step Scaling**
    - Example: 
        - When a CloudWatch alarm is triggered (example average CPU > 70%), then add 2 units
        - When a CloudWatch alarm is triggered (example average CPU < 30%), then remove 1 unit
- **Scheduled Actions**
    - Can be used if we can anticipate scaling based on known usage patterns
    - Example: increase the min capacity to 10 at 5 PM on Fridays

### Scaling Cool-downs

- The cool-down period helps to ensure that our ASG doesn't launch or terminate additional instances before the previous scaling activity takes effect
- In addition to default cool-down for ASG we can create cool-downs that apply to specific *simple scaling policy*
- A scaling-specific cool-down overrides the default cool-down period
- Common use case for scaling-specific cool-downs is when a scale-in policy terminates instances based in a criteria or metric. Because this policy terminates instances, an ASG needs less time to determine wether to terminate additional instances
- If the default cool-down period of 300 seconds is too long, we can reduce costs by applying a scaling-specific cool-down of 180 seconds for example
- If our application is scaling up and down multiple times each hour, we can modify the ASG cool-down timers and the CloudWatch alarm period that triggers the scale

## Suspend and Resume Scaling Processes

- We can suspend and then resume one or more of the scaling processes for our ASG. This can be useful when we want to investigate a configuration problem or other issue with our web application and then make changes to our application, without invoking the scaling processes.
- We can manually move an instance from an ASG and put it in the standby state
- Instances in standby state are still managed by Auto Scaling, are charged as normal, and do not count towards available EC2 instance for workload/application use. Auto scaling does not perform health checks on instances in the standby state. Standby state can be used for performing updates/changes/troubleshooting etc. without health checks being performed or replacement instances being launched.

## ASG for Solutions Architects

- **ASG Default Termination Policy**
    1. Find the AZ which has to most number of instances
    2. If there are multiple instances to choose from, delete the one with the oldest launch configuration
- Lifecycle Hooks
    - By default as soon as an instance is launched in an ASG, the instance goes in service
    - ASGs provide the ability to perform extra steps before the instance goes in service
    - Also, we have he ability to perform some actions before the instance is terminated
    - Lifecycle hooks diagram: https://docs.aws.amazon.com/autoscaling/ec2/userguide/lifecycle-hooks.html
- Launch Templates vs. Launch Configurations
    - Both allow to specify the AMI, the instance type, a key par, security groups and the other parameters that we use to launch EC2 instances (tags, user-data, etc.)
    - Launch Configurations are considered to be legacy:
        - They must be recreated every time
    - Launch Templates:
        - They can have multiple versions
        - They allow parameter subsets used for partial configuration for re-use and inheritance
        - We can provision both On-Demand and Spot instances (or a mix of two)
        - We can use the T2 unlimited burst feature
        - Recommended by AWS





