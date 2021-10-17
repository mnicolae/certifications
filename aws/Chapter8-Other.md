# SQS

Amazon SQS is a web service that gives you access to a message queue that can be used to store messages while waiting for a computer to process them.

Amazon SQS is a distributed queue system that enables web service applications to quickly and reliably queue messages that one component in the application generates to be consumed by another component; A queue is a temporary repository for messages that are awaiting processing.

## What is SQS?

Using Amazon SQS, you can decouple the components of an application so they run independently, easing message management between components.

Any component of a distributed application can store messages in the queue. Messages can contain up to 256 KB of text in any format. Any component can later retrieve the messages programmatically using the Amazon SQS API.

The queue acts as a buffer between the component producing and saving data, and the component receiving the data for processing. This means the queue resolves issues that arise if the producer is producing work faster than the consumer can process it, or if the producer or consumer are only intermittently connected to the network.

## Queue types

* Standard Queues (standard)

Amazon SQS offers standard as the default queue type. A standard queue lets you have a nearly-unlimited number of transactions per second. Standard queues guarantee that a message is delivered at least once. However, occasionally (because of the highly-distributed architecture that allows high throughput), more than one copy of a message might be delivered out of order. Standard queues provide best-effort ordering which ensures that messages are generally delivered in the same order as they are sent.

* FIFO Queues

The FIFO queue complements the standard queue. The most important features of this queue type are FIFO delivery and exactly-once processing: the order in which the messages are received and sent is strictly preserved and a message is delivered once and remains available until a consumer processes and deletes it; duplicates are not introduced into the queue. FIFO queues also support message groups that allow multiple ordered message groups within a single queue. FIFO queues are limited to 300 transactions per second (TPS), but have all the capabilities of standard queues.

## SQS Key Facts

* SQS is pull-based, not pushed-based
* Messages are 256 KB in size
* Message can be kept in the queue from 1 minute to 14 days
* Default retention period is 4 days
* SQS guarantees that your messages will be processed at least once

## SQS Visibility Timeout

* The Visibility Timeout is the amount of time that the message is invisible in the SQS queue after a reader picks up that message. Provided the job is processed before the visibility timeout expires, the message will then be deleted from the queue. If the job is not processed within that time, the message will become available again and another reader will process it. This could result in the same message being delivered twice.
* Default visibility timeout is 30 seconds
* Increase it if your task takes > 30 seconds
* Maximum is 12 hours

## SQS Long Polling

* Amazon SQS long polling is a way to retrieve messages from your Amazon SQS queues.
* While the regular short polling returns immediately (even if that message queue being polled is empty), long polling doesn't return a response until a message arrives in the message queue, or the long poll times out.
* As such, long polling can save you money.

## SQS Exam Tips

* SQS is a distributed message queueing system
* Allows you to decouple the components of an application so that they are independent
* Pull-based, not push-based
* Standard Queues (default) - best-effort ordering: message delivered at least once
* FIFO Queues (First In First Out) - ordering strictly preserved, message delivered once, no duplicates. e.g., good for banking transactions which need to happen in strict order.
* Visibility Timeout. Default is 30 seconds - increase if your task takes > 30s to complete. Max 12 hours.
* Short polling - returned immediately even if no messages are in the queue.
* Long polling - polls the queue periodically and only returns a response when a message is in the queue or the timeout is reached.

# Simple Notification Service

## What is SNS?

* Amazon Simple Notification Service (Amazon SNS) is a web service that makes it easy to set up, operate, and send notifications from the cloud.
* It provides developers with a highly scalable, flexible, and cost-effective capability to publish messages from an application and immediately deliver them to subscribers or other applications.
* Push notifications to Apple, Google, Fire OS, and Windows devices, as well as Android devices in China with Baidu Cloud Push.
* Besides pushing cloud notifications directly to mobile devices, Amazon SNS can also deliver notifications by SMS text message or email to Amazon Simple Queue Service (SQS) queues, or to any HTTP endpoint.
* SNS notifications can also trigger Lambda functions: When a message is published to an SNS topic that has a Lambda function subscribed to it, the Lambda function is invoked with the payload of the published message. The Lambda function receives the message payload as an input parameter and can manipulate the information in the message, publish the message to another SNS topic, or send the message to other AWS services.

## SNS Topics

SNS allows you to group multiple recipients using topics. A topic is an "access point" for allowing recipients to dynamically subscribe for identical copies of the same notifications.

One topic can support deliveries to multiple endpoint types - for example, you can group together iOS, Android and SMS recipients. When you publish once to a topic, SNS delivers appropriately formatted copies of your message to each subscriber.

To prevent messages from being lost, all messages published to Amazon SNS are stored redundantly across multiple availability zones.

## SNS Benefits

