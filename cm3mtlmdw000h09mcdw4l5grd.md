---
title: "SSA - C03 Certification: Storage Extras"
datePublished: Mon Nov 18 2024 09:25:30 GMT+0000 (Coordinated Universal Time)
cuid: cm3mtlmdw000h09mcdw4l5grd
slug: ssa-c03-certification-storage-extras
tags: aws

---

## AWS Snow Family

Highly secure, portable devices to **collect and process** data at the edge, and migrate data into and out of AWS

**AWS Snow Family**: offline devices to perform data migrations  
If it takes **more than a week** to transfer over the network, use **Snowball** devices!

### Usage Process

1. Request Snowball devices from the AWS Console
    
2. Install the snowball client / AWS OpsHub on your servers
    
3. Connect the snowball to your servers and copy files using the client
    
4. Ship back the device when you are done
    
5. Data will be loaded into an S3 bucket
    

### The primary use cases of the AWS Snow Family

1. **Data Migration: has 3 types of devices**  
    \- Snowcone  
    \- Snowball Edge  
    \- Snowmobile
    
2. **Edge Computing: (collect, and process data before transfer to AWS)**  
    \- Snowcone  
    \- Snowball Edge
    

|  | **Snowcone** | **Snowball** | **Snowmobile** |
| --- | --- | --- | --- |
| Storage capacity | 8 TB usable | 80 TB usable | &lt; 100 PB |
| Migrate size | up to 24 TB, online or offline | up to petabytes, offline | up to exabytes, offline |
| DataSync | pre-installed |  |  |
| Storage cluster |  | can add a maximum of 15 nodes to increase capacity |  |

> **Snowball** cannot import data directly to **Glacier**. You need to import it to another storage class (e.g., **Standard IA**) and then use S3 lifecycle policies to move it to Glacier later.

## Amazon FSx

### Overview

Launch 3rd party high-performance file systems on AWS

Fully managed service

### FSx for Windows (File Server)

* **It is similar to EFS but supports running on both Windows and Linux**
    

* Supports SMB protocol and Windows NTFS
    
* Microsoft Active Directory integration, ACLs, user quotas
    

* It can be mounted on Linux EC2
    
* Supports Microsoft’s Distributed File System Namespaces
    
* Scales up to **10s of GB/s, millions of IOPS, 100s PB of data**
    
* Storage options: **SSD** & **HDD**
    
* Can be accessed from your on-premises infra (VPN or Direct Connect)
    
* It can be configured to be Multi-AZ
    
* Data is backed up daily on S3
    

### FSx for Lustre

* Parallel distributed file system, for large-scale computing
    
* The name Lustr is derived from “Linux” and “Cluster”
    
* Use cases: machine learning, high-performance computing, video processing,…
    
* Scales up to **100s GB/s, millions of IOPS, sub-ms latencies**
    
* Storage options: **SSD & HDD**
    
* Seamless integration with S3
    
    * Can “read s3” as a file system
        
    * Can write the output of the computations back to S3
        
* Can be used from on-premises servers (VPN or Direct Connect)
    

### FSx file system deployment options

When creating an FSx file system, you need to understand the difference between two options: **Scratch File System** and **Persistent File System**

* **Scratch File System:**
    
    * Temporary storage
        
    * The data does not replicate
        
    * High write though
        
    * High write throughput
        
    * Use in short-time process, optimize cost
        
* **Persistent File System:**
    
    * Long-term storage
        
    * The data is replicated in a single Availability Zone (AZ)
        
    * Recover error files in just one to a few minutes
        
    * Use in a long-term process
        

### Edge Computing

* Snowcone
    
    * 2 CPUs, 4 GB RAM, can be accessed wired or wireless
        
    * USB - C Port
        
* Snowball Edge - Computed Optimized
    
    * 52 vCPUs, 208 GB RAM
        
    * Optimized GPU
        
* Snowball Edge - Storage Optimized
    
    * Maximum 40 vCPUs, 80 GB RAM
        
    * Having Object Storage Clustering
        

> These edge computing devices can run using EC2 instances or Lambda functions

### What is AWS OpsHub

> AWS OpsHub is software that can be installed on your machine to manage Snow Family devices.

## Storage Gateway

There are **four types** of storage class:

### AWS S3 File Gateway

* Configure access S3 using NFS/SMB protocol
    
* Supporting S3 Standard, S3 IA, S3 One Zone IA
    
* Data can be cached at the S3 File Gateway, which reduces latency.
    
* It can be mounted on many different servers
    
* Using **Active Directory** for User Authentication
    

### AWS Volume Gateway

* Block storage uses iSCSI
    
* You will save your data with an EBS snapshot that will help you restore the volume on-premises.
    
* There are two types:
    
    * Cache Volume: It provides lower latency for frequently accessed data
        
    * Stored Volume: All data is stored on-premises, with scheduled backups on S3
        

### AWS Tape Gateway

* The primary purpose is backup data
    
* Allows replacing the use of physical tapes on-premises with Virtual Tapes on AWS
    

### AWS FSx Gateway

* Native access to Amazon FSx for Windows File Server
    
* Local cache for frequently accessed data
    
* Windows native compatibility (SMB, NTFS,…)
    
* Useful for group file sharing and home directories
    

#### Storage Gateway Hardware Appliance

* If you use **Storage Gateway**, your application will connect through a virtual machine
    
* However, you can choose to use **Storage Gateway Hardware Appliance**, which is a device that you can buy through [amazon.com](https://amazon.com)
    
* The device works with three types of devices: **File, Volume, Tape**
    
* The device has memory, network, CPU, and SSD
    
* It is handy for daily NFS backups in a small data center
    

## AWS Transfer Family

* A fully managed service for file transfer into and out of S3 or EFS using **FTP protocol**
    
* Supported Protocols:
    
    * AWS Transfer for FTP
        
    * AWS Transfer for FTPS
        
    * AWS Transfer for SFTP
        
* Managed infrastructure, scalable, reliable, highly available (multi-AZ)
    
* Pay per provisioned endpoint per hour + data transfer in GB
    
* Store and manage user’s credentials within the service
    
* Integrate with existing authentication systems (Microsoft Active Directory, LDAP, Okta,…)
    
* Usage: sharing files, public datasets, CRM, ERP,…