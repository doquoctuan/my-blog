---
title: "SAA - C03 Certification: Other Services"
datePublished: Tue Dec 03 2024 07:14:08 GMT+0000 (Coordinated Universal Time)
cuid: cm484igad002h09kyehcyc6ia
slug: saa-c03-certification-other-services
tags: aws

---

# CloudFormation

## Benefits of AWS CloudFormation

* Infrastructure as code
    
* Cost
    
    * Each resource in the stack is tagged with an identifier so you can easily see how much a stack costs
        
    * Estimate the costs of resources using the CloudFormation template
        
    * Saving strategy: In Dev, you could automate the deletion of templates at 5 PM and recreate them at 8 A, safely
        
* Productivity
    
    * Automated generations of Diagram for template
        
* Do not reinvent the wheel
    
    * Leverage existing templates on the web
        
    * Leverage the documentation
        
* Supports (almost) all AWS resources
    

## Service Role

* Use cases:
    
    * You want to achieve the least privilege principle
        
    * But you do not want to give the user all the required permissions to create the stack resources
        
* User must have **iam:PassRole** permissions
    

# AWS SES

* Fully managed service to send emails securely, globally, and at scale
    
* Allow inbound/outbound emails
    
* Reputation dashboard, performance insights, anti-spam feedback
    
* Use cases: transactional, marketing, and bulk email communications
    

# Amazon Pinpoint

* Supports email, SMS, push, voice, and in-app messaging
    
* Possibility of receiving replies
    
* Scales to billions of messages per day
    
* Use cases: run campaigns by sending marketing, bulk, and transactional SMS messages
    
* Versus SNS or SES
    
    * In SNS & SES you managed each message’s audience, content, and delivery schedule.
        
    * In Pinpoint, you create message templates, delivery schedules, highly-targeted segments, and full campaigns.s
        

# System Manager - SSM Session Manager

* Allows to start a secure shell on EC2 and on-premises servers
    
* No SSH access, bastion hosts, or SSH Keys needed
    
* There is no need to open port 22
    
* Supports Linux, MacOS, Windows
    
* Send session log data to S3 or CloudWatch Logs
    

# System Manager

## Run command

* Execute a script or just run a command
    
* Run command across multiple instances (using resource groups)
    
* No need for SSH
    
* Command output can be shown in the AWS Console, and sent to the S3 bucket or CloudWatch Lo.gs.
    
* Send notifications to SNS about command status
    
* Integrated with IAM & CloudTrail
    
* It can be invoked using EventBridge
    

## Patch Manager

* Automates the process of patching managed instances
    
* OS updates, application updates, security updates
    
* Supports EC2 instances and on-premises servers
    
* Supports Linux, MacOS, Windows
    
* Patch on-demand or on a schedule using **Maintenance Windows**
    
* Scan instances and generate patch compliance reports (missing patches)
    

## **Maintenance Windows**

* Defines a schedule for when to perform actions on instances
    
* Example: OS patching, updating drivers, installing software,…
    

## Automation

* Simplifies common maintenance and deployment tasks of EC2 instances and other AWS resources
    
* Ex: restart instances, create an AMI, EBS Snapshot,…
    
* **Automation Runbook** - SSM Documents to define actions pre-formed on EC2 instances or AWS Resources
    
* Can be triggered using:
    
    * Manually using AWS Console, AWS CLI, SDK
        
    * EventBridge
        
    * On a schedule using **Maintenance Windows**
        
    * By AWS Config for **rules remediations**
        

# AWS Outposts

* Benefits:
    
    * Low-latency access to on-premises systems
        
    * Local data processing
        
    * Data residency
        
    * Easier migration from on-premises to the cloud
        
    * Fully managed service
        
* Some service that work on Outposts: EC2, EBS, S3, EKS, ECS, RDS, EMR
    

# AWS Batch

* Fully managed batch processing at any scale
    
* Efficiently run 100,000s of computing batch jobs on AWS
    
* A “batch” job is a job with a start and an end
    
* Batch will dynamically launch EC2 or Spot Instances
    
* Batch jobs are defined as Docker images and run on ECS
    
* Helpful for cost optimizations and focusing less on the infrastructure
    

| **Lambda** | **Batch** |
| --- | --- |
| Time Limit | No time limit |
| Limited runtimes | Any runtime as long as it’s packaged as a docker image |
| Limited temporary disk space | rely on EBS/Instance storage |
| Serverless | Relies on EC2 |

# Amazon AppFlow

* Fully managed integration service that enables secure transfer of data between SaaS applications and AWS
    
* Sources: Salesforce, SAP, ServiceNow
    
* Destinations: S3, Redshift,…
    
* Frequency: on a schedule, in response to events, on-demand
    

# AWS Amplify

* A set of tools and services that helps develop and deploy scalable full-stack web and mobile applications
    

# Instance Scheduler on AWS

* Automatically start/stop AWS services
    
* Supports cross-account and cross-region resources
    
* Schedules are managed in a DynamoDB table
    
* Supports EC2, EC2 Auto Scaling Groups, and RDS instances