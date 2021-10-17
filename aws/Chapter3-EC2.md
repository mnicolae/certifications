# EC2 101

## What is EC2?

Amazon Elastic Compute Cloud (Amazon EC2) is a web service that provides resizable compute capacity in the cloud. Amazon EC2 reduces the time required to obtain and boot new server instances to minutes, allowing you to quickly scale capacity, both up and down, as your computing requirements change.

Amazon EC2 changes the economics of computing by allowing you to pay only for capacity that you actually use. Amazon EC2 provides developers the tools to build failure resilient applications and isolate themselves from common failure scenarios.

## EC2 options

* **On demand** - allows you to pay a fixed rate by the hour (or by the second) with no commitment.
* **Reserved** - provides you with a capacity reservation, and offer a significant discount on the hourly charge for an instance. 1 Year or 3 Year terms.
* **Spot** - enables you to bid whatever price you want for an instance capacity, providing for even greater savings if your applications have flexible start and end times.
* **Dedicated Hosts** - Physical EC2 server dedicated for your use. Dedicated Hosts can help you reduce costs by allowing you to use your existing server-bound software licenses.

## On Demand

* Perfect for users that want the low cost and flexibility of Amazon EC2 without any up-front payment or long-term commitment.
* Applications with short term, spiky, or unpredictable workloads that cannot be interrupted.
* Applications being developed or tested on Amazon EC2 for the first time.

## Reserved Instances

* Applications with steady state or predictable usage
* Applications that require reserved capacity
* Users can make up-front payments to reduce their total computing costs even further
** Standard RIs (up to 75% off on-demand)
** Convertible RIs (up to 54% off on-demand) feature the capability to change the attributes of the RI as long as the exchange results in the creation of Reserved Instances of equal or greater value.
** Scheduled RIs are available to launch within the time window you reserve. This option allows you to match your capacity reservation to a predictable recurring schedule that only requires a fraction of a day, a week, or a month.


## Spot instances

* Applications that have flexible start and end times.
* Applications that are only feasible at very low compute prices
* Users with an urgent need for large amounts of additional computing capacity.

## Dedicated Hosts

* Useful for regulatory requirements that may not support multi-tenant virtualization.
* Great for licensing which does not support multi-tenancy or cloud deployments.
* Can be purchased On-Demand (hourly)
* Can be purchased as a Reservation for up to 70% off the On-Demand price.

## EC2 instance types

* How I remember them;
** F for FPGA
** I for IOPS
** G - Graphics
** H - High Disk Throughput
** T - cheap general purpose (think T2 micro)
** D for Density
** R for RAM
** M - main choice for general purpose apps
** C for Compute
** P - Graphics (think Pics)
** X - Extreme Memory

## What is EBS?

Amazon EBS allows you to create storage volumes and attach them to Amazon EC2 instances. Once attached, you can create a file system on top of these volumes, run a database, or use them in any other way you would use a block device. Amazon EBS volumes are placed in a specific Availability Zone, where they are automatically replicated to protect you from the failure of a single component.

## EBS volume types

* General purpose SSD (GP2)
** General purpose, balances both price and performance.
** Ratio of 3 IOPS per GB with up to 10,000 IOPS (I/O operations per second) and the ability to burst up to 3,000 IOPS for extended periods of time for volumes at 3334 GiB and above.
* Provisioned IOPS SSD (IO1)
** Designed for I/O intensive applications such as large relational or NoSQL databases.
** Use if you need more than 10,000 IOPS.
** Can provision up to 20,000 IOPS per volume.
* Throughput Optimized HDD (ST1)
** Big data
** Data warehouses
** Log processing
** Cannot be a boot volume
* Cold HDD (SC1)
** Lowest Cost Storage for infrequently accessed workloads
** File server
** Cannot be a boot volume
* Magnetic (Standard)
** Lowest cost per gigabyte of all EBS volume types that is bootable. Magnetic volumes are ideal for workloads where data is accessed infrequently, and applications where the lowest storage cost is important.
** Legacy.

