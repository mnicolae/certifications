# Introduction to DynamoDB

## What is DynamoDB?

`Amazon DynamoDB` is a fast and flexible NoSQL database service for all applications that need consistent, single-digit millisecond latency at any scale.

It is a fully managed database and supports both document and key-value data models.

Its flexible data model and reliable performance make it a great fit for mobile, web, gaming, ad-tech, IoT, and many other applications.

## DynamoDB

* Stored on SSD storage.
* Spread across 3 geographically distinct data centers.
* Choice of 2 consistency models: Eventual Consistent Reads (Default), Strongly Consistent Reads

Eventually Consistent Reads:
* Consistency across all copies of data is usually reached within a second. Repeating a read after a short time should return the updated data. (Best Read Performance)

Strongly Consistent Reads:
* A strongly consistent read returns a result that reflects all writes that received a successful response prior to the read.

## DynamoDB

* Tables
* Items (Think a row of data in a table)
* Attributes (Think a column of data in a table)
* Supports key-value and document data structures
* Key = The name of the data, Value = the data itself
* Documents can be written in JSON, HTML or XML

## DynamoDB - Primary Keys

* DynamoDB stores and retrieves data based on a Primary Key
* 2 types of Primary Key
* `Partition Key` - unique attribute (e.g., user ID)
* Value of the Partition Key is input to an internal hash function which determines the partition or physical location on which the data is stored.
* If you are using the Partition Key as your PK, then no two items can have the same Partition Key.
* `Composite Key` - (`Partition Key` + `Sort Key`) in combination
* e.g., same user posting multiple times to a forum
* PK would a be a Composite Key consisting of: Partition Key - User ID + Sort key - timestamp of the posting
* 2 items may have the same partition key, but they must have a different sort key
* All items with the same partition key are stored together, then sorted according to the sort key value
* Allows you to store multiple items with the same partition key.

## DynamoDB Access Control

* Authentication and Access Control is managed using AWS IAM.
* You can create an IAM user within your AWS account which has specific permissions to access and create DynamoDB tables.
* You can create an IAM role which enables you to obtain temporary access key which can be used to access DynamoDB.
* You can also use a special `IAM Condition` to restrict user access to only their own records.

## DynamoDB Exam Tips

* Amazon DynamoDB is a low latency NoSQL database.
* Consists of Tables Items and Attributes
* Supports both document and key-value data models.
* Supported document formats are JSON, HTML, XML.
* 2 types of Primary Key - Partition Key and combination of Partition Key + Sort Key (Composite Key)
* 2 Consistency models: Strongly Consistent / Eventually Consistent.
* Access is controlled using IAM policies.
* Fine grained access control using IAM condition parameter: `dynamodb:LeadingKeys` to allow users to access only the items where the partition key value matches their user ID.

# Indexes deepdive

In SQL databases, an index is a data structure which allows you to perform fast queries on specific columns in a table. You select the columns that you want included in the index and run your searches on the index - rather than on the entire dataset.

In DynamoDB, 2 types of index are supported to help speed-up your DynamoDB queries:
* Local Secondary Index
* Global Secondary Index

## Local Secondary Index

* Can only be created when you are creating your table
* You cannot add, remove, or modify it later
* It has the same Partition Key as your original table
* But a different Sort Key
* Gives you a different view of your data, organized according to an alternative Sort Key
* Any queries based on this Sort Key are much faster using the index than the main table
* e.g., partition key: user id, sort key: account creation date

## Global Secondary Index

* You can create when you create your table, or add it later
* Different Partition Key as well as a Different Sort Key
* So gives a completely different view of the data
* Speeds up any queries relating to this alternative partition and sort key
* e.g. partition key: email address, sort key: last log-in date

## DynamoDB Indexes - Exam Tips

* Indexes enable fast queries on specific data columns.
* Give you a different view of your data, based on alternative Partition / Sort Keys.
* Important to understand the differences

