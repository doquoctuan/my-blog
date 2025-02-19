---
title: "How to install Redis Sentinel using Helm in K8S"
datePublished: Wed Feb 19 2025 07:59:11 GMT+0000 (Coordinated Universal Time)
cuid: cm7bmgtyf000u09k46w600lc3
slug: how-to-install-redis-sentinel-using-helm-in-k8s
tags: redis, k8s

---

## Adding bitnami repo into local repo helm

```powershell
helm repo add bitnami https://charts.bitnami.com/bitnami
helm repo ls
```

## Cloning repository Redis on bitnami to machine

```powershell
mkdir redis-sentinel
cd ./redis-sentinel
helm fetch bitnami/redis --untar
```

## Make changes to the configurations

### Edit ***values.yaml*** file

```yaml
replica.replicaCount: 2
sentinel.enabled: true
sentinel.quorum: 2
sentinel.masterSet: mymaster
global.redis.password: <YOUR_PASSWORD>
```

## Creating a new namespace and installing redis-sentinel

```powershell
kubectl create namespace redis-sentinel
helm install redis-sentinel ./ -n redis-sentinel
kubectl get pods -n redis-sentinel
```

---

## How to find a current primary master host

```powershell
redis-cli -h redis-sentinel -p 26379 -a 'YOUR_PASSWORD' SENTINEL get-master-addr-by-name mymaster
```

> Example response: ***redis-sentinel-node-0.redis-sentinel-headless.redis-sentinel.svc.cluster.local***

**The format of that response is:**

> &lt;pod\_name&gt;.&lt;service\_name&gt;.&lt;namespace&gt;.svc.cluster.local

---

## Config Redis Commander for accessing Redis Sentinel

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: redis-commander
  annotations:
    container.apparmor.security.beta.kubernetes.io/redis-commander: runtime/default
    container.security.alpha.kubernetes.io/redis-commander: runtime/default
  labels:
    app.kubernetes.io/part-of: redis-sentinel
    app.kubernetes.io/name: redis-commander
spec:
  replicas: 1
  selector:
    matchLabels:
      app: redis-commander
  template:
    metadata:
      labels:
        app: redis-commander
        app.kubernetes.io/part-of: redis-sentinel
        app.kubernetes.io/name: redis-commander
    spec:
      automountServiceAccountToken: false
      containers:
        - name: redis-commander
          image: ghcr.io/joeferner/redis-commander
          imagePullPolicy: Always
          env:
            - name: SENTINEL_GROUP
              value: "mymaster"
            - name: SENTINEL_PASSWORD
              value: "sJxpl1HBQZLpNoI"
            - name: REDIS_PASSWORD
              value: "sJxpl1HBQZLpNoI"
            - name: SENTINELS
              value: "redis-sentinel-node-0.redis-sentinel-headless.redis-sentinel.svc.cluster.local:26379,redis-sentinel-node-1.redis-sentinel-headless.redis-sentinel.svc.cluster.local:26379,redis-sentinel-node-2.redis-sentinel-headless.redis-sentinel.svc.cluster.local:26379"
          ports:
            - name: redis-commander
              containerPort: 8081
          resources:
            limits:
              cpu: "500m"
              memory: "512M"
          securityContext:
            runAsNonRoot: true
            readOnlyRootFilesystem: false
            allowPrivilegeEscalation: false
            capabilities:
              drop:
                - ALL
```