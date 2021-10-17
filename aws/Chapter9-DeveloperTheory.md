# CI/CD

## What is CI/CD?

* Software Development Best Practice: Continuous Integration, Continuous Delivery / Deployment.
* Make Small Changes & Automate Everything! Small, incremental code changes. Automate as much as possible e.g., code integration, build, test and deployment.
* Why is it so cool? Modern companies like AWS, Netflix, Google and Facebook have pioneered this approach to releasing code, successfully applying thousands of code changes per day.

## Benefits of the CI/CD Approach

Automation Is Good! Fast, repeatable, scalable, enables rapid deployment.

Manual is Bad! Slow, error prone, inconsistent, unscalable, complex.

Small Changes. Test each code change and catch bugs while they are small and simple to fix.

## Continuous Integration Workflow

Shared Code Repository. Multiple developers contributing to a shared code repository like Git. Frequently merging or integrating code updates.

Automated Build. When changes appear in the code repository this triggers an automated build of the new code.

Automated Test. Run automated test to check the code locally before it is committed into the master code repository.

## Continuous Delivery & Deployment Workflow

Code is Merged. After successful tests, the code gets merged to the master repository.

Prepared for Deployment. Code is built, tested and packaged for deployment.

Manual Decision. Humans may be involved in the decision to deploy the code. This is known as Continuous Delivery.

Or Fully Automated. The system automatically deploys the new code as soon as it has been prepared for deployment. This is known as Continuous Deployment.

## AWS Developer Tools

### CodeCommit

Source & Version Control. Source control service enabling teams to collaborate on code, html pages, scripts, images and binaries.

### CodeBuild.

Automated build. Compiles source code, runs tests and produces packages that are ready to deploy.

### CodeDeploy.

Automated deployment. Automates code deployments to any instance, including EC2, Lambda and on-premises.

### CodePipeline.

Manages the workflow. End-to-end solution, build, test, and deploy your application every time there is a code change.

## CI/CD Exam tips

1. Continuous Integration. Integrating or merging the code changes frequently - at least once per day. Think CodeCommit.
2. Continuous Delivery. Automating the build, test and deployment functions. Think CodeBuild and CodeDeploy.
3. Continuous Deployment. Fully automated release process, code is deployed into Staging or Production as soon it has successfully passed through the release pipeline. Think CodePipeline.

AWS White-paper: [Practicing Continuous Integration & Continuous Deployment on AWS](https://d0.awsstatic.com/whitepapers/DevOps/practicing-continuous-integration-continuous-delivery-on-AWS.pdf)

# CodeCommit 101 Exam Tips

1. Centralized Code Repository. A place to store source code, binaries, libraries, images, HTML files etc. Based on Git.
2. Enables Collaboration. Manages updates from multiple users.
3. Version Control. Tracks and manages code changes. Maintains version history.

# CodeDeploy 101 Exam Tips

Know the difference!

In-Place
* Capacity is reduced during the deployment
* Lambda is not supported
* Rolling back involves a re-deploy
* Great when deploying the first time

Blue/Green
* No capacity reduction
* Green instances can be created ahead of time
* Easy to switch between old and new
* You pay for 2 environments until you terminate the old servers
* Safest Option for Production Environment

# CodeDeploy using the AppSpec File Exam Tips

* Configuration File. Defines the parameters to be used by CodeDeploy e.g., OS, files, hooks.
* `appspec.yml`. Should be saved to the root of your revision.
* Hooks. Lifecycle event hooks have a very specific run order.

# CodeDeploy Lifecycle Event Hooks Exam Tips

* Run Order. Lifecycle event hooks are run in a specific order known as the Run Order.
* In-Place Deployment. Broadly 3 phases: de-registering, installation, re-registering with a LB.
* Logical Flow.

# CodePipeline 101 Exam Tips

1. CI/CD service. Orchestrates your end-to-end software release process based on a workflow you define.
2. Automated. Automatically triggers your pipeline as soon as a change is detected in your source code repository.
3. Integrates with AWS & Third-Party Tools.

# Elastic Container Service Exam Tips

* Containers. Virtual operating environment with everything the software needs to run. Includes libraries, tools, code, and runtime. Allows applications to be built using independent stateless components or micro-services running in multiple containers.
* ECS. Container orchestration. ECS will run your containers on clusters of virtual machines.
* Fargate. Serverless. You don't need to worry about the underlying EC2 instances!
* EC2. More control. If you want to control the installation, configuration and management of your compute environment.
* ECR. Container registry. This is where you can store your container images. Docker or Windows Container.

# Docker and CodeBuild Exam Tips

* Docker commands to build, tag and push your Docker image to the ECR repository
* Use buildspec.yml to define the build commands and settings used by CodeBuild to run your build
* You can override the settings in buildspec.yml by adding your own commands in the console when you launch the build
* If your build fails, check the build logs in the CodeBuild console and you can also view the full CodeBuild log in CloudWatch

# Introduction to CloudFormation Exam Tips

* CloudFormation allows you to manage, configure and provision AWS infrastructure as code. (YAML / JSON)
* Remember the main sections in the CloudFormation template:
* Parameters - input custom values
* Conditions - e.g. provision resources based on environment
* Resources - mandatory - the AWS resources to create
* Mappings - create custom mappings like Region : AMI
* Transforms - reference code located in S3 e.g. lambda code or reusable snippets of CloudFormation code

# Serverless Application Model (SAM)

* SAM is the Serverless Application Model (SAM).
* Allows you to define and provision serverless applications using CloudFormation.
* Uses the SAM CLI commands to package and deploy:
** `sam package` - packages your application and uploads to S3
** `sam deploy` - deploys your serverless app using CloudFormation

# CloudFormation Nested Stacks

* Nested stacks allow re-use of CloudFormation code for common use cases.
* e.g. standard configuration for a load balancer, web server, application server, etc.
* Instead of copying out the code each time, create a standard template for each common use case and reference from within your CloudFormation template.

## CloudFormation Nested Stacks Exam tips

* Nested stacks allow you to re-use your CloudFormation code so you don't need to copy / paste every time.
* Really useful for frequently used configurations, e.g. for load balancers, web or application servers
* Simply create a CloudFormation template, store it in S3 and you can reference it later in the Resources section of any CloudFormation template using the Stack resource type.

# Deployment content

[Practicing Continuous Integration and Continuous Delivery on AWS](https://d0.awsstatic.com/whitepapers/DevOps/practicing-continuous-integration-continuous-delivery-on-AWS.pdf)

[Blue/Green deployments on AWS](https://d0.awsstatic.com/whitepapers/AWS_Blue_Green_Deployments.pdf)