| Local Secondary Index | Global Secondary Index |
|---|---|
| Must be created when you create your table | Can create any time - at table creation or after |
| Same Partition Key as your table | Different Partition Key |
| Different Sort Key | Different Sort Key

# Scan vs. Query API call

## What is a Query?

* A Query operation finds items in a table based on thee Primary Key attribute and a distinct value to search for.
* e.g., select an item where the user ID is equal to 212, will select all the attributes for that item, e.g. first name, surname, email, etc.

## What is a Query?

* Use an optional Sort Key name and value to refine the results.
* e.g. if your Sort Key is a timestamp, you can refine the query to only select items with a timestamp of the last 7 days.
* By default, a Query returns all the attributes for the items but you can use the `ProjectionExpression` parameter if you want the query to only return the specific attributes you want.
* e.g., if you only want to see the email address rather than all the attributes

## What is a Query?

* Results are always sorted by the Sort Key
* Numeric order - by default in ascending order (1, 2, 3, 4)
* ASCII character code values
* You can reverse the order by setting the `ScanIndexForward` parameter to false
* By default, Queries are Eventually Consistent
* You need to explicitly set the query to be Strongly Consistent

## What is a Scan?

* A `Scan` operation examines every item in the table.
* By default returns all data attributes.
* Use the `ProjectionExpression` parameter to refine the scan to only return the attributes you want.

## Query or Scan?

* Query is more efficient than a Scan.
* Scan dumps the entire table, then filters out the values to provide the desired result - removing the unwanted data.
* This adds an extra step of removing the data you don't want.
* As the table grows, the scan operation takes longer.
* Scan operation on a large table can use up the provisioned throughput for a large table in just a single operation.

## How To Improve Performance

* You can reduce the impact of a query or scan by setting a smaller page size which uses fewer read operations.
* e.g., set the page size to return 40 items.
* Large number of smaller operations will allow other requests to succeed without throttling.
* Avoid using scan operations if you can: design tables in a way that you can use Query, Get, or BatchGetItem APIs.

## How To Improve Scan Performance

* By default, a scan operation processes data sequentially in returning 1MB increments before moving on to retrieve the next 1MB of data. It can only scan one partition at a time.
* You can configure DynamoDB to use Parallel scans instead by logically dividing a table or index into segments and scanning each segment in parallel.
* Best to avoid parallel scans if your table or index is already incurring heavy read / write activity from other applications.

## Scan Vs. Query Exam Tips

* A Query operation finds items in a table using only the Primary Key attribute.
* You provide the Primary Key name and a distinct value to search for.
* A Scan operation examines every item in the table.
* By default returns all data attributes.
* Use the `ProjectionExpression` parameter to refine the results.
* Query results are always sorted by the Sort Key if there is one.
* Sorted in ascending order.
* Set `ScanIndexForward` parameter to false to reverse the order - queries only.
* Query operation is generally more efficient than a Scan.
* Reduce the impact of a query or scan by setting a smaller page size which uses fewer read operations.
* Isolate scan operations to specific tables and segregate them from your mission-critical traffic.
* Try Parallel scans, rather than the default sequential scan.
* Avoid using scan operations if you can: design tables in a way that you can use the Query, Get, or BatchGetItem APIs.

# DynamoDB Provisioned Throughput

## DynamoDB Read and Write Capacity Units

* DynamoDB Provisioned Throughput is measured in Capacity Units.
* When you create your table, you specify your requirements in terms of Read Capacity Units and Write Capacity Units.
* 1 x Write Capacity Unit = 1 x 1KB Write per second
* 1 x Read Capacity Unit = 1 x Strongly Consistent Read of 4KB per second OR 2 x Eventually Consistent Reads of 4KB per second (Default)

## DynamoDB Example Configuration

* Table with 5 x Read Capacity Units and 5 x Write Capacity Units
* This configuration will be able to perform:
* 5 x 4KB Strongly Consistent Reads = 20KB per second
* Twice as many Eventually Consistent = 40KB
* 5 x 1KB writes = 5KB per second

* If you application reads or writes larger items it will consume more capacity units and will cost you more as well.

