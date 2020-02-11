# Web Identity Federation      
**Web Identity Federation** lets you give your users access to AWS resources after they have successfully authenticated with a web-based identity provier like Amazon, Facebook or Google.  
Following successful authentication, the user receives an authentication code from the Web ID provider, which they can trade for temporary AWS security credentials.        
### Amazon Cognito     
**Amazon Cognito** provides Web Identity Federation with the following features:      
- Sign-up and sign-in to your aps     
- Access for guest users     
- Acts as an Identity Broker between your application and Web ID providers, so you don't need to write any additional code     
- Synchronizes user data for multiple devices     
- Recommended for all mobile applications AWS services     
### Use Cases     
The recommended approach for Web Identiy Federation using social media accounts like Facebook.   
Cognito brokers between the app and Facebook or Google to provide tep creds which map to an IAM rol allowing access to the required resources.      
No need for the application to embed or store AWS credentials locally on the device - it gives the users a seamless experience across all mobile devices.   
# Cognito User Pools     
**User Pools** are user directories used to manage sign-up and sign-in functionality for mobile and web applications.   
Users can sign-in directly to the User Pool, or indirectly via an identity provider like Facebook, Amazon or Google.  Cognito acts as an Identity Broker between the ID providers and AWS.  Successful authentication generates a number of JSON Web tokens (JWTs).   
**Identity Pools** enables you to create unique identities for your users and authenticate them with identity providers.  With an identity, you can obtain temporary, limited-privilege AWS credentials to access other AWS services.        
### Push Synchronization      
Cognito tracks the association between user identity and the various different devices they sign-in from.      
In order to provice a seamless user experience for your application, Cognito uses **Push Synchronization** to push updates and synchronizes user data accross multiple devices.       
Amazon SNS is used to send a silent push notification to all the devices associated with a given user identity whenever data stored in the cloud changes.        
## Exam Tips     
- Cognito uses User Pools to manage user sign-up and sign-in directly or via Web Identity Providers      
- Cognito acts as an Identity broker, handling all interaction with Web Identity Providers     
- Cognito uses Push Synchronization to send a silent push notification of user data updates to multiple device types associated with a user ID      
# Inline Policies vs. Managed Policies vs. Custom Policies     
IAM is used to define user acess permissions with AWS.  
There are three different types of IAM policies available:      
**Managed Policies**   
- An IAM policy which is created and admninistered by AWS.  
- AWS provide Managed Policies for common use cases based on job function - e.g. AmazonDynamoDBFullAccess, AWSCodeCommitPowerUser, AmazonEC2ReadOnlyAccess, etc.      
- These AWS-provided policies allow you to assign appropriate permissions to your users, groups and roles wihtout having to write the policy yourself.    
- A single Managed Policy can be attached to multiple users, groups or roles within the same AWS account and accross different accounts.      
- You cannot change the permissions defined in an AWS Managed Policy  

**Customer Managed Policies**    
- A standalone policy that you create and administer inside of your own AWS account     
- You can attach this policy to multiple users, groups and roles - but only within your own account     
- In order to create a Customer Managed Policy, you copy an existing AWS Managed Policy and customize it to fit the requirements of your organization     
- Recommended for use cases where the existing AWS Managed Policies don't meet the needs of your env     

**Inline Policies**     
- A policy which is actually emvbedded within the user group or role to which it applies.  There is a strict 1:1 relationship between the entity and the policy     
- When you delete the user, group or role in which the inline policy is embedded, the policy will also be deleted     
- In most cases, AWS recommends using Managed Policies over Inline Policies     
- Inline Policies are useful when you want to be sure that the permissions in a policy are not inadvertently assigned to any other user, group or role than the one for which they're intended - i.e. you are creating a policy that must only ever be attached to a single user, group or role)     
# STS: AssumedRoleWithWebIdentity      
`assume-role-with-web-identity` is an API provided by STS (Secure Token Service)     
- Returns temp creds for usres authenticated by a mobile or web application or using a Web ID Provider like Amazon, Facebook or Google     
- For mobile applications, Cognito is recommended      
- Regular web applications can use the STS: `assume-role-with-web-identity` API     
## Exam Tips      
- Part of the Security Token Service     
- Allows users who have authenticated with a Web Identity provider to access AWS resources     
- Once the user has authenticated, teh application makes the assume-role-with-web-identty API call     
- If successful, STS will return temp creds enabling access to AWS     
- AssumedRoleUser ARN and AssumedRoleID - used to programatically reference the temp creds - not an IAM role or user 
# Cross Account Access     
### What is Cross Account Access?      
Many AWS customers use separate AWS accounts for their dev and prod resources.  This separation allows them to cleanly separate different types of resources and can also provide some security benefits.    
Cross account access makes it easier for you to work productively within a multi-accout (or multi-role) AWS env by making it easy to switch roles within the AWS Mgmt Console.  
You can sign in to the console using your IAM user name then switch the console to manage another account without having to enter (or remember) another user name or password.     
### Steps     
- Identify our account numbers     
- Create a group in IAM - Dev     
- Create a user in IAM - Dev     
- Log in to Production     
- Create the `read-write-app-bucket` policy     
- Create the `UpdateApp` Cross Account Role     
- Apply the newly created policy to the role     
- Log into the Dev account     
- Create a new inline policy     
- Apply it to the Dev group     
- Login as John     
- Switch Accounts      







