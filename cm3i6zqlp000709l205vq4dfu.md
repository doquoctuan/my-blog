---
title: "SSA - C03 Certification: S3"
datePublished: Fri Nov 15 2024 03:41:33 GMT+0000 (Coordinated Universal Time)
cuid: cm3i6zqlp000709l205vq4dfu
slug: ssa-c03-certification-s3
tags: aws

---

## Security

* User-based
    
    * IAM policies
        
* Resource-based
    
    * Bucket policies
        
    * Object/Bucket ACL (can be disabled)
        

### Bucket Policies

* JSON-based policies
    
    * Resources: buckets and objects
        
    * Effect: Allow / Deny
        
    * Actions: Set of APIs to Allow or Deny
        
    * Principal: The account or user to apply the policy to
        

## Replication

* Must enable Versioning in source and destination buckets
    
* Cross-Region Replication (CRR)
    
* Same-Region Replication (SRR)
    
* Buckets can be in different AWS accounts
    
* Copying is asynchronous
    
* Must give proper IAM permissions to S3
    

Use cases:

* CRR: lower latency access, replication across accounts
    
* SRR: log aggregation, live replication between production and test accounts
    

Some notes:

* After you enable Replication, only new objects are replicated
    
* Optionally, you can replicate existing objects using **S3 Batch Replication**
    
* For DELETE operations:
    
    * Can replicate delete markers from source to target (optional setting)
        
    * Deletions with a version ID are not replicated (to avoid malicious deletes)
        
* **There is no "chaining" of replication**
    

### Storage Class

* Standard - General Purpose - 99.99% (Big Data, Mobile & Gaming, Content Distribution,...)
    
* Standard - Infrequent Access (IA) - 99.9% (Disaster Recovery, backups)
    
* One Zone - Infrequent Access - 99.5% (Storing secondary backup)
    
* Glacier Instant Retrieval
    
    * Millisecond retrieval, is great for data accessed once a quarter
        
    * Minimum storage duration of 90 days
        
* Glacier Flexible Retrieval
    
    * Expedited (1 to 5 minutes), Standard (3 to 5 hours), Bulk (5 to 12 hours) - free
        
    * Minimum storage duration of 90 days
        
* Glacier Deep Archive - for long-term storage
    
    * Standard (12 hours), Bulk (48 hours)
        
* Intelligent Tiering
    * Small monthly monitoring and auro-tiering free
    * Moves object automatically between Access Tiers based on usage
    * There are no retrieval charges in S3 Intelligent-Tiering
    * Frequent Access tier (auto): default tier
    * Infrequent Access tier (auto): objects not accessed for 30 days
    * Archive Instant Access tier (auto): objects not accessed for 90 days
    * Archive Access tier (optional): configurable from 90 days to 700+ days
    * Deep Archive Access tier (optional): configurable from 180 days to 700+ days

Lifecycle Rules

- Transition Actions: configure objects to transition to another storage class
- Expiration Actions: configure objects to expire (delete) after some time
- Rules can be created for **a certain prefix** (ex: s3://bucket/mp3/*)
- Rules can be created for **certain object tags**

Performance

- Latency 100 - 200ms
- Your application can achieve at least 3,500 PUT/COPY/POST/DELETE or 5,500 GET/HEAD requests per second per prefix in a bucket
- There are no limits to the number of prefixes in a bucket
- If you spread reads across all 4 prefixes evenly, you can achieve 22,00 RPS for GET/HEAD
- Multi-part upload:
  + recommend for files > 100 MB, must use for files > 5 GB
  + can help parallelize upload (speed up transfers)
- Byte-range fetches
  + Parallelize GETs by requesting specific byte ranges
  + Better resilience in case of failures
  + Can be used to speed up downloads

### Object Encryption

- Server-side encryption (SSE)
  + SSE with Amazon S3-Managed Keys (SSE-S3) - enable by default (AES-256)
  + SSE with KMS Keys stored in AWS KMS (SSE-KMS) - Needing to make an API call to KMS to receive an encryption key **(5500, 10000, 3000 req/s based on region)**
    + Can request a quota increase using the **Service Quotas Console**
  + SSE with customer-provided keys (SSE-C) (Only support **HTTPS**)
- Client-side encryption

### S3 Glacier Vault Lock

- Adopt a WORM (write once and read many)
- Create a Vault Lock Policy
- Helpful for compliance and data retention

### S3 Object Lock (versioning must be enabled)

- Adopt a WORM (write once and read many)
- Block an object version deletion for a specified amount of time

### S3 - Access Points

- Each access point has:
  + its own DNS name (Internet Origin or VPC Origin)

VPC Origin

- We can define the access point to be accessible only from within the VPC
- You must create a VPC Endpoint to access the access endpoint (Gateway or Interface Endpoint)
- The VPC endpoint policy must allow access to the target bucket and Access Point