## Strongly Consistent Reads Calculation

* Your application needs to read 80 items (table rows) per second.
* Each item 3KB in size.
* You need Strongly Consistent Reads.

* First, calculate how many read capacity units needed for each read: size of each item / 4KB. 3 KB / 4 KB = 0.75
* Rounded-up to the nearest whole number, each read will need 1 x Read Capacity Unit per read operation.
* Multiplied by the number of reads per second = 80 Read Capacity Units required.

## Eventually Consistent Reads Calculation

* What if you need Eventually Consistent Reads?
* You do the same calculation. However as this is for Eventually Consistent reads and you get 2 x 4KB reads per second - or *double* the throughput of Strongly Consistent reads.

* Size of each item / 4KB.
** 3KB / 4KB = 0.75 round up to the nearest whole number, = 1
** Multiply by the number of reads per second = 80

* Divide 80 by 2, so you only need 40 Read Capacity Units for Eventually Consistent reads.

## Write Capacity Units Calculation

* You want to write 100 items per second.
* Each item 512 bytes in size.

* First, calculate how many Capacity Units for each write: size of each item / 1 KB (for write capacity units)
* 512 bytes / 1 KB = 0.5
* Rounded-up to the nearest whole number, each write will need 1 x Write Capacity Unit per write operation.
* Multiplied by the number of writes per second = 100 Write Capacity Units required.

## DynamoDB Provisioned Throughput Exam Tips

* Provisioned Throughput is measured in Capacity Units.
* 1 x Write Capacity Unit = 1 x 1KB Write per second.
* 1 x Read Capacity Unit = 1 x 4KB Strongly Consistent Read OR 2 x 4KB Eventually Consistent Reads per second.

# DynamoDB On-Demand Capacity

* Charges apply for: Reading, Writing and Storing data
* With On-Demand, you don't need to specify your requirements
* DynamoDB instantly scales up and down based on the activity of your application
* Great for unpredictable workloads
* You want to pay for only what you use (pay per request)

## Which Pricing Model Should I Use?

| On-Demand Capacity | Provisioned Capacity |
|---|---|
| Unknown workloads | You can forecast read and write capacity requirements
| Unpredictable application traffic | Predictable application traffic
| You want a Pay-Per-Use model | Application traffic is consistent or increases gradually.
| Spiky, short lived peaks

# DynamoDB Accelerator (DAX)

## What is DAX?

* DynamoDB Accelerator (or DAX) is a fully managed, clustered in-memory cache for DynamoDB.

* Delivers up to a 10x read performance improvement
* Microsecond performance for millions of requests per second
* Ideal for Read-Heavy and bursty workloads
* e.g., auctions applications, gaming and retail sites during Black Friday promotions

## How Does it Work?

* DAX is a write-through caching service - this means data is written to the cache as well as the back end store at the same time.
* Allows you point your DynamoDB API calls at the DAX cluster
* If the item you are querying is in the cache (cache hit), DAX returns the result to the application.

## How Does it Work?

* If the item is not available (cache miss) then DAX performs an Eventually Consistent GetItem operation against DynamoDB
* Retrieval of data from DAX reduces the read load on DynamoDB tables.
* May be able to reduce Provisioned Read Capacity

## What is it NOT Suitable For?

* Caters for Eventually Consistent reads only - so not suitable for applications that require Strongly Consistent reads
* Write intensive applications
* Applications that do not perform many read operations
* Applications that do not require microsecond response times

## DAX Exam Tips

* Provides in-memory caching for DynamoDB tables
* Improves response times for Eventually Consistent reads only
* You point your API calls to the DAX cluster, instead of your table.
* If the item you are querying is on the cache, DAX will return it; otherwise it will perform an Eventually Consistent GetItem operation to your DynamoDB table.
* Not suitable for write-intensive applications or applications that require Strongly Consistent reads.

# Elasticache

