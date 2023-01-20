# 安装

### Centos7.7 or newer  &#x20;

```bash
yum install -y python3
```

### Centos7.6 or lower

```bash
yum install https://repo.ius.io/ius-release-el$(rpm -E '%{rhel}').rpm
yum update -y
yum install -y python3
```
