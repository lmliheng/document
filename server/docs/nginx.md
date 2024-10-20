### Linux安装
1. 安装必要的依赖包，如 gcc、zlib、pcre-devel、openssl 和 wget。
2. 下载 Nginx 安装包并解压到指定目录。
3. 编译并安装 Nginx。
4. 将 Nginx 的可执行文件路径添加到系统的 PATH 环境变量中。
5. 将 Nginx 注册为系统服务，以便可以使用 systemctl 命令来管理 Nginx 服务。
#### 快速安装
要求：`linux centos 7.x`

执行命令:`curl -O https://heng1.oss-cn-beijing.aliyuncs.com/nginx_install_three.sh && bash nginx_install_three.sh`

[脚本来源](https://heng1.oss-cn-beijing.aliyuncs.com/nginx_install_three.sh)

```bash
[root@RainYun-qrmHoit1 ~]# curl -O https://heng1.oss-cn-beijing.aliyuncs.com/nginx_install_three.sh && bash nginx_install_three.sh
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100  2921  100  2921    0     0   2312      0  0:00:01  0:00:01 --:--:--  2314
检测网络正常！
配置阿里源输入1，任意键跳过配置：1
正在配置阿里源...
阿里源配置已完成！
正在安装依赖包...
依赖包安装已完成！
正在下载安装包和解压安装操作...
Nginx 安装已完成！路径为/usr/local/nginx
#####################################
启动Nginx: nginx
停止Nginx: nginx -s stop
重载Nginx: nginx -s reload
检查Nginx: nginx -t
注意运行命令：source /etc/profile
#####################################
```

#### 正常安装注意点
重点：软链接创建和服务注册
添加软链接
```bash
[root@RainYun-x6pWTQo0 nginx]# vim /etc/profile
写入export PATH=$PATH:/usr/local/nginx/sbin
```
激活软链接
```bash
[root@RainYun-x6pWTQo0 nginx]# source /etc/profile
```
将nginx注册为系统服务
创建 Nginx 服务文件：在 /etc/systemd/system 目录下创建一个名为 nginx.service 的文件,内容如下

```bash
[Unit]
Description=The nginx HTTP and reverse proxy server
After=syslog.target network.target remote-fs.target nss-lookup.target

[Service]
Type=forking
PIDFile=/usr/local/nginx/logs/nginx.pid
ExecStartPre=/usr/local/nginx/sbin/nginx -t
ExecStart=/usr/local/nginx/sbin/nginx
ExecReload=/usr/local/nginx/sbin/nginx -s reload
ExecStop=/bin/kill -s QUIT $MAINPID
PrivateTmp=true

[Install]
WantedBy=multi-user.target
```
重新加载 systemd 配置：`sudo systemctl daemon-reload`
注意nginx查找静态资源权限问题,必要时`修改配置文件使用者为root`


### 负载均衡策略

参考[《Nginx负载均衡+高可用配置》](https://blog.csdn.net/IT_10/article/details/89365436)

`后端业务服务器的IP不会暴露`
#### demo
调度服务器配置
```bash
http {
    upstream backend {
        server 154.64.230.184;
        server 154.9.228.106;
    }

    server {
        listen       80;
        server_name     nginx.hengsir.work;
        location / {
             proxy_pass http://backend;
        }
    }
```
其他的业务服务器按照server正常配置就行，此时业务服务器采用80端口
那么让业务服务器使用其他端口呢


### 跨域配置

```bash
location / {
    # 其他配置...

    # 设置CORS响应头
    add_header 'Access-Control-Allow-Origin' '*';
    add_header 'Access-Control-Allow-Methods' 'GET, POST, OPTIONS, PUT, DELETE';
    add_header 'Access-Control-Allow-Headers' 'DNT,User-Agent,X-Requested-With,If-Modified-Since,Cache-Control,Content-Type,Range,Authorization';
    add_header 'Access-Control-Expose-Headers' 'Content-Length,Content-Range';

    # 如果请求方法是OPTIONS，直接返回200
    if ($request_method = 'OPTIONS') {
        add_header 'Access-Control-Max-Age' 1728000;
        add_header 'Content-Type' 'text/plain; charset=utf-8';
        add_header 'Content-Length' 0;
        return 200;
    }
}
```

### 反向代理之内部和上游
内部代理
```bash
  server {
    listen 80; # 监听的端口
    server_name proxy.liheng.work; # 你的域名

    location / {
        proxy_pass http://127.0.0.1:5000; # 后端服务器地址和端口
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }
}

```
上游参照负载均衡策略


### 防盗链配置

```bash
   server {
        listen 80;
        server_name img.liheng.work;
        root /root/static/img;
        index index.html;
        location / {
         }
        location ~ \.(jpg|png|gif|jpeg)$ {
            valid_referers home.liheng.work;
            valid_referers img.liheng.work;
            if ($invalid_referer) {
                 rewrite ^/ http://web.liheng.work/images/logos/favicon.ico;


            #return 403;

                  }
           }
        error_page   404 403 501 502 503 504 505  /50x.html;
        location = /50x.html {
            root   html;
        }
}

```
location ~ \.(jpg|png|gif|jpeg)$ {}为设置防盗链的文件类型，使用竖线|分隔
valid_referers site1.test.com *.nginx.org;为白名单，使用空格分隔，可以使用*进行泛域名设置。
if ($invalid_referer) {}为判断是否符合白名单，不符合白名单将执行{}内的内容,本身需要写进去
rewrite ^/ http://site3.test.com/notfound.jpg;为重写资源，如果不符白名单，则重写为该地址
return 403;代表返回的状态码为403

### 自定义错误页面
路径`/usr/local/nginx/html`（nginx根目录下）
```bash
        error_page   404 403 501 502 503 504 505  /50x.html;
        location = /50x.html {
            root   html;
        }
```        

### nginx上游服务器资源会不会经过nginx，还是直接流向客户端？

当Nginx配置为一个反向代理服务器时，其主要职责之一就是接收来自客户端的请求，并将这些请求转发到所谓的上游服务器（也称为后端服务器）。上游服务器通常是指实际提供服务的应用服务器，比如运行Web应用程序的服务器。

当客户端请求到达Nginx时，Nginx会根据其配置文件中定义的规则将请求转发给上游服务器。上游服务器处理完请求后，生成的响应会回传给Nginx，Nginx再将这个响应返回给客户端。因此，上游服务器的资源确实会经过Nginx，Nginx不仅仅作为一个简单的通道，它还可能对请求和响应进行一些额外的处理，例如：

1. **负载均衡**：Nginx可以根据配置将请求分发给不同的上游服务器，以达到负载均衡的目的。
2. **缓存**：Nginx可以缓存上游服务器的响应，如果后续请求相同，可以直接从缓存中读取数据，而不必再次请求上游服务器。
3. **SSL终止**：Nginx可以处理SSL/TLS加密，这意味着所有到客户端的加密通信都在Nginx这一层处理，上游服务器可以使用未加密的通信。
4. **压缩**：Nginx可以压缩从上游服务器获取的数据，以便更高效地传输给客户端。
5. **安全性和访问控制**：Nginx可以作为防火墙，阻止恶意请求到达上游服务器，并且可以基于IP或其他条件限制对资源的访问。

简而言之，上游服务器的资源会经过Nginx，而Nginx作为反向代理可以提供多种增值服务。


### 异常
Nginx启动报错，意味尽管配置文件正确，启动还是异常，可能是代理服务器或者内部服务器异常
```bash
Job for nginx.service invalid.
```

nginx自身`80端口被占用`，无法启动，将web项目改为其他就行了

```bash
[root@iZbp1b2qvla6v42j8llwn1Z ~]# systemctl status nginx.service
● nginx.service - The nginx HTTP and reverse proxy server
   Loaded: loaded (/etc/systemd/system/nginx.service; disabled; vendor preset: disabled)
   Active: failed (Result: exit-code) since Thu 2024-06-06 21:45:11 CST; 5min ago
  Process: 11310 ExecStart=/usr/local/nginx/sbin/nginx (code=exited, status=1/FAILURE)
  Process: 11308 ExecStartPre=/usr/local/nginx/sbin/nginx -t (code=exited, status=0/SUCCESS)

Jun 06 21:45:08 iZbp1b2qvla6v42j8llwn1Z nginx[11310]: nginx: [emerg] bind() to 0.0.0.0:80 failed (98: Address already in use)
Jun 06 21:45:11 iZbp1b2qvla6v42j8llwn1Z nginx[11310]: nginx: [emerg] still could not bind()
Jun 06 21:45:11 iZbp1b2qvla6v42j8llwn1Z systemd[1]: nginx.service: control process exited, code=exited status=1
Jun 06 21:45:11 iZbp1b2qvla6v42j8llwn1Z systemd[1]: Failed to start The nginx HTTP and reverse proxy server.
Jun 06 21:45:11 iZbp1b2qvla6v42j8llwn1Z systemd[1]: Unit nginx.service entered failed state.
Jun 06 21:45:11 iZbp1b2qvla6v42j8llwn1Z systemd[1]: nginx.service failed.
[root@iZbp1b2qvla6v42j8llwn1Z ~]# sudo systemctl restart nginx
Job for nginx.service failed because the control process exited with error code. See "systemctl status nginx.service" and "journalctl -xe" for details.

```


### 内核优化

```bash
user  root;
worker_processes  2;


worker_cpu_affinity 01 10;
#error_log  logs/error.log;
#error_log  logs/error.log  notice;
#error_log  logs/error.log  info;

#pid        logs/nginx.pid;


events {
    worker_connections  4096;
    use epoll;
}

```

### 压缩资源

```bash
   # 启动内容压缩，有效降低网络流量
    gzip  on;
    # 过短的内容压缩效果不佳，压缩过程还会浪费系统资源
    gzip_min_length 10k;
    # 可选值1~9,压缩级别越高压缩率越高，但对系统性能要求越高
    gzip_comp_level 4;
    # 压缩的内容类别
    gzip_types text/plain text/css application/javascript application/x-javascript application/json text/xml application/xml application/xml+rss application/x-httpd-php text/javascript image/jpeg image/gif image/png;
    # 是否在http header中添加Vary: Accept-Encoding，建议开启
    gzip_vary on;
    gzip_static on;
    sendfile        on;
```


### SSL

注意需要`ngx_http_ssl_module`才能使用SSL

检查`nginx -V 2>&1 | grep -o 'http_ssl_module'`，若没有输出`http_ssl_module`则没有该模块需要重新编译nginx
```bash
[root@RainYun-qrmHoit1 ~]# nginx -V 2>&1 | grep -o 'http_ssl_module'
http_ssl_module
```


自签名
```bash
[root@RainYun-mjzwJWoB ssl]# openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout /usr/local/nginx/ssl/nginx.key -out /usr/local/nginx/ssl/nginx.crt -subj "/C=US/ST=china/L=changsha/O=centrlsouthuniversity/CN=img.liheng.work"
Generating a 2048 bit RSA private key
.......................+++
....................................................................................................................................................................................................+++
writing new private key to '/usr/local/nginx/ssl/nginx.key'
-----
[root@RainYun-mjzwJWoB ssl]# 
```
配置
```bash
server {
    listen 80;
    server_name img.liheng.work;
    return 301 https://$host$request_uri;
}

server {
    listen 443 ssl;
    server_name img.liheng.work;

    ssl_certificate /usr/local/nginx/ssl/nginx.crt;
    ssl_certificate_key /usr/local/nginx/ssl/nginx.key;
    ssl_protocols TLSv1 TLSv1.1 TLSv1.2;
    ssl_ciphers 'TLS_AES_128_GCM_SHA256:TLS_AES_256_GCM_SHA384:TLS_CHACHA20_POLY1305_SHA256:ECDHE-RSA-AES128-GCM-SHA256:ECDHE-RSA-AES256-GCM-SHA384';
    ssl_prefer_server_ciphers on;
    ssl_session_cache shared:SSL:10m;

    ## 将 root 指令更改为您的网站根目录
             root  /root/static/img;
             index index.html index.htm;
    
                 location / {
                         try_files $uri $uri/ =404;
                             }
                             }
```     


### 伪静态配置
```bash
location / {
  try_files $uri $uri/ /index.html;
}
```