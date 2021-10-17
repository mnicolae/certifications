## Introduction to CloudWatch

Amazon CloudWatch is a monitoring service to monitor your AWS resources, as well as the applications that you run on AWS.

CloudWatch can monitor things like:
* Compute
** Autoscaling Groups
** Elastic Load Balancers
** Route53 Health Checks
* Storage & Content Delivery
** EBS Volumes
** Storage Gateways
** CloudFront
* Database & Analytics
** DynamoDB
** Elasticache Nodes
** RDS Instances
** Elastic MapReduce Job Flows
** Redshift
* Other
** SNS Topics
** SQS Queues
** Ops work
** CloudWatch Logs
** Estimated Charges on your AWS Bill

### CloudWatch and EC2

Host Level Metrics consist of:
* CPU
* Network
* Disk
* Status Checks

Exam tip: RAM utilization is a custom metric! By default EC2 monitoring is 5 minutes intervals, unless you enable detailed monitoring which will then make it 1 minute intervals.

### How Long are CloudWatch Metrics Stored?

You can retrieve data using the `GetMetricStatistics` API or by using third party tools offered by AWS partners.

You can store your log data in CloudWatch Logs for as long as you want. By default, CloudWatch Logs will store your log data indefinitely. You can change the retention for each Log Group at any time.

You can retrieve data from any terminated EC2 or ELB instance after its termination.

### Metric Granularity?

It depends on the AWS service. Many default metrics for many default services are 1 minute, but it can be 3 or 5 minutes depending on the service.

Exam tip: for custom metrics the minimum granularity that you can have is 1 minute.

### CloudWatch Alarms

You can create an alarm to monitor any Amazon CloudWatch metric in your account. This can include EC2 CPU utilization, Elastic Load Balancer Latency or even the charges on your AWS bill. You can set the appropriate thresholds in which to trigger the alarms and also set what actions should be taken if an alarm state is reached. This will be covered in a subsequent lecture.

### CloudWatch Exam Tips

CloudWatch - a monitoring service to monitor your AWS resources, as well as the applications that you run on AWS.

Host Level Metrics consist of:
* CPU
* Network
* Disk
* Status Check

RAM utilization - is a custom metric.

Custom metrics - minimum granularity is 1 minute.

Terminated instances - You can retrieve data from any terminated EC2 or ELB instance after its termination. CloudWatch Logs by default are stored indefinitely.

Metric Granularity
* 1 minute for detailed monitoring
* 5 minutes for standard monitoring

CloudWatch can be used on premise - Not restricted to just AWS resources. Just need to download and install the SSM agent and CloudWatch agent.

## CloudWatch vs. CloudTrail

### CloudWatch vs. CloudTrail vs. Config?

* CloudWatch monitors performance.
* CloudTrail monitors API calls in the AWS platform.
* AWS Config records the state of your AWS environment and can notify you of changes.
