---
title: "SAA - C03 Certification: Disaster Recovery and Migrations"
datePublished: Mon Dec 02 2024 15:47:26 GMT+0000 (Coordinated Universal Time)
cuid: cm477eprx00030ajx2npo3rc1
slug: saa-c03-certification-disaster-recovery-and-migrations
tags: aws

---

# Disaster Recovery in AWS

## There are different kinds of Disaster Recovery

* On-premise → On-premise: traditional DR, and very expensive
    
* On-premise → AWS Cloud: hybrid recovery
    
* AWS Cloud Region A → AWS Cloud Region B
    

## RPO and RTO

### RPO

* How much of a data loss
    

### RTO

* The amount of downtime of the application
    

## Pilot Light

* A small version of the app is always running in the cloud
    
* Useful for the critical core (pilot light)
    
* Very similar to Backup and Restore
    
* Faster than Backup and Restore
    

## Warm Standby

* The full system is up and running but at a minimum size
    
* Upon disaster, we can scale to production load
    

## Multi-Site / Hot Site Approach

* Very low RTO (minutes or seconds) - very expensive
    
* Full Production Scale is running AWS and On-Premise
    

## Disaster Recovery Tips

* Backup
    
    * EBS Snapshots, RDS Automated backups / Snapshots,…
        
    * Regular pushes to S3/S3 IA/Glacier, LifeCycle Policy, Cross Region Replication
        
    * From On-Premise: Snowball or Storage Gateway
        
* HA
    
    * Use Route53 to migrate DNS over from Region to Region
        
    * RDS Multi-AZ, ElasticCache Multi-AZ, EFS, S3
        
    * Site to Site VPN as a recovery from Direct Connect
        
* Replication
    
    * RDS Replication, AWS Aurora + Global Database
        
    * Database replication from on-premise to RDS
        
    * Storage Gateway
        
* Automation
    
    * CloudFormation / Elastic Beanstalk to re-create a whole new environment
        
    * Recover / Reboot EC2 instances with CloudWatch if alarms fail
        
    * AWS Lambda functions for customized automation
        
* Chaos
    
    * Netflix has a “**simian-army**” randomly terminating EC2
        

# Database Migration Service

* Supports:
    
    * Homogeneous migrations: Oracle to Oracle
        
    * Heterogeneous: SQL Server to Aurora
        
* Continuous Data Replication using the CDC
    
* Must create an EC2 instance to perform the replication tasks
    

## AWS Schema Conversion Tool

* Convert Database’s Schema from one engine to another
    
* You do not need to use SCT if you are migrating the same DB engine
    

# RDS & Aurora Migrations

## Migrate to MySQL Aurora

* RDS MySQL to Aurora MySQL
    
    * Option 1: DB Snapshots from RDS MySQL restored as MySQL AuroraDB
        
    * Options 2: Create an Aurora Read Replica from RDS MySQL, and when the replication lag is 0, promote it as its DB cluster (can take time and cost)
        
* External MySQL to Aurora MySQL
    
    * Option 1:
        
        * Use **Percona Xtrabackup** to create a file backup in S3
            
        * Create an Aurora MySQL DB from S3
            
    * Option 2:
        
        * Create an Aurora MySQL DB
            
        * Use the **mysqldump** utility to migrate MySQL into Aurora (slower than the S3 method)
            
* **Use DMS if both databases are up and running**
    

## Migrate to PostgreSQL Aurora

* RDS PostgreSQL to Aurora PostgreSQL
    
    * Option 1: DB Snapshots from RDS PostgreSQLrestored as PostgreSQL AuroraDB
        
    * Options 2: Create an Aurora Read Replica from RDS PostgreSQL, and when the replication lag is 0, promote it as its DB cluster (can take time and cost)
        
* External PostgreSQL to Aurora PostgreSQL
    
    * Create a backup and put it in S3
        
    * Import it using the **aws\_s3 Aurora extension**
        
* **Use DMS if both databases are up and running**
    

# AWS Backup

* Fully managed services
    
* Supported services:
    
    * EC2 / EBS
        
    * S3
        
    * RDS / Aurora / DynamoDB
        
    * DocumentDB / Neptune
        
    * EFS / FSx (Lustre & Windows File Server)
        
    * AWS Storage Gateway
        
* Supports cross-region backups
    
* Supports cross-account backups
    

## AWS Backup Vault Lock

* Enforce a WORM (Write Once Read Many) state for all the backups that are stored in AWS Backup Vault
    
* Even the root user cannot delete backups when enabled
    

# AWS Application Discovery Service

* Plan migration projects by gathering information about on-premises data centers
    
* Server utilization data and dependency mapping are important for migrations
    
* Agentless Discovery: VM inventory, configuration, and performance history such as CPU, memory, and disk usage
    
* Agent-based Discovery: System configuration, system performance, running processes, and details of the network connections between systems
    
* The resulting data can be viewed in the **AWS Migration Hub**
    

# Transferring large amounts of data to AWS

Example: transfer 200 TB of data in the cloud. We have a 100 Mbps internet connection

* Snowball
    
    * Will take 2 to 3 snowballs in parallel
        
    * Takes about 1 week for the end-to-end transfer
        
    * Can be combined with DMS
        
* Direct Connect 1 Gbps
    
    * Long for the one-time setup (over a month)
        
    * Will take 200(TB) \* *1000(GB)* \* 8(MB)/1 Gbps = 1,600,000s = 18.5d
        
* The Internet / Site-to-Site VPN
    
    * Immediate set up
        
    * Will take 200(TB) *\* 1000(GB)* \* *1000(MB)* \* 8(MB)/1 Gbps = 185d