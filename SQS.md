# SQS   
### What is SQS? 
Amazon SQS is a web service that gives you acces to a message queue that can be used to store messages while waiting for a computer to process them.    
Amazon SQS is a distributed queue system that enables web service applications to quickly and reliably queue messages that one component in the appication generates to be consumed by another component.
A queue is a temporary repo for messages that are awaiting procesing.   

Using Amazon SQS, you can decouple the components of an application so they run independtnly, easing message management between components.  
Any component of a distributed application can store messags in the queue.  Messages can contain up to 256KB of text in any format.  Any component can later retrieve the messages programmatically using the Amazon SQS API.  
The queue acts as a buffer between the component producing and saving the data, and the component receiving the data for processing.  This means the queue resolves issues that arise if the producer is producing work faster than the consumer can process it, or if the producer or consumer are only intermittently connected to the network.  
**SQS is a pull based system**   
### Queue Types   
**Standard Queues (default)**   
Amazon SQS offers standard as the dfault queue type.  As standard queue lets you have a nearly-unlimited number of transactions per second.  Standard queues guarantee that a message is delivered at least once.  
However, occasinally (because of the highly-distributed architecture that allows high throughput), more than one copy of a message might be delivered out of order.  
Standard queues provide best-effort ordering which ensures that messages are generally delivered in the same order as they are sent.   
**FIFO Queues (First-In-First-Out)**   
The FIFO queue complements the standard queue.  The most important features of this queue type are FIFO delivery and exactly once processing.    
The order in which messages are sent and received is strictly perserved and a message is delivered once and remains available until a consumer processes and deletes it; duplicates are not introduced into the queue.  
FIFO queues also support messages groups that allow multiple ordered message groups within a single queue.  FIFO queues are limited to 300 transactions per second (TPS), but have all the capabilities of standard queues.    
### SQS Key Facts      
- SQS is pull-based, not pushed-based   
- Messages are 256KB in size   
- Messages can be kept in th3e queue from 1 minute to 14 days    
- Default retention period is 4 days   
- SQS guarantees that your messages will be processed at least once   
### SQS Visibility Timeout   
- The visibility timeout is the amount of time that the message is invisible in the SQS queue after a reader picks up that message.  Provided the job is processed before the visibility timeout expires, teh message will then be deleted from the queue.  If the job is not processed within that time, the message will become visible agian and another reader will process it.  This could result in teh same message being delivered twice.   
- Default Visibility Timeout = 30 seconds   
- Increase it if your tasks take > 30 seconds   
- Max = 12 hours   
### SQS Long Polling   
- Amazon SQS long polling is a way to retrieve messages from yoru Amazon SQS queues   
- While the regular short polling returns immmediately (eve if the message queue being polled is empty), long polling doesn't return a response until a message arrives in the message queue, or the long poll times out   
- As such, long polling can save you money    
## Exam Tips   
- SQS is a distributed message queueing system   
- Allows you to decouple the components of an application so that they are independent  
- Pull based, not push-based   
- Standard Queues (default) - best-effort ordering; messages delivered at least once   
- FIFO Queues - ordering strictly preserved, messages delivered once, no duplicates; e.ge good for banking transactions which need to happen in a strict order    
- Visiblity Timout    
  - Default is 30 seconds - increase if your task takes > 30 seconds to complete    
  - Max 12 hours    
- Short polling - returned immediately even if no message are in the queue    
- Long polling - polls the queue periodically and only returns a response when a message iws in the queue or the timeout is reached    
# Simple Notification Service (SNS)   
### What is SNS?    
**Amazon SNS** is a web service that makes it easy to set up, operate and send notifications from the cloud.  
It provides developers witha highly scalable, flexible, and cost effective capability to publish messages from an application and immediately deliver them to subscribers or other applications.    
- Push notifications to Apple, Google, Fire, OS devices... 
- Besides pushing cloud notifications to mobile defvices, Amazon SNS can also deliver notifications by SMS text message or email to Amazon SQS or any HTTP endpoint    
- SNS notifications can also trigger Lambda functions: 
  - message publishd to an SNS topic
  - Lambda function is a subscriber --> trigger
  - Lambda function is invoked with payload of message    
    - Can manipulate the information or the message, publish the message to another SNS topic or send the message to other AWS services   
