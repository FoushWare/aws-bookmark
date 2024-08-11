

# hands-on course 
- https://www.udemy.com/course/aws-certified-solutions-architect-associate-saa-c03/?kw=aws+sol&src=sac&couponCode=2021PM25
- https://explore.skillbuilder.aws/learn/learning_plan/view/1046/solutions-architect-learning-plan-includes-labs
- https://aws.amazon.com/training/learn-about/architect/
- [this is my archeticture](https://aws.amazon.com/architecture/this-is-my-architecture/?tma.sort-by=item.additionalFields.airDate&tma.sort-order=desc&awsf.category=*all&awsf.industry=*all&awsf.language=*all&awsf.show=*all&awsf.product=*all)

# notes 
- [set of articles](https://chloemcateer.medium.com/aws-solution-architect-associate-exam-study-notes-b6c5884ee500)
- notes for each part of the course https://github.com/Ernyoke/certified-aws-solutions-architect-associate
- https://github.com/saumyap24/aws-solutions-architect-associate-notes?tab=readme-ov-file


# Guid 
- https://rxhl.notion.site/AWS-Solution-Architect-Associate-698442acf94a484caa56477344dafc9d
- https://tutorialsdojo.com/aws-certified-solutions-architect-associate-saa-c03/

# practise exam questions
- https://www.youtube.com/watch?v=Wee_F8_k8s4
- https://github.com/Ditectrev/AWS-Certified-Solutions-Architect-Associate-SAA-C03-Practice-Tests-Exams-Questions-Answers?tab=readme-ov-file#which-set-of-amazon-s3-features-helps-to-prevent-and-recover-from-accidental-data-loss
- 
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
- virtual firewall for Ec2 instances
- all inbound traffic are blocked by default but all outbound traffic is allowed
- you add rules to security groups to allow traffic in.
- security groups are permitive this means you only use it to allow not to prevent or deny
- you can have more than security groups attached to EC2 instance

## EC2 Hibernate
- can be used to save the machine state
- it stories in-memeory RAM to storage EBS
- it can last more than 60 days
- once in hibrnate mode you are not charged you only charged for Elastic IP and other attached volums 

## EC2Placement Groups
- place EC2 instance to minimise failure
- placement groups must be unique across your account
- no charge associated with creating placement Groups

## types of placement groups:

1- clustered => the instances close together in same AZ aimed to provide high throughput and low network latency
2- spread  => can span multiple AZ used for smalll number of application to prevent failure 
3- partioned => .....










