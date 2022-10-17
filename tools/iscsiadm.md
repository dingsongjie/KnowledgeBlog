# iscsiadm

### 发现Target

iscsiadm -m discovery -t st -p \[ip:port]

### 登陆Target

iscsiadm -m node -T \[iqn.2015.06.cn.hrbyg.www.ygcs.c0a802b8:wzg] -l

### 退出登陆

iscsiadm -m node -T \[iqn.2015.06.cn.hrbyg.www.ygcs.c0a802b8:wzg] -u

### 查看当前连接

iscsiadm -m session

### 开机自动连接

iscsiadm -m node -o update -n node.startup -v automatic -T  \[iqn.2015.06.cn.hrbyg.www.ygcs.c0a802b8:wzg]