### SNS Topic   
SNS Allows you to group multliple recipients using tpics.  A tpic is an "access point" for allowing recipients to dynamically subscribe for identical copies of the same notification. 
One topic can support deliveries to multiple endpoint types - e.g. group andoid, iOS and SMS recipients    
When you publish once to a topic, SNS delivers appropriately formatted copies of your message to each subsriber.   
- To prevent messages from being lost, all messages published to Amazon SNS are stored redundantly across multiple availability zones    
### Benefits    
- Instantaneous, push-based delivery (no polling)    
- Simple APIs and easy integration with applications   
- Flexible message delivery over multiple transport protocols    
- Inexpensive, pay-as-you-go model with no up-front costs   
- Web-based AWS Management Console offers the simplicity of a point-and-click interface   
### SNS vs. SQS    
- Both Messaging Services in AWS
- SNS --> Push   
- SQS --> Polls (Pulls)    
### SNS Pricing    
- $0.5 per 1M SNS request    
- $0.06 per 100K Notification deliveries over HTTP   
- $0.75 per 100 Notifications over SMS   
- $2.00 per 100K Notifications over email   
### SNS    
SNS follows the "publish-subscribe" (pub-sub) messaging paradigm, with notifications being delivered to clients using a "push" mechanism that eliminates the need to periodically check or "poll" for new information and updates.      
With simple APIs requiring minimial up-front development effort, no maintenance or management overhead and pay-as-you-go pricing, SNS gives devlopers an easy mechanisim to incorporate a powerful notificatin system with their applications.     
## Exam Tips   
- SNS is a scalable and highly available notification service which allows you to send push notifications from the cloud   
- Variety of message formats suppored: SMS, email, SQS, HTTP endpoints   
- Pub-sub model whereby users subscribe to topics   
- It's a push mechanisim, rather than a pull (poll) mechanism    
- In serverless section    
# SES vs. SNS   
*Amazon SES (Simple Email Service)** is a scalable and highly available email service designed to help marketing teams and application developers send marketing, notification and transactional emails to their customers using a a pay as you go model.   
Can also be use dto recieve emails: incoming mails can be delivered automatically to an S3 bucket.    
Incoming mails can be used to trigger Lambda functions and SNS notifications. 
### SES Use Cases    
- Automated emails    
- Purchase confirmations, shipping notifications, order status updates - e.g. a mibile phone company that needs to send automated confirmation emails every time a customer purchases pre-paid mobile phone minutes   
- Marketing communications, advertisements, newsletters, special offers - e.g. an online retail business that needs to let customers know about sales promotions and discounts   
**SES is asynchronous - SNS is synchronous** . 
SES: An email address is all thats required to start sending messags to a user   
SNS: Consumers must subscribe to a topic to receieve the notifications   
# Kinesis 101    
### What is streaming data?   
Data that is generated continuously by thousands of data sources, which typically send in the data records simultaneously and in small sizes (kilobytes).   
- Purchaes from online stores (think amazon.com)   
- Stock prices   
- Game data    
- Social network data   
- Geospacial data (think uber.com)    
- iOT sensor data   
### What is Kinesis?   
**Amazon Kinesis** is a platform on AWS to send your streaming data too.  Kinesis makes it easy to load and analyze streaming data, and also providing the ability for you to build your own custom applications for your business needs.     
### Core Kinesis Services    
**Kinesis Streams**: Consist of shards
- Manual scaling   
- 5 transactions per second for reads up to a max total data read rate of 2MB per second 
- 1,000 records per second for write, up to a max total data write rate of 1MB per second (including partition keys)   
- The Data capacity of your stream is a function of the number of shards that you specify for the stream.  The total capacity of the stream is the sum of the capacities of its shards        
- Data is retained from 24 hours to seven days (Default is 24 hours)   
**Kinesis Firehose**:
- Autoscaling    
- Automated - firehose just send data to S3   
- An ingestion engine   
**Kinesis Analytics**   
- Analyzing the data inside Kensis - running SQL queries on data as it exists in Firehose or Streams   
- Store that SQL query inside S3, Redshift, Elasticsearch Cluster    
## Exam Tips   
- Know the difference between Kinesis Streams and Kenisis Firehose.  You will be given scenario questions and you must choose the most relevant service.  
  - Question about shards --> streams 
  - Question about analyzing data using Lambda --> firehose . 
- Understand what Kenisis Analytics is.
# Elastic Beanstalk    
### What is Elastic Beanstalk?      
**Elastic Beanstalk** is a service for deploying and scaling web applications developed in many popular languages: Java, .NET, PHP, Node.js, Python, Ruby, Go and Docker onto widely used application server plaforms like Apache Tomcat, Nginx, Passenger and IIS.  
Developers can focus on writing code and don't need tow orry about any of the underlying infrastucture needed to run the application.   
A provisioning service.     
You uplode the code and Elsastic Beanstalk will handle deployment, capacity provisioning, load balancing, auto-scaling and application health.  
You retain full control of the underlying AWS resources powering your application and you pay onl for the AWS resources required to store and run your applications - e.g. EC2 instances and S3 buckets.   
- Fastest and simplest way to deploy your application in AWS  
- Automacially scales your application up and down      
- You can select the EC2 instance type that is optimal for your application    
- You can retain full admin control over the resources powering your appliation, or have Elastic Beanstalk do it for you    
- Managed Platform Updates feature automatically applies updates to your OS, Java, PHP, Node.js, etc.   
- Monitor and manage application health via a dashboard    
- Integrated with CloudWatch and X-Ray for performance data and metrics   
## Exam Tips    
- Deploys and scales your web applications including the web application server platform where required 
- Provisions underlying resources for you    
# Updating Elastic Beanstalk   
### EBS Deployement Policies    
**Elastic Beanstalk** supports several options for processing deployments: 
1) All at once 
  - Deploys the new version to all instance simultaneously    
  - All of your instances are out of service while the deployment takes place   
  - You will experience an outage while the deployment is taking place - not ideal for mission-critical production systems   
  - If the update fails, you need to roll back the changes by re-deployging the original version to all your instances   
