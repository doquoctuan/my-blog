---
title: "SSA - C03 Certification: SQS, SNS, Kinesis"
datePublished: Wed Nov 20 2024 09:51:51 GMT+0000 (Coordinated Universal Time)
cuid: cm3ppf7ar000k09l182wwekbr
slug: ssa-c03-certification-sqs-sns-kinesis
tags: aws

---

## Amazon SQS

### Standard Queue

#### Attributes

* **Unlimited throughput**, **unlimited number of messages in queue**
    
* Default retention of messages: 4 days, maximum of 14 days
    
* Low latency (**&lt; 10 ms** on publish and receive)
    
* Limitation of 256 KB per message sent
    

Can **have duplicate messages** (at least once delivery)  
Can **have out-of-order messages**

#### Producing Messages

* Produced to SQS using the SDK (**SendMessage** API)
    
* The message persists in SQS until a consumer deletes it
    
* Message retention: default 4 days, up to 14 days
    

#### Consuming Messages

* Consumers (EC2, Lambda, Servers,…)
    
* Poll SQS for messages (receive up to 10 messages at a time)
    
* Delete the messages using the **DeleteMessage** API
    

#### Securities

* **Encryption**
    
    * In-flight encryption using HTTPS API
        
    * At-rest encryption using KMS keys
        
    * Supporting client-side encryption
        
* **Access Controls**: IAM Policies
    
* **SQS Access Policies** (similar to S3 bucket policies)
    
    * Useful for cross-account access to SQS
        
    * Useful for allowing other services (SNS, S3,…) to write to an SQS
        

#### Long Polling

Where a consumer requests messages from the queue, it can optionally “wait” for messages to arrive if there are none in the queue =&gt; **This is called Long Polling**

Long Polling **decreases the number of API calls** made to SQS while increasing the **efficiency and reducing** latency for application

The wait time can be between 1 sec to 20 sec

Long Polling is preferable to Short Polling

It can be enabled at the queue level or the API level (**WaitTimeSeconds** API)

### FIFO Queue

* Limit throughput: 300 msg/s without batching, 3000 msg/s with batching
    
* Exactly-once-send capability (by removing duplicates)
    
* Messages are processed in order by the consumers
    

## Amazon SNS

* Up to 12,500,000 subscriptions per topic
    
* 100,000 topics limit
    

Many services send data directly to SNS for notifications such as:  
CloudWatch, AWS Budgets, Lambda, Auto Scaling Group, S3, DynamoDB, CloudFormation, AWS DMS, RDS Events,…

### SNS + SQS: Fan out

* Push once in SNS, receive in all SQS queues
    
* Fully decoupled, no data loss
    
* SQS allows for data persistence, delayed processing, and retries of work
    
* Ability to add more SQS subscribers over time
    
* Make sure the SQS queue access policy allows for SNS to write
    
* Cross-Region Delivery: works with SQS in other regions
    

### SNS - FIFO Topic

* Similar features as SQS FIFO:
    
    * Ordering by Message Group ID
        
    * Deduplication using a Deduplication ID or Content-Based Deduplication
        
* Can have SQS Standard or SQS FIFO as subscribers
    
* Limit throughput: 300 msg/s without batching, 3000 msg/s with batching
    

### SNS - Message Filtering

* JSON policy used to filter messages sent to SNS topic’s subscriptions
    
* If a subscription does not have a filter policy, it receives every message
    

## Kinesis

### Overview

* Make it easy to collect, process, and analyze streaming data in real-time
    
* Ingest real-time data such as Application Logs, Metrics, Website, clickstreams, IoT telemetry data,…
    
* Kinesis Data Streams: capture, process, and store data streams
    
* Kinesis Data Firehose: load data streams into AWS data stores
    
* Kinesis Data Analytics: analyze data streams with SQL or Apache Flink
    
* Kinesis Video Streams: capture process and store video streams
    

### Kinesis Data Streams

* Retention between 1 day to 365 days
    
* Once data is inserted in Kinesis, it can not be deleted
    
* Ability to reprocess data
    
* Data that share the same partition go to the same shard
    

#### Capacity Modes

* **Provisioned** mode:
    
    * You choose the number of shards provisioned, Salce manually or using API
        
    * Each shard gets 1MB/s in (or 1000 records per second)
        
    * Each shard gets 2MB/s out
        
    * You pay per shard provisioned per hour
        
* **On-demand** mode:
    
    * No need to provision or manage the capacity
        
    * Default capacity provisioned (4MB/s or 4000 records per second)
        
    * Scales automatically based on observed throughput peaks during the last 30 days
        
    * Pay per stream per hour & data in/out per GB
        

#### Security

* Control access/authorization using IAM policies
    
* Encryption in flight using HTTPS
    
* Encryption at rest using KMS
    
* Supporting encrypt/decrypt at the client side
    
* VPC endpoints for Kinesis to access in VPC
    
* Monitor API calls using CloudTrail
    

### Kinesis Data Firehose

* Fully managed service, automatic scaling, serverless
    
    * AWS: Redshift, S3, OpenSearch,…
        
    * 3rd party: MongoDB, DataDog,…
        
    * Custom: send to any HTTP endpoint
        
* Pay for data going through Firehose
    
* Near real-time
    
    * Buffer interval: 0 seconds to 900 seconds
        
    * Buffer size: minimum 1MB
        
* Supports many data formats, conversions, transformations, compression
    
* Support custom data transformations using Lambda
    
* Can send failed or all data to a backup S3 bucket
    

The comparison table between **Data Stream** and **Firehose**

| **Data Streams** | **FireHose** |
| --- | --- |
| Real-time (~200ms) | Near real-time |
| Manage scaling | Automatic scaling |
| Data storage for 1 to 365 days | No data storage |
| Supports replay capability | It does not support replay capability |
| Write custom code (producer/consumer) | Fully managed |