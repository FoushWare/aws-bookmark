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
