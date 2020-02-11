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
### What does API Gateway Do?    
- Exposes HTTPS endpoints to define a RESTful API    
- Serverless-ly connect to services like Lambda & DynamoDB  
- Send each API endpoint to a different target  
- Run efficiently with low cost     
- Scale effortlessly  
- Track and control usage by API key   
- Throttle requests to prevent attacks  
- Connect to CloudWatch to log all requests for monitoring   
- Maintain multiple versions of yoru API   
### Configure API Gateway  
- Define an API (container)   
- Define Resources and nested Resources (URL paths)   
- For each resource:    
  - Select supported HTTP methods (verbs)  
  - Set security   
  - Choose target (such as EC2, Lambda, DynamoDB, etc.)   
  - Set request and response transformations    
- Deploy API to a Stage:  
  - Uses API Gateway domain, by default   
  - Can use custom domain   
  - Now supports AWS Certificate Manager: free SSL/TLS certs!     
### What is API Caching?  
With Caching, you can reduce the number of calls made you your endpoint and also imporve the latency of the requests to your API.  When you enable caching for a stage, API Gateway caches responses from your endpoint for a specified time-to-live (TTL) period, in seconds.  API Gateway then reponds to the request by looking up teh endpoint response from the cache instead of making a request to your endpoint.    
### Same Origin Policy   
In computing, the **same-origin policy** is an importatn concept in the web application security model.  Under the policy,  a web browser permits scripts contained in a first webpage to access data in a second web page, but only if both web pages have the same origin.   

This is done to prevent *Cross-Site Scripting* (XSS) atttacks.   
- Enforced by web browsers     
- Ignored by tools like PostMan and curl    
### Cross-Origin Resource Sharing (CORS)  
CORS is the way the server at the other end (not the client code in the browser) can relax the same-origin policy.   
CORS is a mechanism that allows restricted resources (e.g. fonts on a web page to be requested from aonther domain outside the domain from which the first resource was served.   
- Browser makes an HTTP OPTIONS call for a URL   
  - OPTIONS is an HTTP method like GET, PUT and POST  
- Server returns a response that says: `These other domains are approved to GET this URL`
- Error - `Origin poliocy cannot be read at the remote resource?`
  - Need to enable CORS on API Gateway    
## Examp Tips   
- Remeber what API Gateway is at a high level   
- API Gateway has caching capabilities to increase performance   
- API Gateway is low cost and scales automatically   
- You can throttle API Gateway to prevent attacks  
- You can log results to CloudWatch   
- If you are using JavaScript/AJAX that uses multiple domains with API Gateway, ensure that you enable CORS on API Gateway   
- CORS is enforced by the client   
# Version Control With Lambda   
## Versioning  
When you use versioning in AWS Lambda, you can publish one or more verions of your Lambda function.  As a result, you can work with different variations of your Lambda function in your development workflow, such as development, beta and production.   
Each Lambda function version has a unique Amazon Resource Name (ARN).  After you publish a version, it is immutable (that it, it can not be changed).  
AWS Lambda maintains your latest function code in the $LATEST version.  When you update your function code, AWS Lambda replaces the code in teh $LATEST version of the Lambda function.    
### Qualified / Unqualified ARNs   
You can refer to this function using ARN.  There are two ARNS associated with this initial version:    
- Qualified ARN: The function ARN with teh version suffix.
  - arn:aws:lambda:aws-region-acct-id:function:helloworld:$LATEST  
- Unqualified ARN - The function ARN without the version suffix.  
  - arn:aws:lambda:aws-region:acct-id:function:helloworld   
### Alias  
After initially create a Lambda function (the $LATET versin), you can publish a version 1 of it.  By creating an alias named PROD that poins to version 1, you can now use the PROD alias to invoke version 1 of the Lambda funciton.    
Now, you can update the code (the $LATEST version) with all of your improvements, and then publish another stable and improved version (version 2).  You can promote version 2 to production by remapping the PROD alias so that it points to version 2.  If you find something wrong, you can easily roll back that production version to version 1 by remapping the PROD alias so that it points to version 1.  
## Exam Tips  
- Can have multiple version of lambda functions    
- Latest version will use $LATEST   
- Qualified verions will use $LATEST, unqualified will not have it   
- Versions are immutable (can not be changed)   
- Can split traffic using aliases to different versions   
- Can not split traffic with $LATEST, instead create an alias to latest
# Step Functions   
**Step Functions:** 
- Allows you to visualize and test your serverless applications   
- Provides a graphical console to arrange and visualize the components of your application as a series of steps.  This makes it simple to build and run multistep applications.   
- Automatically triggers and tracks each step, and retries when there are errors, so your application executes in order and as expected.   
- Logs the state of each step, so when things do go wrong, you can diagnose and debug problems quickly. 
## Exam Tips   
- Great way to visualize your serverless application   
- Automatically triggers and tracks each step    
- Logs the state of each step so if something goes wrong you can track what went wrong and where   
# AWS X-Ray   
**AWS X-RAY** is a service that collects data about requests that your application serves, and provides tools you can use to view, filter and gain insights into that data to identify issues and opportunities for optimization.  For any traced request to your application, you can see detailed information not only about the request and response, but also about calls that your application makes to downstream AWS resources, microservices, databases and HTTP web APIs.     
### X-Ray SDK    
The X-Ray SDK provides: 
- Interceptors to add to your code to trace incoming HTTP requests   
- Client handlers to instrument AWS SDK clients that your application uses to call other AWS services   
- An HTTP client to use to instrument calls to other internal and external HTTP web services    
### X-Ray Integration   
The X-Ray integraes with the following AWS services:    
- Elastic Load Balancing  
- AWS Lambda   
- Amazon API Gateway   
- Amazon Elastic Cloud Compute   
- AWS Elastic Beanstalk   
### X-Ray Languages   
- Java  
- Go   
- Node.js   
- Python   
- Ruby   
- .Net    
# Advanced API Gateway   
You can use the **API Gateway Import** API feature to import an API from an external definition file into API Gateway.  Currently, the Import API feature supports **Swagger v2.0** definition files.    

With the Import API, you can either create a ne2 APII by submitting an POST request that includes a Swagger definition in the payload and endpoint configurate, or you can update an existing API by using a PUT request that contains a Swagger definition in the payload.  You can update an API by overwriting it with a new definition, or merge a definition with an existing API.  You specifiy the options using a mode query parameter in the requst URL.   
## API Throttling   
By default, API Gateway limits the steady-state request rate to **10,000 requests per second** (rps).   
The maximum concurrent requests is 5000 across all APIs within an AWS account.    
If you go over 10,000 requests per second or 5000 concurrent requests you will receive a **429 Too Many Requests** error response.   
## SOAP Webservice Passthrough   
You can configure API Gateway as a SOAP web service passthrough.    

