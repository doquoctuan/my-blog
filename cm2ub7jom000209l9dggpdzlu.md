---
title: "Install a free SSL certificate on Linux utilizing Certbot."
datePublished: Tue Oct 29 2024 10:33:07 GMT+0000 (Coordinated Universal Time)
cuid: cm2ub7jom000209l9dggpdzlu
slug: install-a-free-ssl-certificate-on-linux-utilizing-certbot
tags: tricks, linux, tips

---

#### 1. Installing Let's Encrypt client

```
$ apt-get update
$ sudo apt-get install certbot
$ apt-get install python3-certbot-nginx
```

#### 2. Installing SSL for your domain

```
sudo certbot --nginx -d example.com -d www.example.com
```

```
Congratulations! You have successfully enabled https://example.com and https://www.example.com 

-------------------------------------------------------------------------------------
IMPORTANT NOTES: 

Congratulations! Your certificate and chain have been saved at: 
/etc/letsencrypt/live/example.com/fullchain.pem 
Your key file has been saved at: 
/etc/letsencrypt/live/example.com//privkey.pem
Your cert will expire on 2022-12-12.
```

#### 3. Verifying the nginx config file

```
server {
    listen 80 default_server;
    listen [::]:80 default_server;
    root /var/www/html;
    server_name  example.com www.example.com;

    listen 443 ssl; # managed by Certbot

    # RSA certificate
    ssl_certificate /etc/letsencrypt/live/example.com/fullchain.pem; # managed by Certbot
    ssl_certificate_key /etc/letsencrypt/live/example.com/privkey.pem; # managed by Certbot

    include /etc/letsencrypt/options-ssl-nginx.conf; # managed by Certbot

    # Redirect non-https traffic to https
    if ($scheme != "https") {
        return 301 https://$host$request_uri;
    } # managed by Certbot
}
```

#### 4. Setuping cronjobs for auto-renew SSL

```
crontab -e
```

```
0 12 * * * /usr/bin/certbot renew --quiet
```