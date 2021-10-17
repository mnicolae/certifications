# S3 101

## What is S3?

S3 provides developers and IT teams with secure, durable, highly-scalable object storage. Amazon S3 is easy to use, with a simple web services interface to store and retrieve any amount of data from anywhere on the web.

S3 is a safe place to store your files.

It is object-based storage.

The data is spread across multiple devices and facilities.

## S3 - The Basics

* S3 is object-based - i.e., allows you to upload files.
* Files can be from 0 Bytes to 5 TB.
* There is unlimited storage.
* Files are stored in buckets (similar to a folder).
* S3 is a universal namespace. That is, names must be unique globally.
* When you upload a file to S3, you will receive a HTTP 200 status code if the upload was successful.

## Data Consistency Model for S3

* Read after Write consistency for PUTS of new Objects
* Eventual Consistency for overwrite PUTS and DELETES (can take some time to propagate)

## S3 Is a Simple Key-value Store

* S3 is Object based. Objects consist of the following:
** Key (this is simply the name of the object)
** Value (this is simply the data, which is made up of a sequence of bytes).
** Version ID (important for versioning)
** Metadata (data about data you are storing)
** Sub-resources - bucket specific configuration: bucket policies, access control lists, cross origin resource sharing (CORS), transfer acceleration

## S3 - The Basics

* Built for 99.99% availability for the S3 platform
* Amazon guarantees 99.9% availability
* Amazon guarantees 99.999999999% durability for S3 information (remember 11 x 9s)
* Tiered storage
* Lifecycle Management
* Versioning
* Encryption
* Secure your data - ACLs, bucket policies

## S3 - Storage Tiers / Classes

* S3: 99.99% availability, 99.999999999% durability, stored redundantly across multiple devices in multiple facilities, and is designed to sustain the loss of 2 facilities concurrently.
* S3 - IA (infrequent accessed): for data that is accessed less frequently, but requires rapid access when needed. Lower fee than S3, but you are charged a retrieval fee.
* S3 - One Zone IA: Same as IA however data is stored in a single AZ only, still 99.999999999% durability, but only 99.5% availability. Cost is 20% less than regular S3 - IA.
* Reduced Redundancy Storage: Designed to provide 99.99% durability and 99.99% availability of objects over a given year. Used for data that can recreated if lost, e.g. thumbnails. (Starting to disappear from AWS docs but may still feature in exam)
* Glacier: Very cheap, but used for archival only. Optimized for data that is infrequently accessed and it takes 3 - 5 hours to restore from Glacier.

## S3 - Storage Tiers / Classes

| Storage class | Durability | Availability | Other considerations |
|---|---|---|---|
| STANDARD | 99.999999999% | 99.99% | None
| STANDARD_IA | 99.999999999% | 99.9% | Retrieval fee for all S3 objects |
| ONEZONE_IA | 99.999999999% | 99.5% | Not resilient to loss of AZ.
| GLACIER | 99.999999999% | 99.99% (after you restore objects) | No real-time access, 3 - 5 hours to access.
| RRS | 99.99% | 99.99% | None

## S3 - Intelligent Tiering

* Unknown or unpredictable access patterns.
* 2 tiers - frequent and infrequent access.
* Automatically moves your data to most cost-effective tier based on how frequently you access each object.
* 99.999999999% durability
* 99.9% availability over a given year
* Optimizes cost
* No fees for accessing your data but a small monthly fee for monitoring / automation $0.0025 per 1,000 objects.

## S3 - Charges

Charged for:
* Storage per GB
* Requests (Get, Put, Copy, etc.)
* Storage Management Pricing
** Inventory, Analytics, and Object Tags
* Data Management Pricing
** Data transferred out of S3
* Transfer acceleration
** Use of CloudFront to optimize transfers

## S3 - Exam Tips for S3 101

* Remember that S3 is Object-Based: i.e., allows you to upload files. Object-based storage only (for files)
* Not suitable to install an OS or running a database on.
* Files can be from 0 Bytes to 5 TB.
* There is unlimited storage.
* Files are stored in buckets.
* S3 is a universal namespace. That is, names must be unique globally.
* Read after Write consistency for PUTS of new Objects
* Eventual Consistency for overwrite PUTS and DELETES (can take some time to propagate)
* S3 Storage Classes / Tiers
* Remember the core fundamentals of an S3 object:
** Key (name)
** Value (data)
** Version ID
** Metadata
** Sub-resources - bucket-specific config: bucket policies, access control lists, CORS, transfer acceleration.
* Successful uploads will generate a HTTP 200 status code - when you use the CLI or rapid
* Make sure you read the S3 FAQ: https://aws.amazon.com/s3/faqs

