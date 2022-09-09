# linux

文档地址：[https://github.com/prometheus/node\_exporter](https://github.com/prometheus/node\_exporter)



### Centos7安装并生成system服务

curl -Lo /etc/yum.repos.d/\_copr\_ibotty-prometheus-exporters.repo https://copr.fedorainfracloud.org/coprs/ibotty/prometheus-exporters/repo/epel-7/ibotty-prometheus-exporters-epel-7.repo

yum install node\_exporter

cat < /etc/systemd/system/node\_exporter.service \[Unit] Description=Node Exporter After=network.target

\[Service] User=node\_exporter Group=node\_exporter Type=simple ExecStart=/usr/sbin/node\_exporter

\[Install] WantedBy=multi-user.target EOF
