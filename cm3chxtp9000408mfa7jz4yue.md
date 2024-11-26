---
title: "SAA-C03 Certification: RDS, Aurora and ElastiCache"
datePublished: Mon Nov 11 2024 04:01:22 GMT+0000 (Coordinated Universal Time)
cuid: cm3chxtp9000408mfa7jz4yue
slug: saa-c03-certification-rds-aurora-and-elasticache
tags: aws

---

## RDS Read Replicas vs Multi-AZ

* Up to 15 Read Replicas
    
* Within AZ, Cross AZ, or Cross region
    
* Replication is ASYNC, so reads are eventually consistent
    
* Replicas can be promoted to their DB
    
* Use-case: can be used for the **report service** that doesn't need to create, update, or delete records
    

### Network Cost

* For RDS read replicas with the same region, you don't pay that fee
    

### Multi-AZ (Disaster Recovery)

* This is not intended for scaling. It is only for adapting to disaster recovery situations
    
* The Read Replicas can be set as Multi-AZ for Disaster Recovery.
    
* To enable Multi-AZ: click "modify" for the database and enable the multi-AZ feature.
    

### Aurora

* It is a proprietary technology from AWS
    
* MySQL and Postgres are both supported as Aurora DB
    
* 5x performance improvement over MySQL on RDS, over 3x the performance of Postgres on RDS
    
* Storage automatically from 10 GB to 128 TB
    
* Up to 15 replicas and the replication process is faster than MySQL (10ms replica lag)
    
* Failover is instantaneous
    
* Costs more than RDS (20% more)
    

#### Aurora - High Availability and Read Scaling

* 6 copies of data across 3 AZ:
    
    * 4 copies out of 6 needed to write
        
    * 3 copies out of 6 needed for reads
        
    * self-healing with peer-to-peer replication
        
    * Storage is striped across 100s of volumes
        
* One Aurora instance takes writes (master instance)
    
* Automated failover for master in less than 30 seconds
    
* Master + up to 15 read replicas serve read
    
* Support for cross-region replication
    

Aurora has two types of endpoints: one for writing data and one for reading data. (Writer Endpoint and Reader Endpoint)

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1731238407782/9a2cb7e4-6f55-463f-9442-0edd6d31a3a4.png align="center")

### RDS Backup

* Automated backups:
    
    * Daily full backup of the database
        
    * Transaction logs are backed up by RDS every 5 minutes
        
    * \=&gt; ability to restore to any point in time (from oldest backup to 5 minutes ago)
        
    * 1 to 35 days of retention, set 0 to disable automated backup
        
* Manual DB Snapshots
    
* Trick: in a stopped RDS db, you will still pay for storage. If you plan on stopping it for a long time, you should snapshot and restore instead.
    

### Aurora Backup

* Automated backup
    
    * 1 to 35 days (cannot be disabled)
        
    * point in time recovery in that timeframe
        
* Manual Db snapshots (same as RDS)
    

Restoring an RDS / Aurora backup or a snapshot creates a new database Restoring MySQL RDS database from S3

* Create a backup of your on-premises database
    
* Store it on S3
    
* Restore the backup file onto a new RDS instance running MySQL
    

Restoring MySQL Aurora cluster from S3

* Create a backup of your on-premises database using **Percona XtraBackup**
    
* Store the backup file on S3
    
* Restore the backup file onto a new Aurora cluster running MySQL
    

### Aurora database cloning

* Create a new Aurora Db cluster from an existing one
    
* Faster than snapshot & restore
    
* Uses copy-on-write protocol
    
* Very fast & cost-effective
    
* Useful to create a staging db from a production db without impacting the production database
    

### RDS & Aurora Security

* At-rest encryption
    
    * Db master & replicas encryption using AWS KMS - must be defined as a launch time
        
    * If the master is not encrypted, the read replicas cannot be encrypted
        
    * To encrypt an un-encrypted DB, go through a DB snapshot & restore it as encrypted
        
* In-flight encryption: TLS-ready by default, use the AWS TLS root certificates client-side
    
* IAM Authentication: IAM role to connect to your DB (instead of username/password)
    
* Security group: control network access to RDS / Aurora DB
    
* No SSH available except on RDS custom
    
* Audit Logs can be enabled and sent to CloudWatch Logs for longer retention
    

### RDS Proxy

* Supports RDS (MySQL, PostgreSQL, MariaDB, SQL Server) and Aurora
    
* Reduced RDS & Aurora failover time by up 66%
    
* Serverless, auto-scaling, HA (multi-AZ)
    
* No code changes
    
* RDS Proxy is never publicly accessible (must be accessed from VPC)
    

### ElastiCache

* ElastiCache is to be managed by Redis or Memcached
    
* Helps make your application stateless
    
* Using ElastiCache involves heavy application code changes
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1731296718701/dcd203e2-585a-45a8-a6ec-6cb0e0d7fdf0.png align="center")

