---
title: "SAA - C03 Certification: CloudFront"
datePublished: Mon Nov 18 2024 04:15:56 GMT+0000 (Coordinated Universal Time)
cuid: cm3mijija000l09mkfydf7jco
slug: ssa-c03-certification-cloudfront
tags: aws

---

### Origins

#### S3 bucket

* CloudFront can be used as an ingress (to upload files to S3)
    

#### Custom Origin (HTTP)

* Application Load Balancer
    
* EC2 Instance
    
* S3 website (must first enable the bucket as a static s3 website)
    
* Any HTTP backend you want
    

The difference between **CloudFront** and **S3 Cross Region Replication**

| **CloudFront** | **S3 Cross Region Replication** |
| --- | --- |
| Global network edge | Must be set for each region you wish replication to happen |
| Files are cached for a TTL | Files are updated in near real-time |
| Read Only |  |
| Great for static content that must be available everywhere | Great for dynamic content that needs to be available at low latency in a few regions |

### Price Classes

You can reduce the number of edge locations for cost reduction

Three price classes:

* Price Class All: all regions - best performance
    
* Price Class 200: most regions
    
* Price Class 100: only the least expensive region
    

### Cache Invalidations

If you update the back-end origins, CloudFront does not know about it and will only get the refreshed content after the expired TTL

However, you can force an entire or partial cache refresh by performing a **CloudFront Invalidation**

You can invalidate all files (\*) or a special path (/images/\*)

### AWS Global Accelerator

Leverage the AWS **internal network** to route your application

2 Anycast IPs are created for your application

The Anycast IP sends traffic directly to Edge Locations

The Edge locations send the traffic to your application

Works with **Elastic IP, EC2, ALB, NLB, public or private**

**Unicast vs Anycast IP**

Unicast IP: one server holds one IP address

Anycast IP: all servers hold the same IP address and the client is routed to the nearest one