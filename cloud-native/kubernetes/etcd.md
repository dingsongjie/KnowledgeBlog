# etcd

### 在pod中运行etcdctl

```bash
ETCDCTL_API=3 etcdctl --endpoints endpoint1,endpoint2,endpoint3
-w table
--cert=/etc/kubernetes/pki/etcd/server.crt
--key=/etc/kubernetes/pki/etcd/server.key
--cacert=/etc/kubernetes/pki/etcd/ca.crt \
```
