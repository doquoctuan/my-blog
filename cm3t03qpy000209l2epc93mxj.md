---
title: "SAA - C03 Certification: Serverless"
datePublished: Fri Nov 22 2024 17:14:10 GMT+0000 (Coordinated Universal Time)
cuid: cm3t03qpy000209l2epc93mxj
slug: saa-c03-certification-serverless
tags: aws

---

## Lambda Function

### Limits

* Execution:
    
    * Memory allocation: 120 MB - 10 GB
        
    * Maximum execution time: 900 seconds (15 minutes)
        
    * Environment variables (4 KB)
        
    * Concurrency executions: 1000 (can be increased)
        
    * Disk capacity (in /tmp): 512 MB to 10 GB
        
* Deployment:
    
    * Lambda function deployment size (compressed .zip): 50 MB
        
    * Size of uncompressed deployment: 250 MB
        
    * You can use the /tmp directory to load other files at startup
        
    * Size of environment variable: 4 KB
        

### Lambda SnapStart

* Improves Lambda functions performance up to 10x at no extra cost for Java 11 and above
    
* When enabled, the function is invoked from a pre-initialized state
    
* When you publish a new version:
    
    * Lambda initialize function
        
    * Takes a snapshot of memory and disk state of the initialize function
        
    * Snapshot is cached for low-latency access
        

### Customization at the Edge

* Edge Function:
    
    * A code that you write and attach to CloudFront
        
    * Run close to your users to minimize latency
        
* CloudFront provides two types: **CloudFont Functions & Lambda Edge**
    
* Use case: customize the CDN content
    
* Pay only for what you use
    
* Fully serverless
    

#### Some use-cases

* Website Security and Privacy
    
* Dynamic web application at the Edge
    
* SEO
    
* Intelligently Route Across Origins and Data Centers
    
* Bot mitigation at the Edge
    
* Real-time Image Transformation
    
* A/B Testing
    
* Use Authen/Author
    
* User Tracking and Analytics
    

#### CloudFront Functions

* Lightweight functions written in JavaScript
    
* Sub-ms startup times, millions of requests/second
    
* Used to change **Viewer requests** and **Viewer responses**
    
* Native feature of CloudFront (manage code directly in CloudFront)
    
* Use cases: **cache key normalization** (transform request attributes to create an optimal Cache key), **insert/modify/delete HTTP headers**, **URL rewrites** or **redirects**, **generate**
    

* **and validate user-generated tokens** (e.g. JWT) to allow/deny requests
    

#### Lambda Edge

* Lambda functions written in NodeJS or Python
    
* Scales to 1000s of requests/second
    
* Used to change CloudFront requests CloudFront and responses to the origin
    
* Author your functions in one AWS region (us-east-1) then CloudFront replicates to its locations
    
* Use cases: Longer execution time, code depends on a 3rd library, network access to use external services for processing, file system access or access to the body of HTTP requests
    

### Lambda in VPC

By default, the Lambda function is launched outside VPC, therefore, it cannot access resources in VPC (RDS, ElastiCache, internal ELB,…)

#### Solutions

* Defint the VPC ID, the Subnets and Security Groups
    
* Lambda will create an ENI (Elastic Network Interface) in a subnet
    

#### Lambda with RDS Proxy

* To reduce the workload when lots of lambda functions directly access the database =&gt; using **RDS Proxy**
    
* RDS Proxy
    
    * Improve scalability by pooling and sharing DB connections
        
    * Improve availability by reducing by 66% the failover time and preserving connections
        
    * Improve security by enforcing IAM authentication and storing credentials in Secrets Manager
        

> The Lambda Function must be deployed in VPC, because RDS Proxy is never publicly accessible

## Amazon DynamoDB

* NoSQL - with transaction support
    
* Scales to massive workload, distributed database
    
* Millions of requests per second, trillions of rows, 100s of TB of storage
    
* Fast and consistent in performance
    
* Low-cost and auto-scaling capabilities
    
* There is no maintenance or patching. It is always available
    
* Standard & Infrequent Access (IA) Table Class
    

### Basics

* Each table has a Primary Key that needs to be defined when creating it
    
* Each table can have an infinite number of items
    
* Each item has attributes (can be added over time - can be null)
    
* The maximum size of an item is 400 KB
    
* Data types supported are:
    
    * Scalar Types - String, Number, Binary, Boolean, Null
        
    * DocumentTypes - List, Map
        
    * SetTypes - String Set, Number Set, Binary Set
        

### Read/Write Capacity Modes

**Provisioned Mode (default)**

* You specify the number of reads/writes per second
    
* You need to plan capacity beforehand
    
* Pay for provisioned Read Capacity Units (RCU) & Write Capacity Units (WCU)
    
