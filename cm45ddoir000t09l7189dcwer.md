---
title: "SAA - C03 Certification: Networking"
datePublished: Sun Dec 01 2024 08:59:03 GMT+0000 (Coordinated Universal Time)
cuid: cm45ddoir000t09l7189dcwer
slug: saa-c03-certification-networking
tags: aws

---

# Public and Private IP

* **Private IP**
    
    * 10.0.0.0 - 10.255.255.255 (10.0.0.0/8)
        
    * 172.16.0.0 - 172.31.255.255 (172.16.0.0/12) ← AWS default VPC in that range
        
    * 192.168.0.0 - 192.168.255.255 (192.168.0.0/16) ← home networks
        
* **Public IP**: All the rest of the IP addresses
    

# Subnet

* AWS reserves 5 IP addressed (first 4 and last 1) in each subnet
    
    * Example: if CIDR blocks 10.0.0.0/24, then reserved IP addresses are:
        
        * **10.0.0.0** - Network Address
            
        * **10.0.0.1** - reserved by AWS for the VPC router
            
        * **10.0.0.2** - mapping to Amazon-provided DNS
            
        * **10.0.03** - future use
            
        * **10.0.0.255** - Network Broadcast Address
            

# NAT Instance

* Allows EC2 Instances in a private subnet to connect to the Internet
    
* **Must be launched in a public subnet**
    
* **Must disable EC2 Setting: Source/destination Check**
    
* **Must have Elastic IP attached to it**
    
* Route Tables must be configured to route traffic from **Private Subnets** to the **NAT Instance**
    

## Comments

* Pre-configured Amazon Linux AMI is available
    
    * Reached the end of standard support on 31/12/2020
        
* Not HA / Resilient setup out of the box
    
    * It would help if you created an ASG in multi-AZ + resilient user-data script
        
* Internet traffic bandwidth depends on EC2 Instance Type
    
* You must manage Security Groups & Rules:
    
    * Inbound
        
        * Allow HTTP/HTTPS traffic coming from Private Subnets
            
        * Allow SSH from your home network
            
    * Outbound
        
        * Allow HTTP/HTTPS traffic to the Internet
            

# NAT Gateway

* AWS-managed NAT, higher bandwidth, HA, no administration
    
* Pay per hour for usage and bandwidth
    
* NATGW is created in a specific AZ, uses an Elastic IP
    
* Cannot be used by EC2 instance in the same subnet
    
* **Requires an IGW** (Private Subnet → NATGW → IGW)
    
* 5 Gbps of bandwidth with automatic scaling up to 100 Gbps
    
* No Security Groups to manage/required
    

## NAT Gateway with HA

* NAT Gateway is resilient within a single AZ
    
* Must **create multiple NAT Gateways** in multiple AZs for fault-tolerance
    

# VPC Peering

* You can create VPC Peeing connections between VPCs in different AWS accounts/regions
    
* You can reference a security group in a peered VPC (works cross accounts - same region)
    

# VPC Endpoints (AWS PrivateLink)

* Every AWS service is publicly exposed (public URL)
    
* VPC Endpoints (powered by AWS PrivateLink) allows you to connect to AWS services using a private network instead of using the public internet
    

## Types of Endpoints

* Interface Endpoints (powered by PrivateLink)
    
    * Provisions an ENI (private IP address) as an entry point (must attach a Security Group)
        
    * Supports most AWS Services
        
    * $ per hour + $ per GB of data processed
        
* Gateway Endpoints
    
    * Provisions a gateway and must be used as a target in a route table (does not use security group)
        
    * Supports both **S3** and **DynamoDB**
        
    * Free
        

# AWS Site-to-Site VPN

* **Virtual Private Gateway (VGW)**
    
    * VPN concentrator on the AWS side of the VPN connection
        
    * VGW is created and attached to the VPC from which you want to create the Site-to-Site VPN connection
        
    * Possibility to customize the ASN (Autonomous System Number)
        
* **Customer Gateway (CGW)**
    
    * A software application or physical device on the customer side of the VPN connection
        

> Enable Route Propagation for the **VGW** in the route table that is accociated with subnets

## AWS VPN CloudHub

* Provide secure communication between multiple sites, if you have multiple VPN connections
    
* Low-cost hub-and-spoke model for primary or secondary network connectivity between different locations (VPN only)
    
* It’s a VPN connection so it goes over the public internet
    
* To set it up, connect multiple VPN connections on the same VGW, set dynamic routing, and configure route tables
    

# Direct Connect (DX)

* Provides a dedicated private connection from a remote network to VPC
    
* Supports both IPv4 and IPv6
    
* Use Cases:
    
    * Increase bandwidth throughput
        
    * More consistent network experience
        
    * Hybrid Environments (on-prem + cloud)
        

## Connection Types

* Dedicated Connections: 1 Gbps, 10 Gbps and 100 Gbps capacity
    
* Hosted Connections: 50 Mbps, 500 Mbps, to 10 Gbps
    
* Lead times are often longer than 1 month to establish a new connection
    

## Encryption

* Data in transit is not encrypted but is private
    
* AWS Direct Connect + VPN provides an IPsec-encrypted private connection
    
* Good for an extra level of security
    

> In case Direct Connect fails, you can set up a backup Direct Connect connection (expensive), or a Site-to-Site VPN connectio

# Transit Gateway

* For having transitive peering between thousands of VPC and on-prem connection
    
* Regional resources can work cross-region
    
* Supports IP Multicast
    

# Traffic Mirroring

* Allows to capture and inspect network traffic in VPC
    
* Route the traffic to security appliances
    
* Capture the traffic
    
    * From (Source)
        
    * To (Targets)
        

# Egress Only Internet Gateway

* Used for IPv6 only (similar to a NAT Gateway but for IPv6)
    
* Must update the **Route Tables**