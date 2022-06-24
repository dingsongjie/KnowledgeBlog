---
description: 诊断工具的安装，基本Debain的镜像，以及apt使用清华大学镜像源
---

# Tools in container

#### Apt sources

```bash
cat >/etc/apt/sources.list <<EOF 
# 默认注释了源码镜像以提高 apt update 速度，如有需要可自行取消注释 
deb https://mirrors.tuna.tsinghua.edu.cn/debian/ buster main contrib non-free 
# deb-src https://mirrors.tuna.tsinghua.edu.cn/debian/ buster main contrib non-free 
deb https://mirrors.tuna.tsinghua.edu.cn/debian/ buster-updates main contrib non-free 
# deb-src https://mirrors.tuna.tsinghua.edu.cn/debian/ buster-updates main contrib non-free 

deb https://mirrors.tuna.tsinghua.edu.cn/debian/ buster-backports main contrib non-free 
# deb-src https://mirrors.tuna.tsinghua.edu.cn/debian/ buster-backports main contrib non-free 

deb https://mirrors.tuna.tsinghua.edu.cn/debian-security buster/updates main contrib non-free 
# deb-src https://mirrors.tuna.tsinghua.edu.cn/debian-security buster/updates main contrib non-free 
EOF
```

#### Base on .NET6-SDK

```bash
apt-get update && apt-get install -y wget && wget https://packages.microsoft.com/config/debian/11/packages-microsoft-prod.deb -O packages-microsoft-prod.deb && dpkg -i packages-microsoft-prod.deb \
&& apt-get install -y apt-transport-https && apt-get update && apt-get install -y dotnet-sdk-6.0
```

####

