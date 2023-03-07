# 双网卡，跨网段配置

### 关闭默认路由的反向路由检查

```bash
echo 0 > /proc/sys/net/ipv4/conf/all/rp_filter
echo 0 > /proc/sys/net/ipv4/conf/<网卡名>/rp_filter
```
