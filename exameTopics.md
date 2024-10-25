## Question 1

A company collects data for temperature, humidity, and atmospheric pressure in cities across multiple continents. The average volume of data that the company collects from each site daily is 500 GB. Each site has a high-speed Internet connection.  
The company wants to aggregate the data from all these global sites as quickly as possible in a single Amazon S3 bucket. The solution must minimize operational complexity.  
**Which solution meets these requirements?**

- [ ] **A.** Turn on S3 Transfer Acceleration on the destination S3 bucket. Use multipart uploads to directly upload site data to the destination S3 bucket.
- [ ] **B.** Upload the data from each site to an S3 bucket in the closest Region. Use S3 Cross-Region Replication to copy objects to the destination S3 bucket. Then remove the data from the origin S3 bucket.
- [ ] **C.** Schedule AWS Snowball Edge Storage Optimized device jobs daily to transfer data from each site to the closest Region. Use S3 Cross-Region Replication to copy objects to the destination S3 bucket.
- [ ] **D.** Upload the data from each site to an Amazon EC2 instance in the closest Region. Store the data in an Amazon Elastic Block Store (Amazon EBS) volume. At regular intervals, take an EBS snapshot and copy it to the Region that contains the destination S3 bucket. Restore the EBS volume in that Region.

### Answer and Explanation

**Correct Answer:** **A.** Turn on S3 Transfer Acceleration on the destination S3 bucket. Use multipart uploads to directly upload site data to the destination S3 bucket.

#### Explanation:

- **S3 Transfer Acceleration** allows for faster global uploads by utilizing Amazon CloudFront’s distributed edge locations, making it ideal for high-speed transfers over long distances.
- **Multipart uploads** facilitate large file transfers by breaking them into smaller parts, enabling efficient parallel uploads and reducing upload time.
- This approach keeps operational complexity low by avoiding additional infrastructure, replication, or deletion processes. Sites can directly upload data to the destination bucket with optimized transfer speeds.

#### Why Other Options Are Less Suitable:

- **Option B:** Cross-Region Replication increases operational complexity by requiring data management in origin buckets.
- **Option C:** AWS Snowball Edge is best for offline migration or limited internet bandwidth, which is unnecessary given high-speed internet at each site.
- **Option D:** Involves a complex setup with EC2, EBS, snapshots, and volume restoration, increasing operational complexity and delay in data aggregation.


## Question 2

A company needs the ability to analyze the log files of its proprietary application. The logs are stored in JSON format in an Amazon S3 bucket. Queries will be simple and will run on-demand. A solutions architect needs to perform the analysis with minimal changes to the existing architecture.  
**What should the solutions architect do to meet these requirements with the LEAST amount of operational overhead?**

- [ ] **A.** Use Amazon Redshift to load all the content into one place and run the SQL queries as needed.
- [ ] **B.** Use Amazon CloudWatch Logs to store the logs. Run SQL queries as needed from the Amazon CloudWatch console.
- [ ] **C.** Use Amazon Athena directly with Amazon S3 to run the queries as needed.
- [ ] **D.** Use AWS Glue to catalog the logs. Use a transient Apache Spark cluster on Amazon EMR to run the SQL queries as needed.

### Answer and Explanation

**Correct Answer:** **C.** Use Amazon Athena directly with Amazon S3 to run the queries as needed.

#### Explanation:

- **Amazon Athena** is a serverless, on-demand query service that allows users to directly analyze data stored in Amazon S3 without the need for data movement or infrastructure setup.
- **Minimal Operational Overhead:** Athena requires no additional infrastructure or complex setup. It supports querying JSON data directly from S3, which meets the company’s need for simple, on-demand queries with low maintenance.
- This solution maintains the existing architecture by allowing analysis directly on the S3-stored JSON logs.

#### Why Other Options Are Less Suitable:

- **Option A:** Amazon Redshift would require data loading, management, and a more complex setup, adding unnecessary operational overhead for simple queries.
- **Option B:** CloudWatch Logs is not designed for direct querying of JSON files stored in S3, and moving logs to CloudWatch adds complexity and storage costs.
- **Option D:** AWS Glue and Amazon EMR with Apache Spark are more suited for complex ETL and large-scale analytics, which would add significant operational overhead for on-demand querying.


## Question 3

A company uses AWS Organizations to manage multiple AWS accounts for different departments. The management account has an Amazon S3 bucket that contains project reports. The company wants to limit access to this S3 bucket to only users of accounts within the organization in AWS Organizations.  
**Which solution meets these requirements with the LEAST amount of operational overhead?**

