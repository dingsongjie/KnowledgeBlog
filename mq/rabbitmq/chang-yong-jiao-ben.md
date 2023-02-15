# 常用脚本

### 添加用户

```bash
rabbitmqctl add_user userName password
```

### 用户添加tag

```bash
rabbitmqctl set_user_tags userName administrator
```

### 用户设置权限

```bash
rabbitmqctl set_permissions -p / userName ".*" ".*" ".*"
```