* Instantaneous, push-based delivery (no polling)
* Simple APIs and easy integration with applications
* Flexible message delivery over multiple transport protocols.
* Inexpensive, pay-as-you-go model with no up-front cost.
* Web-based AWS Management Console offers the simplicity of a point-and-click interface.

## SNS vs SQS

* Both Messaging Services in AWS
* SNS - Push
* SQS - Polls (Pulls)

## SNS Pricing

* Users pay $0.50 per 1 million Amazon SNS Requests
* $0.06 per 100,000 Notification deliveries over HTTP
* $0.75 per 100 Notification deliveries over SMS
* $2.00 per 100,000 Notification deliveries over Email

## SNS

Amazon SNS follows the "publish-subscribe" (pub-sub) messaging paradigm, with notifications being delivered to clients using a "push" mechanism that eliminates the need to periodically check or "poll" for new information and updates.

With simple APIs requiring minimal up-front development effort, no maintenance or management overhead and pay-as-you-go pricing, Amazon SNS gives developers an easy mechanism to incorporate a powerful notification system with their application.

## SNS Exam Tips

* SNS is a scalable and highly available notification service which allows you to send push notifications from the cloud
* Variety of message formats supported: SMS text messages, email, Amazon Simple Queue Service (SQS) queues, any HTTP endpoint.
* Pub-sub model whereby users subscribe to topics
* It is a push mechanism, rather than a pull (poll) mechanism

# SES vs SNS

* `Amazon SES (Simple Email Service)` is a scalable and highly available email service design to help marketing teams and application developers send marketing, notification, and transactional emails to their customers using a pay as you go model.
* Can also be used to receive emails: incoming emails can be delivered automatically to an S3 bucket.
* Incoming emails can be used to trigger Lambda functions and SNS notifications.

## Amazon SES Use Cases

* Automated emails
* Purchase confirmations, shipping notifications, order status updates
* e.g., a mobile phone company that needs to send automated confirmation email every time a customer purchases pre-paid mobile phone minutes
* Marketing communications, advertisements, newsletters, special offers
* e.g., an online retail business that needs to let customers know about sales promotions and discounts

## SES vs SNS

| SES | SNS |
|---|---|
| Email messaging service | Pub/sub messaging service, formats include SMS, HTTP, SQS, email |
| Can trigger Lambda function or SNS notification | Can be used to trigger Lambda function |
| Can be used for both incoming and outgoing email | Can fan out messages to large number of recipients (replicate and push messages to multiple endpoints and formats)
| An email address is all that is required to start sending messages to a user | Consumers must subscribe to a topic to receive the notifications

## SNS vs SES Exam Tips

* Remember that SES is for email only
* It can be used for incoming and outgoing email
* It is not subscription based, you only need to know the email address

* SNS supports multiple formats (SMS, SQS, HTTP, email)
* Push notifications only
* Pub / sub model: consumers must subscribe to a topic
* You can fan-out messages to large number of recipients, (e.g., multiple clients each with their own SQS queue)

# Kinesis 101

## What is streaming data

Streaming Data is data that is generated continuously by thousands of data sources, which typically send in the data records simultaneously, and in small sizes (order of Kilobytes).

## What is Kinesis

Amazon Kinesis is a platform on AWS to send your streaming data to. Kinesis makes it easy to load and analyze streaming data, and also providing the ability for you to build your own custom applications for your business needs.

## What are the core Kinesis Services

* Kinesis Streams
* Kinesis Firehose
* Kinesis Analytics

## What is Kinesis Streams

* Kinesis Streams consist of shards
* 5 transactions per second for reads, up to a maximum total data read rate of 2 MB per second and up to 1,000 records per second for writes, up to a maximum total data write rate of 1 MB per second (including partition keys).
* The data capacity of your stream is a function of the number of shards that you specify for the stream. The total capacity of the stream is the sum of the capacities of its shards.

## What is Kinesis Firehose

## Kinesis Analytics

## Kinesis Exam Tips

* Know the difference between Kinesis Streams and Kinesis Firehose. You will be given scenario questions and you must choose the most relevant service.
* Understand what Kinesis Analytics is.

# Elastic Beanstalk 101

## What is Elastic Beanstalk?

`Elastic Beanstalk` is a service for deploying and scaling web applications developed in many popular languages: Java, .NET, PHP, Node.js, Python, Ruby, Go, and Docker onto widely used application server platforms like Apache Tomcat, Nginx, Passenger, and IIS.

Developers can focus on writing code and don't need to worry about any of the underlying infrastructure needed to run the application.

You upload the code and Elastic Beanstalk will handle deployment, capacity provisioning, load balancing, auto-scaling and application health.

You retain full control of the underlying AWS resources powering your application and you pay only for the AWS resources required to store and run your applications, (e.g., EC2 instances and S3 buckets).

