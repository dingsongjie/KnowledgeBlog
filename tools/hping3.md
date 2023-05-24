# hping3

### centos7 安装

```bash
yum install epel-release
yum install hping3
```

### 端口扫描

```bash
hping3 --scan 1-30,70-90 -S <ip>
```
