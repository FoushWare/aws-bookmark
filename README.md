

# hands-on course 
- https://www.udemy.com/course/aws-certified-solutions-architect-associate-saa-c03/?kw=aws+sol&src=sac&couponCode=2021PM25
- https://aws.amazon.com/training/learn-about/architect/
- [this is my archeticture](https://aws.amazon.com/architecture/this-is-my-architecture/?tma.sort-by=item.additionalFields.airDate&tma.sort-order=desc&awsf.category=*all&awsf.industry=*all&awsf.language=*all&awsf.show=*all&awsf.product=*all)

# notes 
- [set of articles](https://chloemcateer.medium.com/aws-solution-architect-associate-exam-study-notes-b6c5884ee500)
- notes for each part of the course https://github.com/Ernyoke/certified-aws-solutions-architect-associate
- https://github.com/saumyap24/aws-solutions-architect-associate-notes?tab=readme-ov-file


# Guid 
- https://rxhl.notion.site/AWS-Solution-Architect-Associate-698442acf94a484caa56477344dafc9d
- https://tutorialsdojo.com/aws-certified-solutions-architect-associate-saa-c03/


# My-notes 

-> IAM service
==================
![Logo](https://raw.githubusercontent.com/FoushWare/aws-bookmark/master/1_nQuYpC8oelxaqke2VXPw2w.webp?token=GHSAT0AAAAAACUSL73UEIXQBH7ZAQKCSGJKZVURI6A)

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

EC2 
![Logo](https://raw.githubusercontent.com/FoushWare/aws-bookmark/master/1_joI3hN7W6ZtT-xda7Mp8Bw.webp?token=GHSAT0AAAAAACUSL73VWXIS6GAWUTWESOUMZVUUYZQ)
====================