# S3 Security

## Securing Your buckets

* By default, all newly created buckets are PRIVATE.
* You can set up access control to your buckets using:
** Bucket policies - Applied at a bucket level.
** Access Control Lists - Applied at an object level.
* S3 buckets can be configured to create access logs, which log all requests made to the S3 bucket. These logs can be written to another bucket.

# S3 Encryption

## Encryption

* In Transit: SSL / TLS
* At rest:
** Service Side Encryption:
** S3 Managed Keys - SSE-S3
** AWS Key Management Service, Managed Keys, SSE-KMS
** Server Side Encryption with Customer Provided Keys - SSE-C
** Client Side Encryption

# Enforcing Encryption on S3 buckets

* If the file is to be encrypted at upload time, the `x-amz-server-side-encryption` parameter will be included in the request header
* Two options are currently available:
** `x-amz-server-side-encryption: AES256` (SSE-S3 - S3 managed keys)
** `x-amz-server-side-encryption: ams:kms` (SSE-KMS - KMS managed keys)
* When this parameter is included in the header of the PUT request, it tells S3 to encrypt the object at the time of upload, using the specified encryption method.
* You can enforce the use of Server Side Encryption by using a Bucket Policy which denies any S3 PUT request which doesn't include the `x-amz-server-side-encryption` parameter in the request header.

## S3 Encryption Exam Tips

* Encryption In-Transit: SSL / TLS (HTTPS)
* Encryption At Rest
** Server Side Encryption: SSE-S3, SSE-KMS, SSE-C
** Client Side Encryption
* If you want to enforce the use of encryption for your files stored in S3, use an S3 Bucket Policy to deny all PUT requests that don't include the `x-amz-server-side-encryption` parameter in the request header.

# CloudFront

## What is a CDN?

A content delivery network (CDN) is a system of distributed servers (network) that deliver webpages and other web content to a user based on the geographic locations of the user, the origin of the webpage, and a content delivery server.

## CloudFront - Key Terminology

* `Edge Location` - This is the location where content is cached and can also be written. Separate to an AWS Region / AZ.
* `Origin` - This is the origin of all the files that the CDN will distribute. Origins can be an S3 bucket, an EC2 instance, an ELB, or Route 53.
* `Distribution` - This is the name given the CDN, which consists of a collection of Edge Locations.
* `Web Distribution` - Typically used for Websites.
* `RTMP` - Used for Media Streaming.

## What is CloudFront?

Amazon CloudFront can be used to deliver your entire website, including dynamic, static, streaming, and interactive content using a global network of edge locations. Requests for your content are automatically routed to the nearest edge location, so content is delivered with the best possible performance.

E.g., can be used to optimize performance for users accessing a website backed by S3.

Amazon CloudFront is optimized to work with other Amazon Web Services, like Amazon Simple Storage Service (Amazon S3), Amazon Elastic Compute Cloud (Amazon EC2), Amazon Elastic Load Balancing, and Amazon Route 53. Amazon CloudFront also works seamlessly with any non-AWS origin server, which stores the original, definitive versions of your files.

## CloudFront - Key Terminology

CloudFront Distribution types:
* Web Distribution - Used for websites, HTTP/HTTPS
* RTMP Distribution - (Adobe Real Time Messaging Protocol) - Used for Media Streaming / Flash multi-media content

## CloudFront and S3 Transfer Acceleration

Amazon S3 Transfer Acceleration enables fast, easy, and secure transfers of files over long distances between your end users and an S3 bucket.

Transfer Acceleration takes advantage of Amazon CloudFront's globally distributed edge locations. As the data arrives at an edge location, data is routed to Amazon S3 over an optimized network path.

## CloudFront - Exam Tips

* `Edge Location` - This is the location where content will be cached.
* `Origin` - This is the origin of all the files that the CDN will distribute. Origins can be an S3 bucket, an EC2 instance, an ELB, or Route 53.
* `Distribution` - This is the name given the CDN, which consists of a collection of Edge Locations.
* `Web Distribution` - Typically used for Websites
* `RTMP` - Used for Media Streaming
* Edge locations are not just READ only - you can WRITE to them, too. (i.e., PUT an object on to them)
* CloudFront Edge Locations are utilized by S3 Transfer Acceleration to reduce latency for S3 uploads.
* Objects are cached for the life of the TTL (Time to Live).
* You can clear cached objects, but you will be charged.

# S3 Performance Optimization