## EC2 Exam Tips

* **On demand** - allows you to pay a fixed rate by the hour (or by the second) with no commitment.
* **Reserved** - provides you with a capacity reservation, and offer a significant discount on the hourly charge for an instance. 1 Year or 3 Year terms.
* **Spot** - enables you to bid whatever price you want for an instance capacity, providing for even greater savings if your applications have flexible start and end times.
* **Dedicated Hosts** - Physical EC2 server dedicated for your use. Dedicated Hosts can help you reduce costs by allowing you to use your existing server-bound software licenses.

If a spot instance is terminated by Amazon EC2, you will not be charged for a partial hour of usage. However, if you terminate the instance yourself, you will be charged for the complete hour in which the instance ran.

FIGHT DR MC PX! *mnemonic device for instance types*

SSD
* General purpose SSD - balances price and performance for a wide variety of workloads.
* Provisioned IOPS SSD - Highest-performance SSD volumes for mission-critical low-latency or high-throughput workloads.

Magnetic
* Throughput Optimized HDD - Low cost HDD volume designed for frequently accessed, throughput-intensive workloads.
* Cold HDD - Lowest cost HDD volume designed for less frequently accessed workloads.
* Magnetic - Previous Generation. Can be a boot volume.

# Elastic Load Balancers

## Types of Load Balancers

* Application Load Balancer (ALB)
* Network Load Balancer
* Classic Load Balancer

## Application Load Balancers

**Application Load Balancers** are best suited for load balancing of HTTP and HTTPS traffic. They operate at Layer 7 and are application-aware. They are intelligent, and you can create advanced request routing, sending specified requests to specific web servers.

## Network Load Balancers

**Network Load Balancers** are best suited for load balancing of TCP traffic where extreme performance is required. Operating at the connection level (Layer 4), Network Load Balancers are capable of handling millions of requests per second, while maintaining ultra-low latencies.

Use for extreme performance!

## Classic Load Balancers

**Classic Load Balancers** are the legacy Elastic Load Balancers. You can load balance HTTP/HTTPS applications and use Layer 7-specific features, such as X-Forwarded and sticky sessions. You can also use strict Layer 4 load balancing for applications that rely purely on the TCP protocol.

## Load Balancer Errors

**Classic Load Balancers** - if your application stops responding, the ELB (classic load balancer) responds with a 504 error.

This means that the application is having issues. This could be either at the web server layer or at the database layer.

Identify where the application is failing, and scale it up or out where possible.

## ELB Exam Tips

* 3 types of load balancers;
** Application Load balancers
** Network load balancers
** Classic load balancers
* 504 error means the gateway has timed out. This means that the application not responding within the idle timeout period.
** Troubleshoot the application. Is it the web server or the database server?
* If you need the IPv4 address of your end user, look for the X-Forwarded-For header.

# Route 53

## Route 53 exam tips

* Route 53 is Amazon's DNS service
* Allows you to map your domain name to
** EC2 instances
** Load balancers
** S3 buckets

# AWS CLI

## CLI Tips

**Least privilege** - Always give your users the minimum amount of access required.

**Create Groups** - Assign your users to groups. Your users will automatically inherit the permissions of the group. The group permissions are assigned using policy documents.

**Secret Access Key** - You will see this only once. If you do not save it, you can delete the Key Pair (Access Key ID and Secret Access Key) and regenerate it. You will need to run **aws configure** again.

**Do not use just one access key** - Do not create just one access key and share that with all your developers. If someone leaves the company on bad terms, then you will need to delete the key and create a new one and every developer would then need to update their keys. Instead create one key pair per developer.

# EC2 with S3 Role

## Exam tips

