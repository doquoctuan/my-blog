---
title: "SAA - C03 Certification: CloudWatch, CloudTrail and Config"
datePublished: Tue Nov 26 2024 08:41:19 GMT+0000 (Coordinated Universal Time)
cuid: cm3y7jmb4000r09mnemrzc7cj
slug: saa-c03-certification-cloudwatch-cloudtrail-and-config
tags: aws

---

## CloudWatch

### Metrics

* Provides metrics for every service in AWS
    
* Metrics belong to **namespaces**
    
* Dimension is an attribute of a metric (instance id, environment,…)
    
* Up to 30 dimensions per metric
    
* Metrics have **timestamps**
    
* Can create CloudWatch dashboards of metrics
    
* Can create **Custom Metrics**
    

### Metric Streams

* Continually stream CloudWatch metrics to a destination, with near-real-time delivery and low latency
    
    * Amazon Kinesis Data Firehose
        
    * 3rd party service provider: **Datadog**, **Sumo Logic**,…
        

### Logs

* Log groups: arbitrary name, usually representing an application
    
* Can define log expiration policies (never expire, 1 day to 10 years,…)
    
* CloudWatch Logs can send logs to:
    
    * S3 (export)
        
    * Kinesis Data Streams/Firehose
        
    * Lambda
        
    * OpenSearch
        
* Logs are encrypted by default
    
* Can set KMS-based encryption with own keys
    

##### Logs - Sources

* SDK, CloudWatch Logs Agent, CloudWatch Unified Agent
    
* Elastic Beanstalk, ECS, Lambda, VPC Flow Logs, API Gateway, CloudTrail, Route53
    

#### Logs Insights

* Search and analyze log data stored in CloudWatch Logs
    
* Example: find a specific IP inside a log,…
    
* Provides a purpose-built query language
    
    * Automatically discovers fields from AWS Services and JSON log events
        
    * Can save queries and add them to **CloudWatch Dashboards**
        
* Can query multiple Log Groups in different AWS Accounts
    
* It’s a query engine, not a real-time engine
    

#### S3 Export

* Log data can take up to 12 hours to become available for export
    
* The API call is **CreateExportTask**
    
* Not near-real-time or real-time,… use **Logs Subscription** instead
    

#### Logs Subscriptions

* Get real-time log events from CloudWatch Logs for processing and analysis
    
* Send to Kinesis Data Streams/Firehose or Lambda
    
* **Subscription Filter**
    

### CloudWatch Unified Agent

* Collected Linux server / EC2 instance directly
    
* CPU
    
* Disk metrics
    
* RAM
    
* Netstat
    
* Processes
    
* Swap Space
    
* Reminder: out-of-the-box metrics for EC2 - disk, CPU, network (high level)
    

### CloudWatch Alarm

* Used to trigger notifications for any metric
    
* Various options (sampling, %, max, min, etc,…)
    

Alarm States:

* OK
    
* INSUFFICIENT\_DATA
    
* ALARM
    

### Alarm Target

* Stop, Terminate, Reboot or Recover an EC2 Instance
    
* Trigger Auto Scaling Action
    
* Send notification to **SNS**
    

### Composite Alarms

* CloudWatch Alarms are on a single metric
    
* Composite Alarms monitor the states of multiple other alarms
    
* **AND** and **OR** conditions
    

### Good to know

* Alarms can be created based on CloudWatch Logs Metrics Filters
    
* To test alarms and notifications, set the alarm state to Alarm using CLI
    
* ```bash
    aws cloudwatch set-alarm-state --alarm-name "myalarm" --state-value ALARM --state-reason "testing purpose"
    ```
    

## EventBridge (formerly CloudWatch Events)

* Schedule: Cron jobs
    
* Event pattern: event rules to react to a service doing something
    
* Trigger Lambda function, send SQS/SNQ messages,…
    

## CloudWatch Container Insights

* Collect, aggregate, and summarize metrics and logs from containers
    
* Available for containers on:
    
    * ECS
        
    * EKS
        
    * K8S on EC2
        
    * Fargate
        

## CloudWatch Lambda Insights

* Collects, aggregates, and summaries system-level metrics including CPU time, memory, disk, and network
    
* **Lambda insights** are provided by the **Lambda layer**
    

## CloudWatch Contributor Insights

* Analyze log data and create a time series that displays contributor data
    
    * See metrics about the top-N contributors
        
    * The total number of unique contributors and their usage
        

## CloudWatch Application Insights

* Provides automated dashboards that show potential problems with monitored applications, to help isolate ongoing issues
    
* Powered by SageMaker
    
* Enhance visibility into application health to reduce the time it will take to troubleshoot and repair application
    
* Findings and alerts are sent to EvenBridge and SSM OpsCenter
    

## CloudTrail

* CloudTrail is enabled by default
    
* It provides governance, compliance, and audit for AWS account
    
* Get **a history of events** / **API calls** made within the AWS account
    
    * SDK
        
    * Console
        
    * CLI
        
    * AWS Services
        
* Can put logs from CloudTrail into S3 or CloudWatch Logs
    
* **A Trail can be applied to All Regions (default) or Single Region**
    
* If a resource is deleted in AWS, investigate **CloudTrail** first
    

### CloudTrail Events

* Management Events
    
* Data Events
    
* CloudTrail Insights Events
    
    * To detect unusual activity in an AWS account
        
    * CloudTrail Insights analyses normal management events to create a baseline
        
    * Then, it continuously analyzes written events to detect unusual activity
        

### CloudTrail Events Retention

* Events are stored for 90 days in CloudTrail
    
* To keep events beyond this period, log them to S3 and use Athena
    

## AWS Config

* Helps with auditing and recording compliance of AWS resources
    
* Helps record configurations and changes over time
    
* Questions that can be solved by AWS Config
    
    * Is there unrestricted SSH access to my security groups?
        
    * Do my buckets have any public access?
        
* You can receive alerts (SNS) for any changes
    
* AWS Config is a per-region service
    
* Possibility of storing the configuration data in S3
    

### Config Rules

* Can use AWS managed config rules (over 75)
    
* Can make custom configuration rules (must be defined in AWS Lambda)
    
* Rules can be evaluated/triggered:
    
    * For each configuration change
        
    * And/or: at regular time intervals
        
* **AWS Config Rules** does not prevent actions from happening
    

## Summary

* CloudWatch
    
    * Performance monitoring & dashboard
        
    * Events & Alerting
        
    * Log Aggregation & Analysis
        
* CloudTrail
    
    * Record API calls made in the AWS Account by everyone
        
    * Can define trails for specific resources
        
    * Global service
        
* Config
    
    * Record configuration changes
        
    * Evaluate resources against compliance rules
        
    * Get timeline of changes and compliance