* `Elasticache` - in memory cache in the cloud
* Improves performance of web applications, allowing you to retrieve information from fast in-memory caches rather than slower disk based databases
* Sits between your application and the database:
* e.g., an application frequently requesting specific product information for your best selling products
* Takes the load off your database
* Good if your database is particularly **read-heavy** and the data is not changing frequently.

## Elasticache Benefits and Use Cases

* Improves performance for read-heavy workloads
* e.g., Social Networking, gaming media sharing, Q&A portals
* Frequently-accessed data is stored in memory for low-latency access, improving the overall performance of your application.
* Also good for compute heavy workloads
* e.g., recommendation engines
* Can be used to store results of I/O intensive database queries or output of compute-intensive calculations.

## 2 Types of Elasticache

* Memcached
* Widely adopted memory object caching system
* Multi-threaded
* No multi-AZ capability

* Redis
* Open-source in-memory key-value store
* Supports more complex data structures: sorted sets and lists
* Supports Master / Slave replication and multi-AZ for cross AZ redundancy

## Caching Strategies

* 2 strategies available: `Lazy Loading` and `Write-Through`:
* `Lazy Loading` - Loads the data into the cache only when necessary
* If requested data is in the cache, Elasticache returns the data to the application.
* If the data is not in the cache or has expired, Elasticache returns a null.
* Your application then fetches the data from the database and writes the data received into the cache so that it is available next time.

## Lazy Loading Advantages and Disadvantages

| Advantages | Disadvantages |
|---|---|
| Only requested data cached: avoids filling up cache with useless data | Cache miss penalty
| Node failures are not fatal | Stale data - if data is only updated when there is a cache miss, it can become stale.

## Lazy Loading and TTL

* `TTL (Time To Live)`
* Specifies the number of seconds until the key (data) expires to avoid keeping stale data in the cache
* Lazy Loading treats an expired key as a cache miss and causes the application to retrieve the data from the database and subsequently write the data into the cache with a new TTL
* Does not eliminate stale data - but helps to avoid it

## Write-Through Advantages and Disadvantages

* `Write-Through` - adds or updates data to the cache whenever data is written to the database

| Advantages | Disadvantages |
|---|---|
| Data in the cache is never stale | Write penalty |
| Users are generally more tolerant of additional latency when updating data than when retrieving it | If a node fails or a new one is spun up, data is missing until added or updated in the database |
| | Wasted resources if most of the data is never read |

## Elasticache Exam Tips

* In-memory cache sits between your application and database
* 2 different caching strategies: Lazy Loading and Write Through

* Lazy Loading strategy only caches the data when it is requested
* Elasticache Node failures not fatal, just lots of cache misses
* Cache miss penalty: Initial request, query database, writing to cache
* Avoid stale data by implementing a TTL

* Write Through strategy writes data into the cache whenever there is a change to the database
* Data is never stale
* Write penalty: each write involves a write to the cache
* Elasticache node failure means that data is missing until added or updated in the database
* Wasted resources if most of the data is never used.

# DynamoDB Transactions

`DynamoDB Transactions`:
* ACID Transactions (Atomic, Consistent, Isolated, Durable)
* Read or write multiple items across multiple tables as an all or nothing operation
* Check for a pre-requisite condition before writing to a table

# DynamoDB TTL

`DynamoDB TTL`
* Time to Live attribute defines an expiry time for your data
* Expired items marked for deletion
* Great for removing irrelevant or old data: session data, event logs, temporary data
* Reduces cost by automatically removing data which is no longer relevant

# DynamoDB Streams

`DynamoDB Streams`
* Time-ordered sequence of item level modifications (insert, update, delete)
* Logs are encrypted at rest and stored for 24 hours
* Accessed using a dedicated endpoint
* By default the Primary Key is recorded
* Before and After images can be captured

## Processing DynamoDB Streams

* Events are recorded in near real-time
* Applications can take actions based on contents
* Event source for lambda
* Lambda polls the DynamoDB stream
* Executes Lambda code based on a DynamoDB Streams event

## DynamoDB Streams Exam Tips

