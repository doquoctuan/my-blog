---
title: "SAA - C03 Certification: Containers on AWS"
datePublished: Thu Nov 21 2024 03:46:05 GMT+0000 (Coordinated Universal Time)
cuid: cm3qrsok1000508l4dheh4va5
slug: ssa-c03-certification-containers-on-aws
tags: aws

---

Docker Containers Management on AWS

1. **Amazon Elastic Container Service** (ECS) - Amazon’s container
    
2. **Amazon Elastic Kubernetes Service** (EKS) - Open-source
    
3. **AWS Fargate** - Amazon’s serverless container
    
4. **Amazon Elastic Container Registry** (ECR) - Store container images
    

# Amazon ECS

## EC2 Launch Type

* Launch Docker containers on AWS = Launch **ECS Tasks** on ECS Cluster
    
* You must provision and maintain the infrastructure (the EC2 instances)
    
* Each EC2 instance must run the **ECS Agent** to register in the ECS Cluster
    
* AWS takes care of stopping/starting container instances
    

## Fargate Launch Type

* You do not provision the infrastructure (no EC2 instances)
    
* It is all Serverless
    
* AWS runs **ECS Tasks** for you based on the CPU/RAM you need
    
* To scale, increase the number of tasks, no more EC2 instances
    

## IAM Roles for ECS

* EC2 Instance Profile (EC2 Launch Type only)
    
    * Used by the ECS agent
        
    * Makes API calls to ECS service
        
    * Send container logs to CloudWatch Logs
        
    * Pull Docker image from ECR
        
    * Reference sensitive data in Secrets Manager
        
* **ECS Task** Role
    
    * Allow each task to have a specific role
        

## Load Balancer Integrations

* ALB is supported and works for most use cases
    
* NLB is recommended only for high throughput / high-performance use cases, or to pair it with **AWS Private Link**
    

## Data Volumes (EFS)

* Mount EFS file systems onto ECS tasks
    
* Work for both EC2 and Fargate launch types
    
* Tasks running in any AZ will share the same data in the EFS file system
    
* Fargate + EFS = Serverless
    
* Use cases: persistent multi-AZ shared storage for containers
    

## ECS Service Auto Scaling

* Automatically increase/decrease the desired number of ECS tasks
    
* ECS Auto Scaling uses AWS Application Auto Scaling
    
    * ECS Service Average CPU Utilization
        
    * ECS Service Average RAM
        
    * ALB request Count per Target - metric from ALB
        
* Target Tracking - scale based on target value for a specific CloudWatch metric
    
* Step Scaling - scale based on a specified CloudWatch Alarm
    
* Schedule Scaling
    
* ECS Service Auto Scaling (**task level**) ≠ EC2 Auto Scaling (**instance level**)
    

# Amazon EKS

* It’s an alternative to ECS, with a similar goal but a different API
    
* EKS supports **EC2** if you want to deploy worker nodes or **Fargate** to deploy serverless containers
    
* Use case: if your company is already using K8S on-premises or in another cloud, and wants to migrate to AWS using K8S
    

## Node Types

### Managed Node Groups

* Create and manage Nodes (EC2) for you
    
* Nodes are part of an ASG managed by EKS
    
* Supports On-Demand or Spot Instances
    

### Self-Managed Nodes

* Nodes are created by you and registered to the EKS cluster and managed by an ASG
    
* You can use pre-built AMI
    
* Support On-Demand or Spot Instances
    

### AWS Fargate

* No need to manage nodes
    

## Data Volumes

* Need to specify **StorageClass** manifest on EKS Cluster
    
* Leverages a **Container Storage Interface** compliant driver
    
* Support for: **EBS**, **EFS (work with Fargate)**, **FSx for Lustre**, **FSx for NetApp ONTAP**
    

# AWS App Runner

* No infra experience is required
    
* Start with your source code or container image
    
* Automatically builds and deploys the web app
    
* Automatic scaling, HA, load balancer, encryption
    
* VPC access support
    
* Connect to database, cache, and message queue services
    
* Use cases: web apps, APIs, microservices, rapid production deployments
    

# AWS App2Container

* CLI Tool for migrating and modernizing Java and DotNET web apps into Docker Containers
    
* Lift-and-shift apps running in on-premises bare metal, virtual machines, or in any Cloud to AWS
    
* Generates CloudFormation templates
    
* Register generated Docker containers to ECR
    
* Deploy to ECS, EKS, or App Runner