2) Rolling   
  - Deploys the new version in bactches      
  - Ecah bacth of intances is taken out of service while the deployment takes place   
  - Your env capacity will be reduced by the number of instances in a batch while the deployment takes place   
  - Not ideal for performance sensitive systems   
  - If the update fails, you need to perform and additional rolling update to roll back the changes   
3) Rolling with additional batch   
  - Launches an additional batch of instances    
  - Deploys the new verions in batches   
  - Maintains full capacity during the deployment process   
  - If the update fails, you need to perform an additional rolling update to roll back the changes   
4) Immutable   
  - Deploys the new version to a fresh group of instances in their own new autoscaling group   
  - When the new instances pass their health checks, they are moved to your existing auto scaling group; and finally, the old instances are terminated   
  - Maintains full capacity during the deployment process   
  - The impace of a failed update is far less, and the rollback process requires only terminating the new auto scaling group   
  - *Preferred option for *Mission Critical production systems*   
## Exam Tips 
1) All at once 
  - Service interruption while you update the entire env at once1) All at once 
  - To roll back, perform a further all at once upgrade
2) Rolling     
- Reduced capacity during deployment     
- To roll back, perform a further rolling update     
3) Rolling with Additional Batch     
- Maintains full capacity     
- To roll back, perform a further rolling update    
4) Immutable: *Preferred choice for mission critical systems*
- Maintains full capacity         
- To roll back, just delete the new instances and autoscaling group         
# Advanded Elastic Beanstalk        
You can customize your Elastic Beanstalk env using Elastic Beanstalk config files (e.g. you can define packages to install, create Linux users and groups, run shell commands, specifiy services to enable or configure your load balancer, etc.)        
These are files written in YAML or JSON format. They can have a filename of your choice but must have a .config extension and be saved inside a folder called **.ebextensions**. 
The **.ebextension** folder must be in teh top-level directory of your application source bundle.    
This means that the configuration files can be placed under source control along with the rest of your application code.         
# RDS & Elastic Beanstalk        
Elastic Beanstalk supports two ways of integrating an RDS database with your Beanstlk env.          
You can launch the RDS instance from whthin the Elastic Beanstalk console, which means the RDS instance is created within your Elastic Beanstalk env - a good option for Dev and Test deployments.           
However this may not be idal for prouduction envs because it means the lifecycle of your database is tied to the lifecycle of your application env.  If you terminate the env, the database instance will be terminated too.    
*For production envs*, the preferred option is to decouple the RDS instance from yoru EBS env: i.e. launch it outside of Elastic Beanstalk, directly from the RDS section of the console.   
This option gives you a lot more flexibility, allows you to connect multiple envs to the same database, provides a wider choice of database types and allows you to tear down your application env without affecting the database instance.   
### Access to RDS from Elastic Beanstalk        
To allow the EC2 instance in your Elastic Beanstlk env to connet to an outside databse, there are two additional configuration steps required: 
- An additional Security Group must be added to your env's Auto Scaling Group        
- You'll need to provide connection sgring configuration information to your application servers (endpoint, password, using Elastic Beanstalk env properties)         
## Exam Tips        
Two different options for launching your RDS instance        
**Launch within Elastic Beanstalk**        
- When you termiante the EB env, the databadse will also be terminated        
- Quick and easy to add your DB and get started        
- Suitable for Dev and Test envs only         
**Launch outside of Elastic Beanstalk**        
- Additional config steps required        
  - Security Group and Connection Information         
- Suitable for prod envs, more flexibility         
- Allows connection from multiple envs, you can tear downt he application stack without impacting the DB        
# System Manager and Parameter Store        
### Real World Scenario        
You work for a bank as a systems admin.  You need to store confidential information such as users, passwords, license keys, etc.  This information needs to be passed to EC2 as a bootstrap script, while maintaining the confidentiality of the information.    
## Exam Tips         
- Confidential info such as passwrods, DB connection strings and license codes can be stored in SSM Parameter Store        
- You can store values as plain text or you can encrypt the data        
- You can then reference these values by using their names        
- You can use this service with EC2, CloudFormation, Lambda, EC2 Run command, etc.  
