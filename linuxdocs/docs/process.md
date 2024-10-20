## 进场管理
### 检查进程PID
`lsof`（查看PID）,`ps`,`top`

进程（PID），PID就是程序在内存单元的唯一标识符
其实长期稳定运行的进程也就是服务，比如nginx web服务，后端python持续响应代码
### 杀死进程
`kill PID`

彻底`sudo fuser -k 80/tcp`

### 查看进程占用资源

`free`

### 进程和网络监控

`netstat`


### 定时任务

检查cron服务是否正在运行：
```shell
sudo systemctl status cron或者ceond
```
或者，对于使用systemd的系统：
```shell
sudo systemctl status cronie
```
如果cron服务未运行，请使用以下命令启动它：
```shell
sudo systemctl start cron
```
编辑crontab文件
```shell
crontab -e
```
在打开的编辑器中，添加一行以设置定时任务。例如，要每天凌晨1点运行Python脚本，请添加以下行
```shell
0 1 * * * /usr/bin/python3 /path/to/your/script.py
```
列出当前用户的crontab条目：
```shell
crontab -l
```
查看cron日志，您需要找到正确的日志文件。在某些系统上，cron日志可能位于/var/log/cron或/var/log/syslog。请尝试以下命令查找cron日志：
不建议使用cron的日志
```shell
grep CRON /var/log/cron
```
