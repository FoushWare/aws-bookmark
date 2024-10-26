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

Resource: practise Article https://aws.plainenglish.io/access-aws-s3-buckets-without-internet-connection-ff65ccfd1cc7


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


## Question 6

A company uses NFS to store large video files in on-premises network attached storage. Each video file ranges in size from 1 MB to 500 GB. The total storage is 70 TB and is no longer growing. The company decides to migrate the video files to Amazon S3. The company must migrate the video files as soon as possible while using the least possible network bandwidth.  
**Which solution will meet these requirements?**

- [ ] **A.** Create an S3 bucket. Create an IAM role that has permissions to write to the S3 bucket. Use the AWS CLI to copy all files locally to the S3 bucket.
- [ ] **B.** Create an AWS Snowball Edge job. Receive a Snowball Edge device on premises. Use the Snowball Edge client to transfer data to the device. Return the device so that AWS can import the data into Amazon S3.
- [ ] **C.** Deploy an S3 File Gateway on premises. Create a public service endpoint to connect to the S3 File Gateway. Create an S3 bucket. Create a new NFS file share on the S3 File Gateway. Point the new file share to the S3 bucket. Transfer the data from the existing NFS file share to the S3 File Gateway.
- [ ] **D.** Set up an AWS Direct Connect connection between the on-premises network and AWS. Deploy an S3 File Gateway on premises. Create a public virtual interface (VIF) to connect to the S3 File Gateway. Create an S3 bucket. Create a new NFS file share on the S3 File Gateway. Point the new file share to the S3 bucket. Transfer the data from the existing NFS file share to the S3 File Gateway.

### Answer and Explanation

**Correct Answer:** **B.** Create an AWS Snowball Edge job. Receive a Snowball Edge device on premises. Use the Snowball Edge client to transfer data to the device. Return the device so that AWS can import the data into Amazon S3.

#### Explanation:

- **AWS Snowball Edge** provides a high-speed, offline data transfer solution, ideal for large-scale data migration without using network bandwidth. Snowball Edge devices are shipped to the customer’s premises, where data is loaded locally, then returned to AWS for direct import into S3.
- **Minimal Network Usage:** This solution avoids reliance on the network, which is beneficial for transferring large datasets quickly.

#### Why Other Options Are Less Suitable:

- **Option A:** Using the AWS CLI to upload 70 TB over the network would consume a significant amount of bandwidth and may not be feasible within a short timeframe.
- **Option C:** S3 File Gateway would still rely on network bandwidth, potentially slowing down the migration process.
- **Option D:** AWS Direct Connect provides a dedicated line but would require setup time and potentially higher costs for a one-time migration.

## Question 7

A company has an application that ingests incoming messages. Dozens of other applications and microservices then quickly consume these messages. The number of messages varies drastically and sometimes increases suddenly to 100,000 each second. The company wants to decouple the solution and increase scalability.  
**Which solution meets these requirements?**

- [ ] **A.** Persist the messages to Amazon Kinesis Data Analytics. Configure the consumer applications to read and process the messages.
- [ ] **B.** Deploy the ingestion application on Amazon EC2 instances in an Auto Scaling group to scale the number of EC2 instances based on CPU metrics.
- [ ] **C.** Write the messages to Amazon Kinesis Data Streams with a single shard. Use an AWS Lambda function to preprocess messages and store them in Amazon DynamoDB. Configure the consumer applications to read from DynamoDB to process the messages.
- [ ] **D.** Publish the messages to an Amazon Simple Notification Service (Amazon SNS) topic with multiple Amazon Simple Queue Service (Amazon SQS) subscriptions. Configure the consumer applications to process the messages from the queues.

### Answer and Explanation

**Correct Answer:** **D.** Publish the messages to an Amazon Simple Notification Service (Amazon SNS) topic with multiple Amazon Simple Queue Service (Amazon SQS) subscriptions. Configure the consumer applications to process the messages from the queues.

#### Explanation:

- **Amazon SNS** is ideal for applications where messages need to be sent to multiple destinations, as it can broadcast messages to multiple SQS queues. 
- **Amazon SQS** provides scalability by allowing consumers to pull messages independently, which helps handle large surges in message volume. SQS scales automatically and supports decoupling, allowing each consumer to process messages independently.

#### Why Other Options Are Less Suitable:

- **Option A:** Amazon Kinesis Data Analytics is more suited for real-time data analytics rather than decoupling and distributing high-volume messages to multiple applications.
- **Option B:** Scaling EC2 instances in an Auto Scaling group based on CPU utilization does not inherently support message queuing or decoupling.
- **Option C:** A single Kinesis shard would not handle 100,000 messages per second and would likely result in bottlenecks. Multiple shards would be necessary, but Kinesis Data Streams is more complex and suited for streaming rather than broad message distribution.

## Question 8

A company is migrating a distributed application to AWS. The application serves variable workloads. The legacy platform consists of a primary server that coordinates jobs across multiple compute nodes. The company wants to modernize the application with a solution that maximizes resiliency and scalability.  
**How should a solutions architect design the architecture to meet these requirements?**

