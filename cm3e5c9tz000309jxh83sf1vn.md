---
title: "SAA-C03 Certification: Route 53"
datePublished: Tue Nov 12 2024 07:44:14 GMT+0000 (Coordinated Universal Time)
cuid: cm3e5c9tz000309jxh83sf1vn
slug: saa-c03-certification-route-53
tags: aws

---

The difference between **CNAME** and **ALIAS**

* AWS resources (Load Balancer, CloudFront,…) expose an AWS **hostname**:
    
    * *lb1-123.us-east-2.elb.aws.com* and you want *myapp.mydomain.com*
        

| **CNAME** | **ALIAS** |
| --- | --- |
| Points a hostname to any other hostname | Points a hostname to an AWS resource |
| Only works for **NON-ROOT** domain | Works for **ROOT & NON-ROOT** |
|  | Free & Native health check |
|  | Can’t set the TTL |

### Alias Records Targets

* Elastic Load Balancers
    
* CloudFront
    
* API Gateway
    
* Elastic Beanstalk
    
* S3 Websites
    
* VPC interface endpoints
    
* Global accelerator
    

**You can not set an ALIAS record for the EC2 DNS name**