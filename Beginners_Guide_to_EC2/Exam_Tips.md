# EC2 101   
***FIGHT A DR MC PXZ*** 
**EC2 Instance Types**

### F   
**Accelerated Computing**   
Field Programable Gate Arrays: Customizable hardware acceleration.    
**Use Case**   
Genomics research, financial analytics, real-time video processing, big data search and analysis, and security.     
### I 
**Storage Optimized**   
IPOS: Optimized for low latency, very high random I/O performance, high sequential read through.    
**Use Case**  
NoSQL databases (e.g. Cassandra, MongoDB, Redis), in-memory databases (e.g. Aerospike), scale-out transactional databases, data warehousing, Elasticsearch, analytics workloads.
### G 
**Acceleratd Computing**  
Graphics: accelerate machine learning inference and graphics-intensive workloads.   
**Use Case**   
Machine learning inference for applications like adding metadata to an image, object detection, recommender systems, automated speech recognition, and language translation; and 3D visualizations, 3D rendering, video encoding.   
### H   
**Storage Optimized**   
High Disk Throughput: Balanced compute and memory.    
**Use Case**     
MapReduce-based workloads, distributed file systems such as HDFS and MapR-FS, network file systems, log or data processing applications such as Apache Kafka, and big data workload clusters.
### T
**General Purpose**    
Burstable, general purpose instance type.   
**Use Case**   
Websites and web applications, development environments, build servers, code repositories, micro services, test and staging environments, and line of business applications.   
### A   
**General Purpose**   
Deliver significant cost savings and are ideally suited for scale-out and Arm-based workloads that are supported by the extensive Arm ecosystem.    
**Use Case**  
Scale-out workloads such as web servers, containerized microservices, caching fleets, and distributed data stores, as well as development environments.   
### D  
**Storage Optimized**   
Density: High disk throughput, large local storage.    
**Use Case**  
Massively Parallel Processing (MPP) data warehousing, MapReduce and Hadoop distributed computing, distributed file systems, network file systems, log or data-processing applications.    
### R  
**Memory Optimized**   
RAM: ideal for memory bound workloads.     
**Use Case**   
Well suited for memory intensive applications such as high performance databases, distributed web scale in-memory caches, mid-size in-memory databases, real time big data analytics, and other enterprise applications.
### M   
**General Purpose**  
Main choice for general purpose apps; balance compute, memory and networking.
**Use Case**   
Applications built on open-source software such as application servers, microservices, gaming servers, mid-size data stores, and caching fleets.
### C    
**Compute Optimized**    
Ideal for compute bound applications that benefit from high performance processors. 
**Use Case**  
High performance web servers, scientific modelling, batch processing, distributed analytics, high-performance computing (HPC), machine/deep learning inference, ad serving, highly scalable multiplayer gaming, and video encoding.
### P   
**Accelerated Computing**   
Graphics: GPU instances.   
**Use Case**   
Machine/Deep learning, high performance computing, computational fluid dynamics, computational finance, seismic analysis, speech recognition, autonomous vehicles, drug discovery.    
### X  
**Memory Optimized**   
Extreme Memory: Ideally suited for memory intensive large-scale, enterprise-class in memory applications.   
**Use Case**   
High performance databases, in-memory databases (e.g. SAP HANA) and memory intensive applications.
### Z  
**Memory Optimized**   
High compute and high memory foot print - fastest cloud instance.   
**Use Case**   
Ideal for electronic design automation (EDA) and certain relational database workloads with high per-core licensing costs.