* Roles allow you to not use Access Key IDs and Secret Access Keys.
* Roles are preferred from a security perspective.
* Roles are controlled by policies.
* You can chance a policy on a role and it will take immediate effect.
* You can attach and detach roles to running EC2 instances without having to stop or terminate these instances.

# How to Encrypt an EBS volume attached to EC2

## Exam tips

* You can encrypt the root device volume (the volume the OS is installed on) using Operating System level encryption.
* You can encrypt the root device volume by first taking a snapshot of that volume, and then creating a copy of that snap with encryption. You can then make an AMI of this snap and deploy the encrypted root device volume.
* You can encrypt additional attached volumes using the console, CLI, or API.

# RDS 101

## What is a relational database?

Relational databases are what most of us are all used to. They have been around since the 70s. Think of a traditional spreadsheet:
* Database
* Tables
* Row
* Fields (columns)

## Relational Database Types

* SQL Server
* Oracle
* MySQL Server
* PostgreSQL
* Aurora
* MariaDB

## Non relational databases

* Database
** Collection = Table
** Document = Row
** Key Value Pairs = Fields

## What is data warehousing?

* Used for BI. Tools like Cognos, Jaspersoft, SQL Server Reporting Services, Oracle Hyperion, and SAP NetWeaver.
* Used to pull in very large and complex data sets. Usually used by management to do queries on data (such as current performance vs. targets etc.)

## OLTP vs. OLAP

Online Transaction Processing (OLTP) differs from OLAP Online Analytics Processing (OLAP) in terms of the types of queries you will run.

Data warehousing databases use different type of architecture both from a database perspective and infrastructure layer.

## AWS Database Types

* RDS - OLTP
** SQL
** MySQL
** PostgreSQL
** Oracle
** Aurora
** MariaDB
* DynamoDB - No SQL
* RedShift - OLAP
* Elasticache - in-memory caching
** Memcached
** Redis

# RDS - Back ups, multi-AZ & read replicas

## Automated Backups

* There are two different types of backups for AWS: automated backups and database snapshots.
* Automated backups allow you to recover your database to any point in time within a "retention period". The retention period can be between 1 and 35 days. Automated backups will take a full daily snapshot and will also store transaction logs throughout the day. When you do a recovery, AWS will first choose the most recent daily back up, and then apply transaction logs relevant to that day. This allows you to do a point in time recovery down to a second, within the retention period.

Automated Backups are enabled by default. The backup data is stored in S3 and you get free storage space equal to the size of your database. So if you have an RDS instance of 10Gb, you will get 10Gb worth of storage.

Backups are taken within a defined window. During the backup window, storage I/O may be suspended while your data is backed up and you may experience elevated latency.

## Snapshots

DB Snapshots are done manually (i.e., they are user initiated). They are stored even after you delete the original RDS instance, unlike automated backups.

## Restoring Backups

Whenever you restore either an automatic backup or a manual snapshot, the recovered version of the database will be a new RDS instance with a new DNS endpoint.

## Encryption

Encryption at rest is supported for MySQL, Oracle, SQL Server, PostgreSQL, MariaDB & Aurora. Encryption is done using the AWS Key Management (KMS) Service. Once your RDS instance is encrypted, the data stored at rest in the underlying storage is encrypted, as are its automated backups, read replicas, and snapshots.

At the present time, encrypting an existing DB instance is not supported. To use Amazon RDS encryption for an existing database, you must first create a snapshot, make a copy of that snapshot and encrypt the copy.

## What is a multi-AZ?

Multi-AZ allows you to have an exact copy of your production database in another AZ. AWS handles the replication for you, so when your production database is written to, this write will automatically be synchronized to the stand by database.

In the event of planned database maintenance, DB instance failure, or an availability zone failure, Amazon RDS will automatically failover to the standby so that database operations can resume quickly without administrative intervention.

Multi-AZ is for Disaster Recovery only. It is not primarily used for improving performance. For performance improvement, you need read replicas.

## Multi-AZ Databases