S3 is designed to support very high request rates. However, if your S3 buckets are routinely receiving >100 PUT / LIST / DELETE or >300 GET requests per second, then there are some best practice guidelines that will help optimize S3 performance.

The guidance is based on the type of workload you are running:
* GET-Intensive Workloads - use CloudFront content delivery service to get best performance. CloudFront will cache your most frequently accessed objects and will reduce latency for your GET requests.
* Mixed Request Type Workloads - a mix of GET, PUT, DELETE, GET bucket - the key names you use for your objects can impact performance for intensive workloads
* S3 uses the key name to determine which partition an object will be stored in
* The use of sequential key names e.g., names prefixed with a time stamp or alphabetical sequence increases the likelihood of having multiple objects stored on the same partition.
* For heavy workloads this can cause I/O issues and contention
* By using a random prefix to key names, you can force S3 to distribute your keys across multiple partitions, distributing the I/O workload.

## S3 Performance Optimization - Exam Tips

* Remember the 2 main approaches to Performance Optimization for S3:
** GET-Intensive Workloads - Use CloudFront
** Mixed-Workloads - Avoid sequential key names for your S3 objects. Instead, add a random prefix like a hex hash to the key name to prevent multiple objects from being stored on the same partition.

# S3 Performance Update

* In July 2018, Amazon announced a massive increase in S3 performance.
** 3500 put requests per second
** 5500 get requests per second

* This new increased performance negates the previous guidance to randomize your object key names to achieve faster performance.
* This means logical and sequential naming patterns can now be used without any performance implications.

# S3 Summary

## S3 101 - Summary

* Remember that S3 is object-based: i.e., allows you to upload files.
* Files can be from 0 Bytes to 5 TB.
* There is unlimited storage.
* Files are stored in buckets.
* S3 is a universal namespace. That is, names must be unique globally.

## S3 101 - Summary

* Read after Write consistency for PUTS of new Objects
* Eventual Consistency for overwrite PUTS and DELETES (can take some time to propagate)

## S3 101 - Summary

* S3 Storage Classes / Tiers

## S3 101 - Summary

* Remember the core fundamentals of an S3 object:
** Key (name)
** Value (data)
** Version ID
** Metadata
** Sub-resources - bucket specific configuration: bucket policies, access control lists, cross origin resource sharing (CORS), transfer acceleration

## S3 101 - Summary

* Object-based storage only (for files)
* Not suitable to install an operating system on.
* Successful uploads will generate a HTTP 200 status code.

## S3 Security - Summary

* By default, all newly created buckets are PRIVATE.
* You can set up access control to your buckets using:
** Bucket policies - Applied at a bucket level.
** Access Control Lists - Applied at an object level.
* S3 buckets can be configured to create access logs, which log all requests made to the S3 bucket. These logs can be written to another bucket.

## S3 Encryption - Summary

* Encryption In Transit: SSL / TLS
* At rest:
** Service Side Encryption:
** SSE-S3
** SSE-KMS
** SSE-C
** Client Side Encryption

* Remember that we can use a Bucket Policy to prevent unencrypted files from being uploaded by using a a policy which only allows requests which include the `x-amz-server-side-encryption` parameter in the request header.

## S3 CORS - Summary

* Cross Origin Resource Sharing (CORS)
** Used to enable cross origin access for your AWS resources
** e.g., hosted website accessing javascript or image files located in another S3 bucket
** by default resources in one bucket cannot access resources located in another
** to allow this we need to configure CORS on the bucket being accessed and enable access for the origin (bucket) attempting to access
** always use the S3 website URL, not the regular bucket URL.

## S3 CloudFront - Summary

* `Edge Location` - This is the location where content is cached. This is separate to an AWS Region / AZ.
* `Origin` - This is the origin of all the files that the CDN will distribute. Origins can be an S3 bucket, an EC2 instance, an ELB, or Route 53.
* `Distribution` - This is the name given the CDN, which consists of a collection of Edge Locations.
* `Web Distribution` - Typically used for Websites
* `RTMP` - Used for Media Streaming

* Edge location are not just READ only - you can write to them too. (i.e., put an object on to them.)
* Objects are cached for the life of the TTL (Time to Live).
* You can clear cached objects, but you will be charged.

## S3 Performance Optimization - Summary

* Remember the 2 main approaches to Performance Optimization for S3:
** GET-Intensive Workloads - Use CloudFront
** Mixed-Workloads - Avoid sequential key names for your S3 objects. Instead, add a random prefix like a hex hash to the key name to prevent multiple objects from being stored on the same partition.

## S3 - Summary

* Read the FAQ!
* https://aws.amazon.com/s3/faqs