- [ ] **A.** Add the aws PrincipalOrgID global condition key with a reference to the organization ID to the S3 bucket policy.
- [ ] **B.** Create an organizational unit (OU) for each department. Add the aws:PrincipalOrgPaths global condition key to the S3 bucket policy.
- [ ] **C.** Use AWS CloudTrail to monitor the CreateAccount, InviteAccountToOrganization, LeaveOrganization, and RemoveAccountFromOrganization events. Update the S3 bucket policy accordingly.
- [ ] **D.** Tag each user that needs access to the S3 bucket. Add the aws:PrincipalTag global condition key to the S3 bucket policy.

### Answer and Explanation

**Correct Answer:** **A.** Add the aws PrincipalOrgID global condition key with a reference to the organization ID to the S3 bucket policy.

#### Explanation:

- **PrincipalOrgID** is a global condition key that allows access to be restricted to all accounts within a specific AWS Organization. By adding this key to the S3 bucket policy with the organization ID, the bucket can be securely accessed only by users in accounts within the organization.
- **Minimal Operational Overhead:** This approach is straightforward to implement, requires no additional resources or tracking, and automatically applies access controls across all accounts within the organization.

#### Why Other Options Are Less Suitable:

- **Option B:** Using `aws:PrincipalOrgPaths` would require organizing accounts into specific OUs and managing policies based on path structure, which increases complexity.
- **Option C:** Relying on CloudTrail to monitor account changes and manually update policies would create significant operational overhead.
- **Option D:** Tagging individual users and managing permissions with `aws:PrincipalTag` is complex and difficult to scale, especially with multiple users across departments.


## Question 4

An application runs on an Amazon EC2 instance in a VPC. The application processes logs that are stored in an Amazon S3 bucket. The EC2 instance needs to access the S3 bucket without connectivity to the internet.  
**Which solution will provide private network connectivity to Amazon S3?**

- [ ] **A.** Create a gateway VPC endpoint to the S3 bucket.
- [ ] **B.** Stream the logs to Amazon CloudWatch Logs. Export the logs to the S3 bucket.
- [ ] **C.** Create an instance profile on Amazon EC2 to allow S3 access.
- [ ] **D.** Create an Amazon API Gateway API with a private link to access the S3 endpoint.

### Answer and Explanation

**Correct Answer:** **A.** Create a gateway VPC endpoint to the S3 bucket.

#### Explanation:

- **Gateway VPC Endpoint** for Amazon S3 allows EC2 instances in a VPC to privately connect to S3 without requiring an internet connection, as it enables secure and private access over the AWS internal network.
- **Minimal Operational Overhead:** This solution is simple to implement and provides the necessary private connectivity directly between the EC2 instance and the S3 bucket without additional configurations.

#### Why Other Options Are Less Suitable:

- **Option B:** Exporting logs through CloudWatch Logs adds unnecessary complexity and costs, as it doesn’t provide a direct private connection to S3 for the EC2 instance.
- **Option C:** An instance profile grants permissions to access S3 but does not ensure private network connectivity, as it still requires internet or a VPC endpoint.
- **Option D:** API Gateway with a private link is not intended for direct S3 access and would create unnecessary complexity and overhead.

## Question 5

A company is hosting a web application on AWS using a single Amazon EC2 instance that stores user-uploaded documents in an Amazon EBS volume. For better scalability and availability, the company duplicated the architecture and created a second EC2 instance and EBS volume in another Availability Zone, placing both behind an Application Load Balancer. After completing this change, users reported that, each time they refreshed the website, they could see one subset of their documents or the other, but never all of the documents at the same time.  
**What should a solutions architect propose to ensure users see all of their documents at once?**

- [ ] **A.** Copy the data so both EBS volumes contain all the documents.
- [ ] **B.** Configure the Application Load Balancer to direct a user to the server with the documents.
- [ ] **C.** Copy the data from both EBS volumes to Amazon EFS. Modify the application to save new documents to Amazon EFS.
- [ ] **D.** Configure the Application Load Balancer to send the request to both servers. Return each document from the correct server.

### Answer and Explanation

**Correct Answer:** **C.** Copy the data from both EBS volumes to Amazon EFS. Modify the application to save new documents to Amazon EFS.

#### Explanation:

- **Amazon EFS (Elastic File System)** provides a shared, scalable storage solution that can be accessed by multiple EC2 instances across Availability Zones. By storing documents in EFS, both instances can read and write to a single storage location, ensuring that users see a consistent set of documents regardless of which instance handles their request.
- **Scalability and Availability:** EFS is designed for multi-AZ access, making it ideal for high availability and scalability across multiple instances.

#### Why Other Options Are Less Suitable:

- **Option A:** Copying data between EBS volumes manually would be difficult to keep consistent, particularly as new documents are uploaded.
- **Option B:** Directing users to a specific server does not solve the issue of data consistency and may fail if an instance becomes unavailable.
- **Option D:** Sending requests to both servers adds unnecessary complexity and would not fully address consistency unless both EBS volumes are kept in sync, which is challenging with EBS.


