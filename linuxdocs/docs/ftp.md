### FTP
FTP(File Transfer Protocol，文件传输协议)
先简单认识下FTP协议，FTP即文件传输协议的简称，它是TCP/IP协议簇中的一员，也是Internet上最早使用的协议之一，通过它可以实现电脑与电脑间对文件的各种操作（如文件的增、删、改、查、传送等），FTP的目标是提高文件的共享性，提供非直接使用远程计算机，实现计算机文件的相互操作，使存储介质对用户透明和可靠高效地传送数据。
它是基于C/S(客户端/服务端)模型设计，工作在网络体系结构中的应用层，
使用TCP进行传输，保证客户与服务器之间的连接是可靠的。


原文链接：https://blog.csdn.net/qq_40891009/article/details/120497976
### FTP服务器

FTP服务器就是支持FTP协议的服务器，我们平常可以在电脑上安装一个FTP工具就可实现与FTP服务器进行文件传输，FTP服务器常见分为：Windows FTP服务器和Linux FTP服务器。
我们自己的电脑也可以当做一个FTP服务器，如Windows系统就可以通过自带的ISS管理器来搭建一个FTP服务器(本文案例就是使用这个)，Linux系统最常用的借助vsftp软件做FTP服务器搭建。
常见的例子： 在学校里上电脑课或者电脑考试时，老师会将上课题目或者考试题目放在某个文件夹中，让学生访问某个地址如：ftp://ip地址，通过这个地址每位同学看到老师共享的文件，下载的对应的试题完成考试。
上面例子上过电脑课的同学应该都经历过(多么美好的学生时代)，学生们访问到的其实就是老师搭建好的FTP服务器，老师提前将共享的文件上传到FTP服务器，学生们可以进行下载等操作。


### FTP服务器客户端

1. 使用命令行FTP客户端

输入ftp并按Enter打开FTP客户端
使用open命令连接到FTP服务器，例如：open ftp.example.com。
输入用户名和密码进行登录。
user：输入用户名。
ftp> user your_username
pass：输入密码。
ftp> pass your_password
ls：列出当前目录的文件和文件夹。
ftp> ls
cd：更改当前目录。
ftp> cd folder_name
get：从FTP服务器下载文件到本地计算机。
ftp> get file_name
put：将本地计算机上的文件上传到FTP服务器。
ftp> put file_name
delete：从FTP服务器删除文件。
ftp> delete file_name
rmdir：从FTP服务器删除文件夹。
ftp> rmdir folder_name
mkdir：在FTP服务器上创建新文件夹。
ftp> mkdir folder_name
quit：断开与FTP服务器的连接并退出FTP客户端。
ftp> quit

2. 使用Web浏览器
   某些FTP服务器可以通过Web浏览器直接访问。只需在浏览器地址栏输入FTP服务器的URL，格式如下：
ftp://ftp.example.com
如果服务器配置允许匿名访问，你可能可以直接浏览文件。否则系统会提示输入用户名和密码

3. 使用第三方应用程序或插件
   有些应用程序或浏览器插件提供了FTP功能，可以在不安装专用FTP客户端的情况下访问FTP服务器。例如，一些文件管理器应用程序可能包含FTP支持，或者你可以安装浏览器扩展来增加FTP功能。