### 主机信息

查看主机名`hostname`，可修改

查看发行版本`cat /etc/os-release`

查看系统信息：`uname -a`

查看CPU信息：`lscpu`

查看内存信息：`free -h`

查看磁盘信息：`df -h` 

查看PIC接口信息`lspci -vv`
### 语系检查

系统语系
```
root@RainYun-SHrBEyXy:/usr/share/doc# localectl
System Locale: LANG=en_US.UTF-8
VC Keymap: n/a
X11 Layout: n/a
```
软件语系
```
root@RainYun-SHrBEyXy:/usr/share/doc# locale
LANG=en_US.UTF-8
LANGUAGE=
LC_CTYPE="en_US.UTF-8"
LC_NUMERIC="en_US.UTF-8"
LC_TIME="en_US.UTF-8"
LC_COLLATE="en_US.UTF-8"
LC_MONETARY="en_US.UTF-8"
LC_MESSAGES="en_US.UTF-8"
LC_PAPER="en_US.UTF-8"
LC_NAME="en_US.UTF-8"
LC_ADDRESS="en_US.UTF-8"
LC_TELEPHONE="en_US.UTF-8"
LC_MEASUREMENT="en_US.UTF-8"
LC_IDENTIFICATION="en_US.UTF-8"
LC_ALL=
root@RainYun-SHrBEyXy:/usr/share/doc# 
```

### 登录自动执行脚本

`/etc/profile.d/ `是一个目录，用于存放一系列脚本文件，这些脚本文件在用户登录或者 shell 启动时会被自动执行，目的是为了设置或调整用户的 shell 环境
```bash
## 激活自动执行脚本
cp systeminfo.sh /etc/profile.d/
chmod +x /etc/profile.d/systeminfo.sh
```
```bash

			系统基本信息：
	------------------------------------------------
	Current Time : Sun Jun  9 13:58:33 CST 2024
	Version      : CentOS Linux 7 (Core)
	Kernel       : 3.10.0-1062.el7.x86_64
	Uptime       : up 2 weeks, 1 day, 21 hours, 8 minutes
	IP addr      : 172.16.53.223
	Hostname     : RainYun-mjzwJWoB
	Cpu          : AMD EPYC 7702 64-Core Processor
	Memory       : 239M/990M
	SWAP         : 0B/0B
	Users Logged : 1 users

			cpu的负载情况
	------------------------------------------------
	CPU load in 1  min is:            0.10
	CPU load in 5  min is:            0.09
	CPU load in 10 min is:            0.06

			内存的使用情况
	------------------------------------------------
	内存总容量:     990M
	内存空闲容量:    79M
	内存缓存:      671M

			各分区使用率
	------------------------------------------------
	/dev/sda1                   16%
```