- [ ] **A.** Configure an Amazon Simple Queue Service (Amazon SQS) queue as a destination for the jobs. Implement the compute nodes with Amazon EC2 instances that are managed in an Auto Scaling group. Configure EC2 Auto Scaling to use scheduled scaling.
- [ ] **B.** Configure an Amazon Simple Queue Service (Amazon SQS) queue as a destination for the jobs. Implement the compute nodes with Amazon EC2 instances that are managed in an Auto Scaling group. Configure EC2 Auto Scaling based on the size of the queue.
- [ ] **C.** Implement the primary server and the compute nodes with Amazon EC2 instances that are managed in an Auto Scaling group. Configure AWS CloudTrail as a destination for the jobs. Configure EC2 Auto Scaling based on the load on the primary server.
- [ ] **D.** Implement the primary server and the compute nodes with Amazon EC2 instances that are managed in an Auto Scaling group. Configure Amazon EventBridge (Amazon CloudWatch Events) as a destination for the jobs. Configure EC2 Auto Scaling based on the load on the compute nodes.

### Answer and Explanation

**Correct Answer:** **B.** Configure an Amazon Simple Queue Service (Amazon SQS) queue as a destination for the jobs. Implement the compute nodes with Amazon EC2 instances that are managed in an Auto Scaling group. Configure EC2 Auto Scaling based on the size of the queue.

#### Explanation:

- **Amazon SQS** provides a reliable queue to decouple and distribute tasks across compute nodes, which improves the system's resiliency and scalability.
- **Auto Scaling based on SQS queue size** allows the number of compute nodes to scale dynamically with the workload, automatically adjusting to changes in job volume without a primary server dependency.

#### Why Other Options Are Less Suitable:

- **Option A:** Scheduled scaling does not offer real-time scaling based on workload demand, making it less resilient to sudden workload changes.
- **Option C:** AWS CloudTrail is not designed for job distribution; it monitors API calls and activity within an AWS account.
- **Option D:** Amazon EventBridge is event-driven, but it is not typically used for coordinating a high-volume job distribution system like SQS.

## Question 9

A company is running an SMB file server in its data center. The file server stores large files that are accessed frequently for the first few days after the files are created. After 7 days, the files are rarely accessed. The total data size is increasing and is close to the company's total storage capacity. A solutions architect must increase the company's available storage space without losing low-latency access to the most recently accessed files. The solutions architect must also provide file lifecycle management to avoid future storage issues.  
**Which solution will meet these requirements?**

- [ ] **A.** Use AWS DataSync to copy data that is older than 7 days from the SMB file server to AWS.
- [ ] **B.** Create an Amazon S3 File Gateway to extend the company's storage space. Create an S3 Lifecycle policy to transition the data to S3 Glacier Deep Archive after 7 days.
- [ ] **C.** Create an Amazon FSx for Windows File Server file system to extend the company's storage space.
- [ ] **D.** Install a utility on each user's computer to access Amazon S3. Create an S3 Lifecycle policy to transition the data to S3 Glacier Flexible Retrieval after 7 days.

### Answer and Explanation

**Correct Answer:** **B.** Create an Amazon S3 File Gateway to extend the company's storage space. Create an S3 Lifecycle policy to transition the data to S3 Glacier Deep Archive after 7 days.

#### Explanation:

- **Amazon S3 File Gateway** allows seamless integration with existing SMB applications, providing low-latency access to frequently accessed files while extending storage capacity.
- By using an **S3 Lifecycle policy**, files can automatically transition to **S3 Glacier Deep Archive** after 7 days, optimizing storage costs and managing lifecycle efficiently.

#### Why Other Options Are Less Suitable:

- **Option A:** AWS DataSync would be suitable for transferring data but does not provide low-latency access to recent files.
- **Option C:** Amazon FSx for Windows File Server is an option but may be more complex and costly than necessary for just extending storage capacity and lifecycle management.
- **Option D:** Installing a utility on each user's computer is not ideal for seamless integration and does not provide a lifecycle management feature like S3 File Gateway.

## Question 10

A company is building an ecommerce web application on AWS. The application sends information about new orders to an Amazon API Gateway REST API to process. The company wants to ensure that orders are processed in the order that they are received.  
**Which solution will meet these requirements?**

- [ ] **A.** Use an API Gateway integration to publish a message to an Amazon Simple Notification Service (Amazon SNS) topic when the application receives an order. Subscribe an AWS Lambda function to the topic to perform processing.
- [ ] **B.** Use an API Gateway integration to send a message to an Amazon Simple Queue Service (Amazon SQS) FIFO queue when the application receives an order. Configure the SQS FIFO queue to invoke an AWS Lambda function for processing.
- [ ] **C.** Use an API Gateway authorizer to block any requests while the application processes an order.
- [ ] **D.** Use an API Gateway integration to send a message to an Amazon Simple Queue Service (Amazon SQS) standard queue when the application receives an order. Configure the SQS standard queue to invoke an AWS Lambda function for processing.

### Answer and Explanation

**Correct Answer:** **B.** Use an API Gateway integration to send a message to an Amazon Simple Queue Service (Amazon SQS) FIFO queue when the application receives an order. Configure the SQS FIFO queue to invoke an AWS Lambda function for processing.

#### Explanation:

- **Amazon SQS FIFO (First-In-First-Out) queue** ensures that messages are processed in the exact order they are sent. This feature is crucial for an ecommerce application that requires orders to be processed in the order they are received.
- Integrating the API Gateway with an SQS FIFO queue allows the application to reliably manage order processing, maintaining the correct sequence of order handling.

#### Why Other Options Are Less Suitable:

- **Option A:** SNS is designed for fan-out scenarios and does not guarantee message order, which does not meet the requirement of processing orders in the order they are received.
- **Option C:** Blocking requests using an API Gateway authorizer is not a practical approach to managing order processing order and could lead to increased latency and poor user experience.
- **Option D:** SQS standard queues do not guarantee the order of message processing, making this option unsuitable for the requirement of sequential order processing.


