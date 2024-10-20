禁用防火墙根据防火墙工具进行操作

1. 使用 iptables

要禁用 iptables，请运行以下命令：
```
sudo iptables -P INPUT ACCEPT
sudo iptables -P FORWARD ACCEPT
sudo iptables -P OUTPUT ACCEPT
sudo iptables -t nat -F
sudo iptables -t mangle -F
sudo iptables -F
sudo iptables -X
```
这些命令将清除所有 iptables 规则并允许所有传入、传出和转发流量。

2. 使用 firewalld

要禁用 firewalld，请运行以下命令：
```
sudo systemctl stop firewalld
sudo systemctl disable firewalld
```
这些命令将停止 firewalld 服务并禁用其自动启动。

3. 使用 ufw

要禁用 ufw，请运行以下命令：
```
sudo ufw disable
```
这个命令将禁用 ufw 防火墙。