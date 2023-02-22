# tcpdump

### centos7 安装

```
yum install tcpdump
```

### ubuntu 安装

```bash
apt-get install tcpdump
```

### 命令选项

* \-i  指定监听网络接口

```bash
tcpdump -i eth0
```

* \-w 生成文件

```bash
tcpdump -w tcp.pcap
```

* \-n 域名转换成ip后显示
* \-nn  域名转换成ip,应用名转换成端口显示
* \-e 显示链路层信息

### 关键词

* host 主机地址
* net 网络地址
* port 端口
* src 源地址
* dst 目标地址
* src or dst 源地址或目标地址
* src and dst 源地址和目标地址
* ip ip协议
* tcp tcp 协议
* udp udp 协议
* imcp imcp 协议

### 逻辑运算

* not 非
* and 与
* or 或

```bash
tcpdump -i eth0  -nn tcp and \(host 192.168.0.250 and ! 192.168.0.74\)
```