* Possibility to add auto-scaling mode for RCU & WCU
    

**On-Demand Mode**

* Read/writes automatically scale up/down with your workload
    
* No capacity planning is needed
    
* Pay for what you use, more expensive
    
* Great for **unpredictable** workloads
    

### DynamoDB Accelerator (DAX)

* Help solve read congestion by caching
    
* Microseconds latency for cached data
    
* Doesn’t require application logic modification (compatible with existing DynamoDB APIs)
    
* 5 minutes TTL for cache (default)
    

### Stream Processing

* Ordered stream of item-level modifications (create/update/delete) in a table
    
* Use cases:
    
    * React to change in real-time
        
    * Real-time usage analytics
        
    * Insert into derivative tables
        
    * Implement cross-region replication
        
    * Invoke AWS Lambda on changes to your DynamoDB table
        
* The characteristics of DynamoDB Streams:
    
    * 24 hours retention
        
    * Limited # of consumers
        
    * Process using AWS Lambda Triggers or Dynamoc DB Stream Kinesis adapter
        
* The characteristics of Kinesis Data Streams (newer):
    
    * 1-year retention
        
    * High # of consumers
        
    * Process using AWS Lambda, Kinesis Data Analytics, Kinesis Data Firehose, AWS Glue Streaming ETLs,...
        

### Global Tables

* Make a DynamoDB table accessible with low latency in multiple regions
    
* Active-Active replication
    
* Applications can **READ** and **WRITE** to the table in any region
    
* Must enable **DynamoDB Stream** as a pre-requisite
    

### Time To Live

* Automatically delete items after an expiry timestamp
    

### Backups for disaster recovery

* Continuous backups using point-in-time recovery (PITR)
    
    * Optionally enabled for the last 35 days
        
    * Point-in-time recovery to any time in the backup window
        
    * The recovery process creates a new table
        
* On-demand backups
    
    * Full backups for long-term retention, until explicitly deleted
        
    * It does not affect performance or latency
        
    * Can be configured and managed in AWS Backup (enables cross-region copy)
        
    * The recovery process creates a new table
        

### Integration with S3

* Export to S3 (must enable PITR)
    
    * It does not affect the reading capacity of the table
        
    * Perform data analysis on top of DynamoDB
        
    * Retain snapshots for auditing
        
    * ETL on top of S3 data before importing back into DynamoDB
        
    * Export in DynamoDB Json or ION format
        
* Import from S3
    
    * Import CSV, DynamoDB Json, or ION format
        
    * It does not consume any writing capacity
        
    * Creates a new table
        
    * Import errors are logged in CloudWatch
        

## API Gateway

* AWS Lambda + API Gateway: no infra to manage
    
* Support for the Websocket
    
* Handle API versioning
    
* Handle different environments
    
* Handle security (authen/author)
    
* Create API keys, handle request throttling
    
* Swagger/Open API import to quickly define APIs
    
* Transform and validate requests and responses
    
* Cache API responses
    
* Generate SDK and API specifications
    
* **Endpoint Types:**
    
    * **Edge-Optimized (default)**: for global clients
        
        * Requests are routed through the CloudFront Edge locations
            
        * The API gateway still lives in only one region
            
    * **Regional**
        
        * For clients in the same region
            
        * Could manually combine with CloudFront
            
    * **Private**
        
        * Can only be accessed from VPC using **VPC Endpoint** (ENI)
            
        * Use a resource policy to define access
            

## AWS Step Functions

* Build serverless visual workflow to orchestrate Lambda functions
    
* Features: sequence, parallel, conditions, timeouts, error handling,…
    
* Can integrate with EC2, ECS, On-premises servers, API Gateway, SQS,…
    
* Possibility of implementing a human approval feature
    
* Use cases: order fulfillment, data processing, web app, any workflow,…
    

## Amazon Cognito

* Give users an identity to interact with web or mobile app
    
* **Cognito User Pools**:
    
    * Sign-in functionality for app users
        
    * Integrate with API gateway & ALB
        
* **Cognito Identity Pools** (Federated Identity)
    
    * Provide AWS credentials to users so they can access AWS resources directly
        
    * Integrate with Cognito User Pools as an identity provider
        

### Cognito User Pools (CUP)

#### User Features

* Create a serverless database of users for web & mobile app
    
* Simple login: username/password
    
* Password reset
    
* Email & phone number verification
    
* MFA
    
* Federated Identities: users from Fb, Google, SAML,…
    

#### Integrations

* CUP integrates with API Gateway and ALB
    

#### Federated Identities

* Get identities for “users” so they obtain temporary AWS credentials
    
* Users can then access AWS services directly or through API Gateway