* SQL Server
* Oracle
* MySQL Server
* PostgreSQL
* MariaDB

## What is a Read Replica?

Read replicas allow you to have a read-only copy of your production database. This is achieved by using Asynchronous replication from the primary RDS instance to the read replica. You use read replicas primarily for very read-heavy database workloads.

## Read Replica Databases

* MySQL Server
* PostgreSQL
* MariaDB
* Aurora

## Read Replica Databases

* Used for scaling, not DR!
* Must have automatic backups turned on in order to deploy a read replica.
* You can have up to 5 read replica copies of any database.
* You can have read replicas of read replicas (but watch out for latency).
* Each read replica will have its own DNS endpoint.
* You can have read replicas that have Multi-AZ.
* Read replicas can be promoted to be their own databases. This breaks the replication.
* You can have a read replica in another region.

# Elasticache 101

## What is Elasticache?

Elasticache is a web service that makes it easy to deploy, operate, and scale an in-memory cache in the cloud. The service improves the performance of web applications by allowing you to retrieve information from fast, managed, in-memory caches, instead of relying entirely on slow disk-based databases.

Amazon Elasticache can be used to significantly improve latency and throughput for many read-heavy application workloads (such as social networking, gaming, media sharing and Q&A portals) or compute-intensive workloads (such as recommendation engines).

Caching improves application performance by storing critical pieces of data in memory for low-latency access. Cached information may include the results of I/O-intensive database queries or the results of computationally-intensive calculations.

## Types of Elasticached

* Memcached
** A widely adopted memory object caching system. ElastiCache is protocol compliant with Memcached, so popular tools that you use today with existing Memcached environments will work seamlessly with the service.
* Redis
** A popular open-source in-memory key-value store that supports data structures such as sorted sets and lists. ElastiCache supports Master / Slave replication and Multi-AZ which can be used to achieve cross AZ redundancy.

## Redis

Although both Memcached and Redis appear similar on the surface (in that they are both in-memory key stores), they are actually quite different in practice. Because of the replication and persistence features of Redis, ElastiCache manages Redis more as a relational database. Redis ElastiCache clusters are managed as stateful entities that include failover, similar to how Amazon RDS manages database failover.

## Memcached

Because Memcached is designed as a pure caching solution with no persistence, ElastiCache manages Memcached nodes as a pool that can grow and shrink, similar to an Amazon EC2 Auto Scaling group. Individual nodes are expendable, and ElastiCache provides additional capabilities here, such as automatic node replacement and Auto Discovery.

## Memcached - Use Cases

* Is object caching your primary goal, for example to offload your database? If so, use Memcached.
* Are you interested in as simple a caching model as possible? If so, use Memcached.
* Are you planning on running large scale cache nodes, and require multithreaded performance with utilization of multiple cores? If so, use Memcached.
* Do you want the ability to scale your cache horizontally as you grow? If so, use Memcached.


## Redis - Use Cases

* Are you looking for more advanced data types, such as lists, hashes, and sets? If so, use Redis.
* Does sorting and ranking datasets in memory help you, such as with leaderboards? If so, use Redis.
* Is persistence of your key store important? If so, use Redis.
* Do you want to run in multiple AWS Availability Zones (multi-AZ) with failover? If so, use Redis.

## Elasticache exam tips

Typically, you will be given a scenario where a particular database is under a lot of stress /load. You may be asked which service you should use to alleviate this.

Elasticache is a good choice if your database is particularly read-heavy and not prone to frequent changing.

Redshift is a good answer if the reason your database is feeling stress is because management keep running OLAP transactions on it, etc.

Use Memcached if
* Object caching is your primary goal
* You want to keep things as simple as possible
* You want to scale your cache horizontally (scale out)

Use Redis if
* You have advanced data types, such as lists, hashes, and sets
* You are doing data sorting and ranking (such as leader boards)
* Data persistence
* Multi AZ
* Pub / Sub capabilities are needed
