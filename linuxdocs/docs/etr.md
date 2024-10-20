### 基础
`./`表示本目录,比如cd ..（省略/)
`../`表示上一目录,比如./hello.sh
### linux文件数据
路径 `/usr/share/doc`

### 欢迎语设置
`vim /etc/motd`

### 动画
[参考](https://juejin.cn/post/7153234992640819230?share_token=2459085b-d4b4-45b4-8d09-41efca3fbc0c)


### SSH连接banner设置
`目的`：在SSH连接成功后了解服务器地址，期限，拥有者，服务器硬件配置，环境变量等重要信息

雨云服务器SS连接成功后展示的内容
```
WARNING! The remote SSH server rejected X11 forwarding request.
Linux RainYun-SHrBEyXy 5.10.0-28-amd64 #1 SMP Debian 5.10.209-2 (2024-01-31) x86_64
Welcome to RainYun Cloud Services                                                                                                                                                    
Check out the latest activities or get help from: https://www.rainyun.com
Last login: Wed Aug 17 21:26:05 2022
```
本文会实现linux中设置ssh登录时显示的banner自定义
启用Banner功能，编辑/etc/ssh/sshd_config文件
```angular2html
sudo vim /etc/ssh/sshd_config
```
文件中找到Banner选项（如果存在），并取消注释。
如果Banner选项不存在，请将其添加到文件中。例如：
```angular2html
Banner /etc/ssh/banner.txt
```
上传/etc/ssh/banner.txt文件
重新启动SSH服务以使更改生效。在大多数Linux发行版中可以使用以下命令重启SSH服务：
```
sudo systemctl restart ssh
```
或者
```
sudo service ssh restart
```
增加后
```angular2html
 __
| |__     ___   _ __     __ _
| '_ \   / _ \ | '_ \   / _` |
| | | | |  __/ | | | | | (_| |
|_| |_|  \___| |_| |_|  \__, |
                        |___/
_________________________________________
Manger:liheng
Aera:China shuqian
System:Linux  Debian 11
Create_time:2024-04-14
End_time:2024-5-15
IP:103.40.13.71
_________________________________________
WARNING! The remote SSH server rejected X11 forwarding request.
Linux RainYun-SHrBEyXy 5.10.0-28-amd64 #1 SMP Debian 5.10.209-2 (2024-01-31) x86_64
Welcome to RainYun Cloud Services
Check out the latest activities or get help from: https://www.rainyun.com
Last login: Thu May  9 22:57:16 2024 from 120.227.56.74
root@RainYun-SHrBEyXy:~# ~
```

### 按键内容
```
root@RainYun-SHrBEyXy:/usr/share/doc# stty -a
speed 38400 baud; rows 56; columns 259; line = 0;
intr = ^C; quit = ^\; erase = ^?; kill = ^U; eof = ^D; eol = <undef>; eol2 = <undef>; swtch = <undef>; start = ^Q; stop = ^S; susp = ^Z; rprnt = ^R; werase = ^W; lnext = ^V; discard = ^O; min = 1; time = 0;
-parenb -parodd -cmspar cs8 -hupcl -cstopb cread -clocal -crtscts
-ignbrk -brkint -ignpar -parmrk -inpck -istrip -inlcr -igncr icrnl ixon -ixoff -iuclc -ixany -imaxbel -iutf8
opost -olcuc -ocrnl onlcr -onocr -onlret -ofill -ofdel nl0 cr0 tab0 bs0 vt0 ff0
isig icanon iexten echo echoe echok -echonl -noflsh -xcase -tostop -echoprt echoctl echoke -flusho -extproc
root@RainYun-SHrBEyXy:/usr/share/doc# 
```

### 时间
```bash
time
或者
time ls -l
```


