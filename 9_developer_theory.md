# What is CI/CD?      
**Continuous Integration & Continuous Delivery/Deployment**      
- CI & CD are Best Practices for software development and deployment      
- They enable frequent software changes to be applied whilst maintaining system and service stability      
- Companies like AWS, Netflix, Google and Facebook have pioneered this approach to release code, successfully applying thousands of changes per day      
### Continuous Integration Workflow      
**1: Code Repo**      
- Multiple developers working on different features or bugs fixes      
- All contributing to the same application       
- Sharing the same code repo (e.g. git)      
- Frequently pushing their updates into the shared repo - at least daily    
**2: Build Management System**
- Code repo integrated with a build mgmt system      
- Code changes trigger an automated build      
- We need a way to ensure that any code changes does not break the build or introduce new bugs into the application     
**3: Test Framework**      
- The test system runs automated tests on the newly built application       
- Identifies any bugs, preventing issues from being introduced in the master code      
- CI focuses on small code changes which frequently commmitted into the main repo once they have been successfully tested      
### Continuous Delivery/Deployment      
- CD can mean either Continuous Delivery or Deployment      
- Continuous Delivery is a Deployment practice where merged changes are automatically built, tested and prepard for release into staging and eventually production environments      
- There is usually a manual decision process to initiate deployment of the new code      
- Continuous Deployment takes the idea of automation one step further and automatically deploys the new code following successful testing, eliminating any manual steps      
- The new code is automatically released as soon as it passes through the stages of your release process (build, test, package)      
- Small changes are released early and frequently      
- Both practices require build, test and deployment processes to be fully automated but Continuous Deployment also automates the release process as well      
## Exam Tips      
- Read the white paper (https://d0.awsstatic.com/whitepapers/DevOps/practicing-continuous-integration-continuous-delivery-on-AWS.pdf)        
- AWS CodeCommit = Source Control service (git)        
- AWS CodeBuild = Compile soure doce, run tests and package code        
- AWS CodeDeploy = Automated Deployment to EC2, on prem systems and Lambda        
- AWS CodePipeline = CI/CD workflow tool, fully automates the entire release process (build, test, deploy)         
# CodeCommit 101        
- Fully managed Source Control service that enables companies to host secure and highly scalable private Git repos        
- Git is an industry-standard Open Source distributed source control system         
  - Centralized repo for all your code, binaries, images and libraries        
  - Tracks and manages code changes        
  - Maintains version history         
  - Manages updates from multiple sources        
  - Enables collaboration         
### Processes        
- Users create a copy (known as a branch) of the master repo, which they can update independently without imacting other users         
- Saved code changes which are ready to be applied to a repo are know as a **commit**        
- When the updated code located in a branch is ready to be added to the master repo, the branch is then merged into the master repo        
- AWS CodeCommit provides all the functionality of Git and you can use Git on your local machine to interact with your CodeCommit repo        
- Your data is encrypted in transit and at rest        
# CodeDeploy 101        
- Automated deployment sercie which allows you to deploy yoru application code automtcially to EC2 instances, on-prem systems and Lambda functions        
- Allows you to quickly release new features, avoid downtime during application deployments and avoid the risks associated with manual processes        
- Automatically scales with yoru infrasturcture and integrates with various CI/CD tools e.g. Jenkins, GitHub, Atlassian, AWS CodePipeline as well as config management tools like Ansible, Puppet and Chef        
- Two deployment approaches available:         
  - In-Place 
    - The application is stopped on each instance and the latest revision installed        
    - The instances is out of service during this time and your capacity will be reduced        
    - If the instances are behind a load balancer, you can configure the load balancer to stop sending requests to the instances which are being upgraded        
    - AKA Rolling Update        
    - Only available for EC2 and on-prem systems - Not supported for Lambda        
    - If you need to roll back your changes, the previous version of the application will need to be re-deployed        
  - Blue/Green        
    - New instances are provisioned and the latest revision is installed on the new instances.  Blue represents the active deployment and green is the new release        
    - The new instandces are registered with an Elastic Load Balancer, traffic is then routed to the new instances and the original instances are evntually terminated        
    - Advantages of a Blue/Green deployment are: 
      - New instances can be created ahead of the time        
      - Code released to production by simply switching all traffic to new servers
    - Switching back to the original env is faster and more reliable and is just a case of routing the traffic back to the original servers (as long as you haven't already terminated them)         
### AWS CodeDeploy Terminology     
**Deployment Group** - A set of EC2 instances or Lambda functions to which a new revision of the software is to be deployed     
**Deployment** - The process and components used to apply a new revision     
**Deployment Configuration** - A set of deploiyment rules as well as success / failure conditions used during a deployment     
**AppSepc File** - Defines the deployment actions you want AWS CodeDeploy to execute     
**Revision** - Everything needed to deploy the new versino: AppSepc file, application files, executables, config files     
**Application** - Unique identifier for the application you want to deploy.  To ensure the correct combination of revision, deployment configuration and deployment group are referenced during a deployment     
## Exam Tips     
**AWS CodeDeploy** is a fully managed automated deployment service and can be used as part of a CD process.       
Two types of deployment approaches:      
- **In-Place or Rolling update** - you stop the application on each host and deploy the latest code. EC2 and on premise systems sonly.  To roll back you must re-deploy the previous version of the application.   
- **Blue / Green** - New instances are provisioned and the new application is deployed to these new instances.  Traffic is routed to the new instances according to your own schedule.  Supported for EC2, on-premise systems and Lambda functions.   Roll back is easy, just route the traffic back to the original instances.
  - *Blue* is the active deployment     
  - *Green* is the new release     
# CodePipeline 101 Hi, I don't have a kit for you you would need to take one of our projects as a starter which I do not have access to right now, i would say around 2 weeks to get started with the stack by the time you request vitalize id, siteminder id and so on for a basic project
**AWS CodePipeline** is a fully managed CI/CD service.  Hi, I don't have a kit for you you would need to take one of our projects as a starter which I do not have access to right now, i would say around 2 weeks to get started with the stack by the time you request vitalize id, siteminder id and so on for a basic project
CodePipeline can orchestrate the build, test and deployment of your appliction every time there is a change to your code - all based on a user devinded software release process.   Hi, I don't have a kit for you you would need to take one of our projects as a starter which I do not have access to right now, i would say around 2 weeks to get started with the stack by the time you request vitalize id, siteminder id and so on for a basic project
Traditional, manual approaches to code delivery can be slow and prone to errors, whereas an automated process allows developers to grequently release new features and bug fixes in a fast and reliable way.   Hi, I don't have a kit for you you would need to take one of our projects as a starter which I do not have access to right now, i would say around 2 weeks to get started with the stack by the time you request vitalize id, siteminder id and so on for a basic project
### Simple WorkflowHi, I don't have a kit for you you would need to take one of our projects as a starter which I do not have access to right now, i would say around 2 weeks to get started with the stack by the time you request vitalize id, siteminder id and so on for a basic project
CodePipeline allows you to model your release process as a workfow or pipeline made up of different tasks, such as the simple workflow represented below:   

`code update -> build --> test --> deploy`     

You define what happens and where for each of the different stages of the workflow and this can be modelled using the CodePipeline GUI or CLI.
Integraes with CodeCommit, CodeBuild, CodeDeploy, Lambda, Elastic Beanstalk, CloudFormation, Elastic Container Service as well as third party tools like Github and Jenkins.      
Every code change pushed to your code repo automatically enters the workflow and triggers the set of actions defined for each stage of the pipeline.       
The pipeline automatically stops if one of the stages fails.  For example, if one of your automated unit tests fails.  This means that buges are caught before the code is deployed while they are still easy to fix.   
# Advanced CodeDeploy: The AppSpec File     
### AppSpec File - Lambda Deployments     
**The AppSpec File** is used to define the parameters that will be used for a CodeDeploy deployment.  The file structure depends on whether you are deploying to Lambda or EC2/On Prem.       
For Lambda deployments, the AppSpec File may be written in YAML or JSON and contains the following fields:      
- **version**: Reserved for furture use - currently the only allowed value is 0.0     
- **resources**: The name and properties of the Lambda function to deploy      
- **hooks**: Specifies Lambda functions to run at set points in the deployment lifecycle to validate the deployment - e.g. validation tests to run before allowing traffic to be sent to your nerwly deployed instances      
#### AppSpec File - Hooks - Lambda       
The following Hooks are available for use:        
**BeforeAllowTraffic**: used to specifiy the tasks or functions you want to run before traffic is routed to the newly deployed Lambda function - e.g. test to validate that the function is deployed correctly.  
**AfterAllowTraffic**: used to specify the tasks or functions you want to run after the traffic is routed to the newly deployed Lambda function - e.g. test to validate that the function is accepting traffic correctly and behaving as expected.   
### AppSpec File - Hooks - EC2 and On Prem      
**version**: Reserved for future use - currently the only allowed value is 0.0      
**os**: The operating system version you are using, e.g. linux, windows      
**files**: The location of any application files that need to be copied and where they should be copied to (source and destination folders).       
**hooks**: Lifecycle event hooks allow you to specify scripts that need to run at set points in the deployment lifecycle (e.g. to unzip application files prior to deployment, run functional tests on the newly deployed application, and to de-register and re-register instances with a load balancer.)    
The appsec.yml file must be placed in the **root of the directory of your revision**.  This is the directory containing your application source code, otherwise the deployment will fail.  
#### AppSpec File - Supported Hooks for EC2 and On Prem   
***THE RUN ORDER OF HOOKS***     
##### The Deregister Block     
**BeforeBlockTraffic**: Run tasks on instances beofre they are degregistered from a load balander     
**BlockTraffic**: Deregister instances from a load balancer     
**AfterBlockTraffic**: Run tasks on instances after they are Deregistered from a load balancer   
##### The Upgrade Block     
**ApplicationStop**: Gracefully stop the application in preparation for deploying the new revision     
**DownloadBundle**: The CodeDeploy agent copies the application revision files to a temp location     
**BeforeInstall**: Details of any pre-installation scripts, e.g. backing up the current version, decrypting files     
**Install**: The CodeDeploy agent copies the application revision files from their temporary location to their correct location      
**AfterInstall**: Details of any post-installation scripts - e.g. configuration tasks, change file permissions     
**ApplicationStart**: Restarts any services that were stopped during ApplicationStop     
**ValidateService**: Details of any tests to validate the service  
##### Load Balancer Reregistration 
**BeforeAllowTraffic**: Run tasks on instances before they are registered with a load balancer     
**AllowTraffic**: Register instances with a load balancer     
**AfterAllowTraffic**: Run tasks on instances after they are registered with a load balancer     
## Exam Tips     
- The AppSpec file defines all the parameters needed for the deployment - e.g. location of application files and pre/post deployment validation tests to run      
- For EC2/On Prem systems, the appspec.yml file must be placed in the root directory of your revision (the same folder that contains your application code).  Written in YAML     
- Lambda supports YAML or JSON      
- Know **run order of hooks**     
# Docker and CodeBuild Lab     
 - **Docker** is an Open Source technology which allows you to create applications based on either Linux or Windows containers     
- A container is a light weight standalong executable software package which includes everything the software needs to run code, runtime env, libraries, env settings, etc.      
- AWS provides **Elastic Container Services** as a fully managed clustered platform which allows you to run your Docker images in the cloud     
- **AWS CodeBuild** is a fully managed build service which runs a set of commands that you define - e.g. compiles code, runs tests and produces artifacts thatr are ready to deploy     
## Summary and Exam Tips     
- Docker commands to build, tag (applies an alias) and push your Docker image to the ECR repo     
  Build: `docker build -t {name_of_image_repo}`
  Tag: `docker tag {name_of_image_repo}:latext ...`
  Push: `docker push .../{name_of_image_repo}:latest`
- Use buildspec.yml to define the build commands and settings used by CodeBuild to run your build     
- You can override the settings in buildspec.yml by adding your own commands in the console when you launch the build     
- If youre build fails, check the build logs in the CodeBuild console and you can also view the full CodeBuild log in CloudWatch     
# Introduction to CloudFormation     
**CloudFormation** is a service that allows you to manage, configure and provision your AWS infrastructure as code.   
- Resources are defined using a CloudFormation template     
- CloudFormation interprets the template and makes the appropriate API calls to create the resources you have defined     
- Supports YAML or JSON     
### CloudFormation Benefits     
- Infrastructure is provisioned consistently, with fewer mistakes     
- Less time and effort than configuring things manually     
- You can version control and peer review your templates     
- Free to use (charged for what you create)      
- Can be used to manage updates & dependencies     
- Can be used to rollback and delete the entire stack as well     
### CloudFormation Template     
- YAML or JSON template used to describe the endstate of the infrastructure you are either provisioning or changing     
- After creating the template, you upload it to CloudFormation using S3     
- CloudFormation reads the template and makes the API calls on your behalf     
- The resulting resources are called a Stack     
- *Resources* is the only mandatory section of the CloudFormation template     
- *Transform* section is used to reference additional code stored in S3, allowing for code re-use, e.g. for Lambda code or tempolate snippets / reusable pieces of CloudFormation code     
## Exam Tips      
- **CloudFormatin** allows you to manage, configure and provision AWS infrastructure as code (YAML/JSON)     
- Main sections of CloudFormation Template:      
  - Parameters - input custom values     
  - Conditions - e.g. provision resources based on env     
  - Resources (**mandatory**) - the AWS resources to create      
  - Mappings - create custom mappings like Region:AMI     
  - Transforms - reference code located in S3 - e.g. Lambda code or reusable snippets of CloudFormation code     
# Serverless Application Model (SAM)      
**Serverless Application Model (SAM)** is an extension to CloudFormation used to define serverless applications     
- Simplified syntax for defining serverless resources: APIs, Lambda Functions, DynamoDB Tables, etc     
- Use the SAM CLI to package your deployment code, upload it to S3 and deploy your serverless application     
### SAM CLI Commands     
`sam package`
  - input = yml template      
  - output = sam compatable template     
  - uploads deployment pkg to specified S3 bucket     
`sam deploy`    
  - input = sam template
  - specifies name of stack     
  - capabilities parameter --> IAM role
## Exam Tips     
- SAM == Serverless Application Model 
- Allows you to define and provision serverless applications using CloudFormation      
- Uses the SAM CLI commands to package and deploy:      
  - `sam package` - packages your application and uploads to S3     
  - `sam deploy` - deploys your serverless app using CloudFormation     
# CloudFormation Nested Stacks     
**Nested Stacks** allow re-use of CloudFormation code for common use cases - e.g. standard configuration for a load balancer, web server, application server, etc     
Instead of copying out the code each time, create a standard template for each common use case and reference from within your CloudFormation template     
### CloudFormation Template Structure - Nested Stack     
Resources: 
  Type: AWS::CloudFormation::Stack     
    Notification: 
    Parameters: 
    Tags
    **TemplateURL: https://s3.amazonaws.com/.../template.yaml**
    TimeoutinMinutes: Integer     
***Must have a TemplateURL location -- Mandatory***     
## Exam Tips     
- Useful for frequently used configurations - e.g. for load balancers, web or application servers     
- Simply create a CloudFormation template, store it in S3 and you can reference it in the Resources section of any Cloudformation using the **Stack** resource type     





