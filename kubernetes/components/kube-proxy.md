---
description: k8s网络代理
---

# kube-proxy

### Service 转发规则

#### Iptables

获取本机所有**KUBE-SERVICES** 链内的记录

```bash
iptables -t nat -L KUBE-SERVICES
```

#### NodePort Service

获取本机所有**KUBE-NODEPORTS** 链内的记录

```bash
iptables -t nat -L KUBE-NODEPORTS
```
