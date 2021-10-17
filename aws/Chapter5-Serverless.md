# Lambda Exam Tips

* Lambda scales out (not up) automatically
* Lambda functions are independent, 1 event = 1 function
* Lambda is serverless
* Know what services are serverless!
* Lambda functions can trigger other lambda functions, 1 event can = X functions if functions trigger other functions
* Architectures can get extremely complicated, AWS X-Ray allows you to debug what is happening
* Lambda can do things globally, you can use it to back up S3 buckets to other S3 buckets etc.
* Know your triggers

# API Gateway Exam Tips

* API Gateway has caching capabilities to increase performance
* API Gateway is low cost and scales automatically
* You can throttle API Gateway to prevent attacks
* You can log results to CloudWatch
* If you are using Javascript / AJAX that uses multiple domains with API Gateway, ensure that you have enabled CORS on API Gateway
* CORS is enforced by the client

# Version Control with Lambda Exam Tips

* Can have multiple versions of lambda functions
* Latest version will use $LATEST
* Qualified version will use $LATEST, unqualified will not have it
* Versions are immutable (cannot be changed)
* Can split traffic using aliases to different versions
* Cannot split traffic with $LATEST, instead create an alias to latest.

# Step Functions

**Step Functions** allow you to visualize and test your serverless applications. Step Functions provides a graphical console to arrange and visualize the components of your applications as a series of steps. This makes it simple to build and run multistep applications. Step Functions automatically triggers and tracks each step, and retries when there are errors, so your application executes in order and as expected. Step Functions logs the state of each step, so when things go wrong, you can diagnose and debug problems quickly.

## Step Functions Exam tips

* Great way to visualize your serverless application.
* Step Functions automatically triggers and tracks each step.
* Step Functions logs the state of each step so if something goes wrong you can track what went wrong and where.

# X-Ray Exam Tips

The X-Ray SDK provides:
* Interceptors to add to your code to trace incoming HTTP requests
* Client handlers to instrument AWS SDK clients that your application uses to call other AWS services
* An HTTP client to use to instrument calls to other internal and external HTTP web services

The X-Ray integrates with the following AWS services:
* Elastic Load Balancing
* AWS Lambda
* Amazon API Gateway
* Amazon Elastic Compute Cloud
* AWS Elastic Beanstalk

The X-Ray integrates with the following languages:
* Java
* Go
* Node.js
* Python
* Ruby
* .NET

# Advanced API Gateway Exam Tips

* Import API's using Swagger 2.0 definition files
* API Gateway can be throttled
* Default limits are 10,000 RPS or 5,000 concurrently
* You can configure API Gateway as a SOAP Webservice passthrough
