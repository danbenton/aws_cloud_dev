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


