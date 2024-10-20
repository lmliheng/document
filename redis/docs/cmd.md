### 检查 redis-cli 是否可用：
```bash
which redis-cli
```

### 打开Redis 客户端
```bash
redis-cli
```
### 输入密码提示:
```bash
NOAUTH Authentication required.
```
输入密码：AUTH 密码

### 检测 redis 服务是否启动
```bash
$ redis-cli
redis 127.0.0.1:6379>
redis 127.0.0.1:6379> PING

PONG
```

### 重启redis服务
```bash
sudo systemctl restart redis
```

### info命令:
```bash
info
```
info命令用于获取Redis服务器信息。