## Exam Tips 
#### EC2 Pricing   
- On Demand: Allows you to pay a fixed rate by hour (or second) with no commitment     
- Reserved: Provides you with a capacity reservation and offer a siginificant discount on the hourly charge for an instance.  1 Year or 3 Year terms avaiable    
- Spot: Enables bidding for instance capacity, providing for even greater savings if your applications have flexible start and end times    
- Dedicated Hosts: Physical EC2 servers dedicated for your use.  Can reduce costs by allowing you to use your existing sever-bound software licenses  
#### EBS   
**SSD**    
- General Purpose SSD: Balances price and performance for a wide variety of workloads   
- Provisioned IOPS SSD: Highest performance SSD volume for mission-critical low-latency or high-throughput workloads   
**Magnetic**  
- Throughput Optimized HHD: Low cost HHD volume designed for frequently accessed, throughput-intensive workloads   
- Cold HHD - Lowest cost HDD volume designed for less frequently accessed workloads   
- Magnetic - Previous Generation, can be a boot volume    
# EC2 Lab    
No Tips    
# Elastic Load Balancer   
## Exam Tips   
Three different types of Load Balancers:    
- Application Load Balancers   
- Network Load Balancers   
- Classic Load Balancers   
504 Error means the gateway has timed out.  This means the application not responding with the idle time period.  Trouble shoot the application.  Is it the Web Server or Database Server?   
If you need th eIPv4 address of your end user, look for the X-Forwarded-For header.     
# Route 53 Lab   
No Tips   
# CLI Demo Lab  
## Exam Tips   
**Least Privilege** - Always give your users the minimum amount of access required   
**Create Groups** - Assign your users to groups.  Your users will automatically inherit the permissions of the group.  The groups permissiosn are assigned using *policy documents*. 
**Secret Access Key** - You will see this only once.  If you do not save it, you can delete the Key Pair and regenerate it.  You will need to run **aws configure** again.   
**Do not use just one access key** - Do not create just one access key and share that with all your developers.  If someone leaves the company on bad terms, then you will need to delete the key and create a new one and every developer would then need to update their keys.  Instead, create one key pair per developer.    
# EC2 with S3 Role Lab   
## Exam Tips    
- Roles allow you to not use Access Key ID's and Secret Keys
- Roles are **preferred** from a security perspective
- Roles are controlled by policies
- You can change a policy on a role and it will take immediate affect
- You can attach and detach roles to running EC2 instances without having to stop or terminate these instances   
# How to Encrypt an EBS Volume Attached to EC2 Lab   
## Exam Tips  
- You can encrypt the rood device volume (the volumem the OS is installed on) using Operating System level encryption.   
- You can encrypt the root device volume by first taking a snapshot of that volume, and then creating a copy of that snap with encryption.  You can then make an AMI of this snap and deploy the encrypted root device volume.   
- You can encrypt additional attached volumes using the console, CLI or API.    
# RDS 101  
### Notes   
#### Databases
RMDBS vs. NoSQL  
Databases vs. Data Warehouse
#### OLTP vs. OLAP   
Online Transaction Processing: Frequent but simple transactions   
Online Analytics PRocessing: More complex with large number of records   
Data Warehouseing databases use different type of architecture both from a database perspective and infrastructural layer. 
#### Elasticache  
Web service that makes it easy to deploy, operate and scale an in-memory cache in the cloud.  The service improves the performace of web applications by allowing you to retrieve information from fast, managed, in-memory caches.    
**Two open source in-memory caching engines:**   
1) Memcached
2) Redis 
## AWS Database Types - Summary    
- RDS - OLTP   
   - SQL  
   - MySQL   
   - PostgreSQL   
   - Oracle   
   - Aurora   
   - MariaDB   
- DynamoDB - NoSQL      
- RedShift - OLAP  
- Elasticache - In Memory Caching:    
   - Memcached   
   - Redis 
# RDS Lab
## Common Exam Question   
EC2 instance and RDS in two different security groups, they can not interface with one another.  What do you do?
*Need to open up port 3306 in the RDS security group instance to teh security group where the EC2 instance is located* Allow the two security groups to talk to one another.    
# RDS - Back Ups, Multi-AZ & Read Replicas  
#### Back Ups   
Two types of backups:   
1) Automated Backups: allow you to recover your database to any point in time within a **retention period**; this can be between one and 35 days.  Automated Backups will take a full daily snapshot and will also store transaction logs throughout the day.  When you do a recovery, AWS will first choose the most recent daily backup and then apply transaction logs relevant to that day.  This allows you to do a point in time recovery down to a second, within the retention period.  
- Enabled by default  
- Stored in S3  
- Free storage space equal to the size of your DB 
2) Snapshot: done manually.  Stored even after you delete the original RDS instance, unlike automated backups.   
Restoring backups will result in new RDS instance with new DNS endpoint. 
#### Multi-AZ  
***For diaster recovery only, not for improving performance***    
Allows you to have an exact copy of your production database in another Availability Zone.  AWS handles the replication for you, so when your production database is written to, this write will automatically be synchronized to the standby databse.  
In the event of planned database maintenance, DB instance falure or an AZ failure, Amazon RDS will automatically failover to the standby so that DB operations can resume quickly without admin intervention.  
Multi-AZ Databases:   
- SQL Server  
- Oracle   
- MySQL Server  
- PostgreSQL    
- MariaDB   
- Aurora  
#### Read Replica  (Scaling out)
5 Read replicas per production DB by default 
Allow you to have a read-only copy of your production DB.  Achieved by using Asychronous replication from the primary RDS instance to the read replicas.  You use the read replicas primarily for very read-heavy DB workloads.   
Read Replica Databases:   
- MySQL Server  
- PostgreSQL  
- MariaDB   
- Aurora  
##### Notes:   
- Used for scaling, **not** for disaster recovery!   
- Must have automatic backups turned on in order to deploy a read replica   
- You can have up to 5 read replica copies of any database  
- You can have read replicas of read replicas (but watch out for latency)   
- Each read replica will have its own DNS end point  
- You **can** have read replicas that have Multi-AZ  
- You **can** create read replicas of Multi-AZ source databases  
- Read replicas can be promoted to be their own databases.  This breaks the replication   
- You can have a read replica in a second region  