* Fastest and simplest way to deploy your application in AWS
* Automatically scales your application up and down
* You can select the EC2 instance type that is optimal for your application
* You can retain full administrative control over the resources powering your application, or have Elastic Beanstalk do it for you
* Managed Platform Updates feature automatically applies updates to your Operating System, Java, PHP, Node.js, etc.
* Monitor and manage application health via a dashboard
* Integrated with CloudWatch and X-Ray for performance data and metrics

## Elastic Beanstalk Exam Tips

 * Deploys and scales your web applications including the web application server platform where required
 * Supports widely used programming technologies - Java, PHP, Python, Ruby, Go, Docker, .NET, Node.js
 * And application server platforms like Tomcat, Passenger, Puma, and IIS
 * Provisions the underlying resources for you
 * Can fully manage the EC2 instances for you or you can take full administrative control
 * Updates, monitoring, metrics and health checks all included

# Updating Elastic Beanstalk

## EBS Deployment Policies

`Elastic Beanstalk` supports several options for processing deployments:
* All at once
* Rolling
* Rolling with additional batch
* Immutable

## All at Once Deployment Policy

All at Once Deployment Updates:
* Deploys the new version to all instances simultaneously
* All of your instances are out of service while the deployment takes place
* You will experience an outage while the deployment is taking place - not ideal for mission-critical production systems
* If the update fails, you need to roll back the changes by re-deploying the original version to all your instances

## Rolling Deployment Policy

Rolling Deployment Updates:
* Deploys the new version in batches
* Each batch of instances is taken out of service while the deployment takes place
* Your environment capacity will be reduced by the number of instances in a batch while the deployment takes place
* Not ideal for performance sensitive systems
* If the update fails, you need to perform an additional rolling update to roll back the changes

## Rolling with Additional Batch Policy

Rolling with Additional Batch Deployment Updates:
* Launches an additional batch of instances
* Deploys the new version in batches
* Maintains full capacity during the deployment process
* If the update fails, you need to perform an additional rolling update to roll back the changes

## Immutable Deployment Policy

Immutable Deployment Updates:
* Deploys the new version to a fresh group of instances in their own new autoscaling group
* When the new instances pass their health checks, they are moved to your existing auto scaling group; and finally, the old instances are terminated
* Maintains a full capacity during the deployment process
* The impact of a failed update is far less, and the rollback process requires only terminating the new auto scaling group
* Preferred option for Mission Critical production systems

## Updating Elastic Beanstalk Exam Tips

* Remember the 4 different deployment approaches:
* **All at once**
* Service interruption while you update the entire environment at once. To roll back, perform a further all at once upgrade.
* **Rolling**
* Reduced capacity during deployment
* To roll back, perform a further rolling update
* **Rolling with Additional Batch**
* Maintains full capacity
* To roll back, perform a further rolling update
* **Immutable**
* Preferred option for mission critical production systems
* Maintains full capacity
* To roll back, just delete the new instances and autoscaling group

# Advanced Elastic Beanstalk

You can customize your Elastic Beanstalk environment using Elastic Beanstalk configuration files. (e.g. you can define packages to install, create Linux users and groups, run shell commands, specify services to enable or configure your load balancer, etc.)
These are files written in YAML or JSON format. They can have a filename of your choice but must have a `.config` extension and be saved inside a folder called `.ebextensions`.

## Location of Configuration Files

The `.ebextensions` folder must be included in the top-level directory of your application source code bundle.

This means that the configuration files can be placed under source control along with the with the rest of your application code.

## Advanced Elastic Beanstalk Exam Tips

* You can customize your Elastic Beanstalk environment by adding configuration files.
* The files are written in YAML or JSON
* Files have a .config extension
* The .config files are saved to the .ebextensions folder
* Your .ebextensions folder must be located in the top level directory of your application source code bundle.

# RDS & Elastic Beanstalk

Elastic Beanstalk supports two ways of integrating an RDS database with your Beanstalk environment.

You can launch the RDS instance from within the Elastic Beanstalk console, which means the RDS instance is created within your Elastic Beanstalk environment - a good option for Dev and Test deployments.

However this may not be ideal for production environments because it means the lifecycle of your database is tied to the lifecycle of your application environment. The database instance will be terminated if you you terminate the environment.

For Production environments, the preferred option is to decouple the RDS instance from your EBS environment: i.e. launch it outside of Elastic Beanstalk, directly from the RDS section of the console.

This option gives you a lot more flexibility, allows you to connect multiple environments to the same database, provides a wider choice of database types, and allows you to tear down your application environment without affecting the database instance.

## Access to RDS from Elastic Beanstalk

To allow the EC2 instances in your Elastic Beanstalk environment to connect to an outside database, there are two additional configuration steps required:
* An additional Security Group must be added to your environment Auto Scaling group
* You'll need to provide connection string configuration information to your application servers (endpoint, password using Elastic Beanstalk environment properties)

