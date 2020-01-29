# Lambda   
Lambda is a compute service where ou can upload your code and create a Lambda function.  AWS lambda takes care of provisioning and managing the servers that you use to run the code.  You don't have to worry about operating systems, patching, scaling, etc.    
You can use Lambda in the following ways:    
- As an **event-driven compute service** where AWS Lambda runs your code in response to events.  These events could be changes to data in an Amazon S3 bucket or an Amazon DynamoDB table.   
- As a **compute service** to run your code in response to HTTP requests using Amazon API Gateway or API calls made using AWS SDKs.   
### Language Support  
- Node.js  
- Java  
- Python  
- C#   
- Go   
### Pricing 
Based on number of requests:    
- First 1MM requests are free, $0.20 per 1MM requests thereafter    
- Duration: calculaed from teh time your code begins executing until it returns or otherwise terminates, rounded up to the nearest 100ms.  The price depends on teh amount of memory you allocate to your function.  You are charged $0.00001667 for every GB-second used.   
## Exam Tips   
- Lambda scales out (not up) automatically   
- Lambda functions are independent, 1 event = 1 function   
- Lambda is serverless   
- Know what services are serverless   
- Lambda functions can trigger other lambda functions, 1 event can = x functions if functions trigger other functions   
- Architectures can get extremely complicated, ***AWS X-ray*** allows you to debut what is happening   
- Lambda can do things globally, you can use it to back up S3 buckets to other S3 buckets, etc.    
- Know the Lambda triggers   
# API Gateway   
An **API** is an Application Programming Interface.    
Types of APIs:   
- REST APIs (**RE**presentational **S**tate **T**ransfer)   
  - Uses JSON     
- SOAP APIs (**S**imple **O**bject **A**ccess **P**rotocol)    
  - Uses XML   
**Amazon API Gateway** is a fully managed service that makes it easy for developers to publish, maintain, monitor
and secure APIs at any scale.  With a few clicks in teh AWS Management Console, you can create an API that acts as a 
"front door" for applications to access data, business logic, or functionality form your back-end services, such as 
applications running on Amazon Elastic Compute Cloud (Amazon EC2), code running on AWS Lambda, or any web application.    

