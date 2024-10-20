### 目录和文件操作

创建目录`mkdir`
删除文件`rm`
删除目录`rmdir`
重命名
移动`mv`
复制`cp`
编辑`vim`
查看文件内容`cat`
切换目录`cd`

### 切换目录
cd（change directory)
```angular2html
切换至某目录（离所在目录较远），推荐使用绝对路径如cd /etc/nginx
使用相对路径切换至上一目录cd ..
```

### 展示目录
文件信息
```
$ ls       # 仅列出当前目录可见文件
$ ls -l    # 列出当前目录可见文件详细信息
$ ls -hl   # 列出详细信息并以可读大小显示文件大小
$ ls -al   # 列出所有文件（包括隐藏）的详细信息
```
目录路径
```angular2html
pwd
```
### 修改文件属性和权限

r(read):4,w(write):2,x(执行)：1
rwxrwxrwx表示三种身份owner，group,others有全部权限
以下命令实现文件权限修改
```angular2html
root@RainYun-SHrBEyXy:~# ls -l
total 4
-rw-r--r-- 1 root root 40 May  9 23:48 hello.sh
root@RainYun-SHrBEyXy:~# chmod 777 hello.sh
root@RainYun-SHrBEyXy:~# ls -l
total 4
-rwxrwxrwx 1 root root 40 May  9 23:48 hello.sh
root@RainYun-SHrBEyXy:~#
```

### 文件查找
find

locate

whereis

### 可执行文件路径变量PATH
常称为环境变量

### 安装.deb文件
安装.deb文件，你需要使用dpkg命令
打开终端（快捷键：Ctrl + Alt + T）。
使用cd命令导航到包含clashcn.com_clash-verge_1.5.11_amd64.deb文件的目录。例如，如果文件位于~/Downloads目录中，输入：
```bash
cd ~/Downloads
```
使用dpkg命令安装.deb文件：
```bash
sudo dpkg -i xxx.deb
```
输入你的用户密码（如果需要）。
安装完成

### 执行.sh文件
权限`chmod`
使用cd命令导航到包含upgrade.sh文件的目录：
为upgrade.sh文件添加可执行权限：
```bash
chmod +x upgrade.sh
```
执行upgrade.sh脚本：
```bash
sudo ./upgrade.sh
```