* Time-ordered sequence of item level modifications in your DynamoDB Tables
* Data is stored for 24 hours only
* Can be used as an event source for Lambda so you can create applications which take actions based on events in your DynamoDB table

# Provisioned Throughput Exceeded Exception & Exponential Backoff

## Provisioned Throughput Exceeded Exception

* `ProvisionedThroughputExceededException`
* Your request rate is too high for the read / write capacity provisioned on your DynamoDB table.
* SDK will automatically retry the request until successful
* If you are not using the SDK you can: reduce request frequency, use exponential backoff

## What is Exponential Backoff?

* Many components in a network can generate errors due to being overloaded
* In addition to simple retries all AWS SDKs use `Exponential Backoff`
* Progressively longer waits between consecutive retries e.g., 50 ms, 100 ms, 200 ms ... for improved flow control
* If after 1 minute this doesn't work, your request size may be exceeding the throughput for your read / write capacity

# DynamoDB - Summary

## DynamoDB - Exam Tips

* Amazon DynamoDB is a low latency NoSQL database.
* Consists of Tables Items and Attributes
* Supports both document and key-value data models.
* Supported document formats are JSON, HTML, XML.
* 2 types of Primary Key - Partition Key and combination of Partition Key + Sort Key (Composite Key)
* 2 Consistency models: Strongly Consistent / Eventually Consistent.
* Access is controlled using IAM policies.
* Fine grained access control using IAM condition parameter: `dynamodb:LeadingKeys` to allow users to access only the items where the partition key value matches their user ID.

## DynamoDB Indexes - Exam Tips

* Indexes enable fast queries on specific data columns.
* Give you a different view of your data, based on alternative Partition / Sort Keys.
* Important to understand the differences

| Local Secondary Index | Global Secondary Index |
|---|---|
| Must be created when you create your table | Can create any time - at table creation or after |
| Same Partition Key as your table | Different Partition Key |
| Different Sort Key | Different Sort Key

## Scan Vs. Query Exam Tips

* A Query operation finds items in a table using only the Primary Key attribute.
* You provide the Primary Key name and a distinct value to search for.
* A Scan operation examines every item in the table.
* By default returns all data attributes.
* Use the `ProjectionExpression` parameter to refine the results.
* Query results are always sorted by the Sort Key if there is one.
* Sorted in ascending order.
* Set `ScanIndexForward` parameter to false to reverse the order - queries only.
* Query operation is generally more efficient than a Scan.
* Reduce the impact of a query or scan by setting a smaller page size which uses fewer read operations.
* Isolate scan operations to specific tables and segregate them from your mission-critical traffic.
* Try Parallel scans, rather than the default sequential scan.
* Avoid using scan operations if you can: design tables in a way that you can use the Query, Get, or BatchGetItem APIs.

## DynamoDB Provisioned Throughput - Exam Tips

* Provisioned Throughput is measured in Capacity Units.
* 1 x Write Capacity Unit = 1 x 1KB Write per second.
* 1 x Read Capacity Unit = 1 x 4KB Strongly Consistent Read OR 2 x 4KB Eventually Consistent Reads per second.

## DAX Exam Tips

* Provides in-memory caching for DynamoDB tables
* Improves response times for Eventually Consistent reads only
* You point your API calls to the DAX cluster, instead of your table.
* If the item you are querying is on the cache, DAX will return it; otherwise it will perform an Eventually Consistent GetItem operation to your DynamoDB table.
* Not suitable for write-intensive applications or applications that require Strongly Consistent reads.

## Elasticache Exam Tips

* In-memory cache sits between your application and database
* 2 different caching strategies: Lazy Loading and Write Through

* Lazy Loading strategy only caches the data when it is requested
* Elasticache Node failures not fatal, just lots of cache misses
* Cache miss penalty: Initial request, query database, writing to cache
* Avoid stale data by implementing a TTL

* Write Through strategy writes data into the cache whenever there is a change to the database
* Data is never stale
* Write penalty: each write involves a write to the cache
* Elasticache node failure means that data is missing until added or updated in the database
* Wasted resources if most of the data is never used.