## RDS & Elastic Beanstalk Exam Tips

* Two different options for launching your RDS instance:
* Launch with Elastic Beanstalk. When you terminate the Elastic Beanstalk environment, the database will also be terminated. Quick and easy way to add your database and get started. Suitable for Dev and Test environments only.
* Launch outside of Elastic Beanstalk. Additional configuration steps required - security group and connection information. Suitable for Production environments, more flexibility. Allows connection from multiple environments, you can tear down the application stack without impacting the database.

# AWS Systems Manager Parameter Store

You work for a bank as a systems administrator. You need to store confidential information such as users, passwords, license keys, etc. This information needs to be passed to EC2 as a bootstrap script, while maintaining the confidentiality of the information.

## AWS Systems Manager Parameter Store Exam Tips

* Confidential Information such as passwords, database connection strings, and license codes can be stored in SSM Parameter Store.
* You can store values as plain text or you can encrypt the data.
* You can then reference these values by using their names.
* You can use this service with EC2, CloudFormation, Lambda, EC Run Command, etc.

# Other AWS Services Summary

## SQS Exam Tips

* SQS is a distributed message queueing system
* Allows you to decouple the components of an application so that they are independent
* Pull-based, not push-based
* Standard Queues (default) - best-effort ordering: message delivered at least once
* FIFO Queues (First In First Out) - ordering strictly preserved, message delivered once, no duplicates. e.g., good for banking transactions which need to happen in strict order.
* Visibility Timeout. Default is 30 seconds - increase if your task takes > 30s to complete. Max 12 hours.
* Short polling - returned immediately even if no messages are in the queue.
* Long polling - polls the queue periodically and only returns a response when a message is in the queue or the timeout is reached.

## SNS Exam Tips

* SNS is a scalable and highly available notification service which allows you to send push notifications from the cloud
* Variety of message formats supported: SMS text messages, email, Amazon Simple Queue Service (SQS) queues, any HTTP endpoint.
* Pub-sub model whereby users subscribe to topics
* It is a push mechanism, rather than a pull (poll) mechanism

## SNS vs SES Exam Tips

* Remember that SES is for email only
* It can be used for incoming and outgoing email
* It is not subscription based, you only need to know the email address

* SNS supports multiple formats (SMS, SQS, HTTP, email)
* Push notifications only
* Pub / sub model: consumers must subscribe to a topic
* You can fan-out messages to large number of recipients, (e.g., multiple clients each with their own SQS queue)

## Kinesis Exam Tips

* Know the difference between Kinesis Streams and Kinesis Firehose. You will be given scenario questions and you must choose the most relevant service.
* Understand what Kinesis Analytics is.

## Elastic Beanstalk Exam Tips

 * Deploys and scales your web applications including the web application server platform where required
 * Supports widely used programming technologies - Java, PHP, Python, Ruby, Go, Docker, .NET, Node.js
 * And application server platforms like Tomcat, Passenger, Puma, and IIS
 * Provisions the underlying resources for you
 * Can fully manage the EC2 instances for you or you can take full administrative control
 * Updates, monitoring, metrics and health checks all included

## Updating Elastic Beanstalk Exam Tips

 * Remember the 4 different deployment approaches:
 * **All at once**
 * Service interruption while you update the entire environment at once. To roll back, perform a further all at once upgrade.
 * **Rolling**
 * Reduced capacity during deployment
 * To roll back, perform a further rolling update
 * **Rolling with Additional Batch**
 * Maintains full capacity
 * To roll back, perform a further rolling update
 * **Immutable**
 * Preferred option for mission critical production systems
 * Maintains full capacity
 * To roll back, just delete the new instances and autoscaling group

## Advanced Elastic Beanstalk Exam Tips

 * You can customize your Elastic Beanstalk environment by adding configuration files.
 * The files are written in YAML or JSON
 * Files have a .config extension
 * The .config files are saved to the .ebextensions folder
 * Your .ebextensions folder must be located in the top level directory of your application source code bundle.

## RDS & Elastic Beanstalk Exam Tips

 * Two different options for launching your RDS instance:
 * Launch with Elastic Beanstalk. When you terminate the Elastic Beanstalk environment, the database will also be terminated. Quick and easy way to add your database and get started. Suitable for Dev and Test environments only.
 * Launch outside of Elastic Beanstalk. Additional configuration steps required - security group and connection information. Suitable for Production environments, more flexibility. Allows connection from multiple environments, you can tear down the application stack without impacting the database.

## AWS Systems Manager Parameter Store Exam Tips

 * Confidential Information such as passwords, database connection strings, and license codes can be stored in SSM Parameter Store.
 * You can store values as plain text or you can encrypt the data.
 * You can then reference these values by using their names.
 * You can use this service with EC2, CloudFormation, Lambda, EC Run Command, etc.
