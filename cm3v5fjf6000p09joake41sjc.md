---
title: "SSA - C03 Certificate: Database in AWS"
datePublished: Sun Nov 24 2024 05:18:51 GMT+0000 (Coordinated Universal Time)
cuid: cm3v5fjf6000p09joake41sjc
slug: ssa-c03-certificate-database-in-aws
tags: aws

---

## RDS

* Managed PostgreSQL, MySQL, Oracle, SQL Server, DB2, MariaDB, Custom
    
* Provisioned RDS Instance Size and EBS Volume Type & Size
    
* Auto-scaling capability for Storage
    
* Support for Read Replicas and Multi-AZ (for HA and have a standby database)
    
* Security through IAM, Securities Groups, KMS, SSL in transit
    
* Automated Backup with Point in time restore feature (up to 35 days)
    
* Manual DB Snapshot for longer-term recovery
    
* Managed and Scheduled maintenance (with downtime)
    
* Support for IAM Authentication, integration with Secrets Manager
    
* RDS Custom for access to and customize the underlying instance (Oracle & SQL Server)
    

> Use cases: store relational datasets (RDMBS/OLTP), perform SQL queries, transactions

## Aurora

* Compatible API for PostgreSQL / MySQL, separation of storage and compute
    
* Storage: data is stored in 6 replicas, across 3 AZ - HA, self-healing, auto-scaling
    
* Compute: Cluster of DB Instance across multiple AZ, auto-scaling of Read Replicas
    
* Cluster: Custom endpoints for writer and reader DB instances
    
* Same security/monitoring/maintenance features as RDS
    
* Know the backup & restore options for Aurora
    
* **Aurora Serverless** - for unpredictable workloads
    
* **Aurora Global:** up to 16 DB Read Instances in reach region, &lt; 1 second storage replication
    
* **Aurora Machine Learning:** perform ML using SageMaker & Comprehend on Aurora
    
* **Aurora Database Cloning:** new cluster from existing one, faster than restoring a snapshot
    

> Use cases: same as RDS, but with less maintenance, more flexibility, more performance, more features

## ElastiCache

* Managed Redis / Memcached
    
* In-memory data store, sub-millisecond latency
    
* Support for Clustering (Redis) and Multi-AZ, Read Replicas (sharding)
    
* Security through IAM, Security Groups, KMS, Redis Auth
    
* Backup / Snapshot, Point in time restore feature
    
* Manage and Schedule maintenance
    
* **Requires some application code changes to be leveraged**
    

> Use cases: Key/Value store, frequent reads, less writes, cache results for DB queries, store session data for websites, cannot use SQL

## DynamoDB

* AWS proprietary technology, managed serverless NoSQL db, millisecond latency
    
* Capacity modes: provisioned capacity with optional auto-scaling or on-demand capacity
    
* Can replace ElastiCache as a key/value store
    
* HA, multi-AZ by default, Read and Writes are decoupled, transaction capability
    
* DAX cluster for read cache, microsecond read latency
    
* Security, authentication/author is done through IAM
    
* Event Processing: DynamoDB Streams to integrate with Lambda or Kinesis Data Streams
    
* Global Table feature: active-active setup
    
* Automated backups up to 35 days with PITR (point-in-time recovery), or on-demand backups
    
* Export to S3 without using RCU in the PITR window, import from S3 without using WCU
    
* It is great to evolve schemas rapidly
    
* Use case: serverless applications development (small document 100s KM), distributed serverless cache
    

## S3

* Great for bigger objects, not so great for many small objects
    
* Serverless, scales infinitely, max object size is 5 TB, version capability
    
* Tiers: S3 Standard, S3 IA, S3 Intelligent, S3 Glacier + lifecycle policy
    
* Features: versioning, encryption, replication, MFA-Delete, Access Logs,…
    
* Security: IAM, bucket policies, ACL, Access Points, Object Lambda, CORD, Object/Vault Lock
    
* Encryption: SSE-S3, SSE-KMS,…
    
* Batch operations on objects using S3 Batch, listing files using S3 Inventory
    
* Performance: Multi-part upload, S3 Transfer Acceleration, S3 Select
    
* Automation: S3 Event notifications (SNS, SQS, Lambda, EventBridge)
    

> Use cases: static files, key valuie store for big files, website hosting

## DocumentDB

* Is the same for MongoDB (like Aurora for MongoDB)
    
* Similar deployment concepts to Aurora
    
* Fully managed, HA with replication across 3 AZ
    
* DocumentDB storage automatically grows in increments of 10 GB
    
* Automatically scales to workloads with millions of requests per second
    

## Neptune

* Full-managed graph database
    
* A popular graph database would be a social network
    
* HA across 3 AZ, up to 15 read replicas
    
* Build and run applications working with highly connected datasets - optimized for these complex and hard queries
    
* Can store up to billions of relations and query the graph with milliseconds latency
    
* Great for knowledge graphs, fraud detection, recommendation engines, social networking
    
* Support for Streams (like Dynamo Data Streams)
    
    * Send notifications when certain changes are made
        
    * Maintain graph data synchronized in another data store (S3, OpenSearch,…)
        
    * Replicate data across regions in Neptune
        

## Keyspaces (for Apache Cassandra)

* Cassandra is an open-source NoSQL distributed database
    
* A managed Apache Cassandra-compatible database service
    
* Serverless, Scalable, HA, fully managed by AWS
    
* Automatically scale tables up/down based on the application’s traffic
    
* Tables are replicated 3 times across multiple AZ
    
* Using the Cassandra Query Language (CQL)
    
* 100s of requests per second
    
* Capacity: on-demand mode or provisioned mode with auto-scaling
    
* Encryption, backup, Point-In-Time recovery up to 35 days
    

> Use cases: store IOT devices info, time-series data,…

## Quantum Ledger Database

* A ledger is a book recording financial transactions
    
* Fully managed, serverless, HA, replication across 3 AZ
    
* Used to review the history of all the changes made to application data over time
    
* Immutable system: no entry can be removed or modified, cryptographically verifiable
    
* 2-3x better performance than common ledger blockchain frameworks, manipulate data using SQL
    

## TimeStream

* Full-managed, fast, scalable, serverless time series database
    
* Automatically scales up/down to adjust capacity
    
* Store and analyze trillions of events per day
    
* 100s time faster & 1/10 the cost of relational databases
    
* Scheduled queries, multi-measure records, SQL compatibility
    

> Use cases: IoT apps, operatinal applications, real-time analytics,…