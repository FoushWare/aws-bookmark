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



