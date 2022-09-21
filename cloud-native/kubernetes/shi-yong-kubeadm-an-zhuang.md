# 使用Kubeadm安装

### Centos7

#### 所有节点

* 修改节点Hostname

```bash
hostnamectl set-hostname my.new-hostname.server
```

* 设置Dns映射

在/etc/host 中添加所有master 包括 kube-api dns和ip之间的映射关系

* 删除之前的docker组件

```bash
sudo yum remove docker \
                  docker-client \
                  docker-client-latest \
                  docker-common \
                  docker-latest \
                  docker-latest-logrotate \
                  docker-logrotate \
                  docker-engine
```

* docker repo 设置

```bash
sudo yum install -y yum-utils
sudo yum-config-manager \
    --add-repo \
    https://download.docker.com/linux/centos/docker-ce.repo
```

* 安装docker

```bash
 sudo yum install  docker-ce-20.10.12 docker-ce-cli containerd.io docker-compose-plugin
```

* 配置docker

```bash
sudo tee /etc/docker/daemon.json <<EOF
{
  "exec-opts": ["native.cgroupdriver=systemd"],
  "log-driver": "json-file",
  "log-opts": {
    "max-size": "100m"
  },
  "storage-driver": "overlay2",
  "storage-opts": [
    "overlay2.override_kernel_check=true"
  ]
}
EOF
```

* 设置开机启动并立即启动docker服务

```bash
sudo systemctl enable --now docker
```

* 禁用SELINUX,关闭swap,关闭防火墙

```bash
sudo setenforce 0
sudo sed -i 's/^SELINUX=enforcing$/SELINUX=permissive/' /etc/selinux/config
sudo sed -i '/ swap / s/^\(.*\)$/#\1/g' /etc/fstab
sudo swapoff -a
sudo systemctl disable --now firewalld
```

* 配置 sysctl

```bash
sudo modprobe overlay
sudo modprobe br_netfilter

sudo tee /etc/sysctl.d/kubernetes.conf<<EOF
net.bridge.bridge-nf-call-ip6tables = 1
net.bridge.bridge-nf-call-iptables = 1
net.ipv4.ip_forward = 1
EOF

sudo sysctl --system
```

* 安装 kubeadm kubelet kubectl

```bash
cat >> /etc/yum.repos.d/kubernetes.repo << EOF
[kubernetes]
name=kubernetes
baseurl=https://mirrors.aliyun.com/kubernetes/yum/repos/kubernetes-el7-x86_64
enabled=1
gpgcheck=0
repo_gpgcheck=0
gpgkey=https://mirrors.aliyun.com/kubernetes/yum/doc/yum-key.gpg
https://mirrors.aliyun.com/kubernetes/yum/doc/rpm-package-key.gpg
EOF

sudo yum install -y kubelet-1.21.3 kubeadm-1.21.3 kubectl-1.21.3 --disableexcludes=kubernetes

sudo systemctl enable --now kubelet

```

* 获取 join 命令

```bash
kubeadm token create --print-join-command
```

* 获取 certificate-key

```bash
kubeadm init phase upload-certs --upload-certs
```
