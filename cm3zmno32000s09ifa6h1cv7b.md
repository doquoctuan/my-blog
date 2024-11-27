---
title: "Setting a Static IP on Ubuntu"
datePublished: Wed Nov 27 2024 08:32:09 GMT+0000 (Coordinated Universal Time)
cuid: cm3zmno32000s09ifa6h1cv7b
slug: setting-a-static-ip-on-ubuntu
tags: ubuntu

---

Config the Static IP at /etc/netplan/00-installer-config.yaml

```yaml
network:
  ethernets:
    enp0s8:
      dhcp4: no
      addresses: [192.168.202.10/24]
  version: 2
```

Apply the new changes

```bash
sudo netplan try
```