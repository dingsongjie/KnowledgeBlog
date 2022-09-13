# linux

文档地址：[https://github.com/prometheus/node\_exporter](https://github.com/prometheus/node\_exporter)



### Centos7安装并生成system服务

```bash
curl -Lo /etc/yum.repos.d/_copr_ibotty-prometheus-exporters.repo https://copr.fedorainfracloud.org/coprs/ibotty/prometheus-exporters/repo/epel-7/ibotty-prometheus-exporters-epel-7.repo


yum install node_exporter


cat > /etc/systemd/system/node_exporter.service<<EOF
[Unit] 
Description=Node Exporter 
After=network.target
[Service] 
User=node_exporter 
Group=node_exporter 
Type=simple 
ExecStart=/usr/sbin/node_exporter
[Install] 
WantedBy=multi-user.target 
EOF
```



