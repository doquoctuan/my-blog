---
title: "Using an SSH local tunnel to establish a connection to a private network"
datePublished: Mon Nov 04 2024 10:27:54 GMT+0000 (Coordinated Universal Time)
cuid: cm32vnxwk000b09jq5ag015vm
slug: using-an-ssh-local-tunnel-to-establish-a-connection-to-a-private-network
tags: tricks, linux, tips

---

#### Local Forwarding

```
ssh -L {local-port}:{internal-ip}:{internal-port} remote-user@remote-ip
```