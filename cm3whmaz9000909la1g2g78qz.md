---
title: "Install Docker & Docker Compose on Amazon Linux EC2"
datePublished: Mon Nov 25 2024 03:47:48 GMT+0000 (Coordinated Universal Time)
cuid: cm3whmaz9000909la1g2g78qz
slug: install-docker-docker-compose-on-amazon-linux-ec2
tags: tricks, docker, tips

---

## To install Docker

```bash
sudo yum update -y 

sudo amazon-linux-extras install docker 

sudo yum install docker 

sudo service docker start 

sudo usermod -a -G docker ec2-user 
```

## To install Docker Compose

```bash
sudo curl -L https://github.com/docker/compose/releases/latest/download/docker-compose-$(uname -s)-$(uname -m) -o /usr/local/bin/docker-compose

sudo chmod +x /usr/local/bin/docker-compose

docker-compose version
```