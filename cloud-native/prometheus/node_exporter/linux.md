# linux

文档地址：[https://github.com/prometheus/node\_exporter](https://github.com/prometheus/node\_exporter)



### Centos7安装并生成system服务

```bash
curl -Lo /etc/yum.repos.d/_copr_ibotty-prometheus-exporters.repo https://copr.fedorainfracloud.org/coprs/ibotty/prometheus-exporters/repo/epel-7/ibotty-prometheus-exporters-epel-7.repo


yum install node_exporter


vi /etc/systemd/system/node_exporter.service<<EOF
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

### Centos6上安装并生成服务



```bash

curl -OL https://github.com/prometheus/node_exporter/releases/download/v1.3.1/node_exporter-1.3.1.linux-amd64.tar.gz

tar -zxvf node_exporter-1.3.1.linux-amd64.tar.gz
mv node_exporter-1.3.1.linux-amd64  node_exporter


vi /etc/init.d/node_exporter

#!/bin/bash
#chkconfig: 2345 80 90
#description:Prometheus node exporter
#
# /etc/rc.d/init.d/node_exporter
#
#  Prometheus node exporter
#
#  description: Prometheus node exporter
#  processname: node_exporter

# Source function library.
. /etc/rc.d/init.d/functions

PROGNAME=node_exporter
PROG=/opt/node_exporter/$PROGNAME
USER=root
LOGFILE=/var/log/prometheus.log
LOCKFILE=/var/run/$PROGNAME.pid

start() {
    echo -n "Starting $PROGNAME: "
    cd /opt/node_exporter/
    daemon --user $USER --pidfile="$LOCKFILE" "$PROG &>$LOGFILE &"
    echo $(pidofproc $PROGNAME) >$LOCKFILE
    echo
}

stop() {
    echo -n "Shutting down $PROGNAME: "
    killproc $PROGNAME
    rm -f $LOCKFILE
    echo
}


case "$1" in
    start)
    start
    ;;
    stop)
    stop
    ;;
    status)
    status $PROGNAME
    ;;
    restart)
    stop
    start
    ;;
    reload)
    echo "Sending SIGHUP to $PROGNAME"
    kill -SIGHUP $(pidofproc $PROGNAME)#!/bin/bash
    ;;
    *)
        echo "Usage: service node_exporter {start|stop|status|reload|restart}"
        exit 1
    ;;
esac


chmod +x /etc/init.d/node_exporter

service node_exporter start

chkconfig --add /etc/init.d/node_exporter

chkconfig node_exporter on



iptables -I INPUT -p tcp --dport 9100 -j ACCEPT
service iptables save
```
