## 检查PostgreSQL进程
使用以下命令来查看是否有PostgreSQL进程正在运行：
```bash
ps -ef | grep postgres
```

## 检查监听端口：
检查PostgreSQL默认端口5432是否已被监听：
```bash
netstat -tuln | grep 5432
```
如果端口处于监听状态，说明PostgreSQL服务已经启动并且在等待连接。

## 启动停止PostgreSQL服务
```bash
sudo systemctl start/stop postgresql-14.service
```

## 查看PostgreSQL服务状态
```bash
systemctl status postgresql-14
```