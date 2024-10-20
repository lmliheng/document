### nginx安装
```shell
#!/bin/bash

# nginx安装包链接
nginx_url="http://nginx.org/download/nginx-1.18.0.tar.gz"
# 下载包存放路径
path="/tmp/"
# 安装路径
int_path="/usr/local/nginx"

# 首先检查网络，114.114.114.114 是一个公共 DNS 服务器地址
ping -c 1 114.114.114.114 > /dev/null 2>&1
if [ $? -eq 0 ];then
    echo "检测网络正常！"

    # 配置阿里源
    read -p "配置阿里源输入1，任意键跳过配置：" number
    case "$number" in
        1)
          echo "正在配置阿里源..."
          mv /etc/yum.repos.d/CentOS-Base.repo /etc/yum.repos.d/CentOS-Base.repo.backup  > /dev/null 2>&1
          wget -O /etc/yum.repos.d/CentOS-Base.repo https://mirrors.aliyun.com/repo/Centos-7.repo > /dev/null 2>&1
          yum clean all > /dev/null 2>&1
          yum makecache > /dev/null 2>&1
          echo "阿里源配置已完成！"
        ;;
        *)
        echo "已跳过配置阿里源！"
    esac

    # 安装依赖包
    echo "正在安装依赖包..."
    yum -y install gcc zlib zlib-devel pcre-devel openssl openssl-devel wget > /dev/null 2>&1
    if [ $? -eq 0 ];then
        echo "依赖包安装已完成！"

        # 下载Nginx包
        echo "正在下载安装包和解压安装操作..."
        wget $nginx_url -P $path > /dev/null 2>&1
        # 创建文件夹，解压安装
        mkdir $int_path && cd $int_path
        nginx_pack=`echo $nginx_url | awk -F '/' '{print $NF}'`
        tar -xf $path/$nginx_pack -C ./

        # 编译安装
        nginx_path=`echo $nginx_pack |awk -F '.' '{print $1"."$2"."$3}'`
        cd $nginx_path && ./configure > /dev/null 2>&1
        make > /dev/null 2>&1
        make install  > /dev/null 2>&1
        echo "Nginx 安装已完成！路径为/usr/local/nginx"

        # 添加软链接
        echo "export PATH=\$PATH:/usr/local/nginx/sbin" >> /etc/profile
        source /etc/profile

        # 将nginx注册为系统服务
        cat > /etc/systemd/system/nginx.service <<EOF
[Unit]
Description=The nginx HTTP and reverse proxy server
After=syslog.target network.target remote-fs.target nss-lookup.target

[Service]
Type=forking
PIDFile=/usr/local/nginx/logs/nginx.pid
ExecStartPre=/usr/local/nginx/sbin/nginx -t
ExecStart=/usr/local/nginx/sbin/nginx
ExecReload=/usr/local/nginx/sbin/nginx -s reload
ExecStop=/bin/kill -s QUIT \$MAINPID
PrivateTmp=true

[Install]
WantedBy=multi-user.target
EOF

        # 重新加载 systemd 配置
        sudo systemctl daemon-reload

        echo -e "#####################################\n启动Nginx: nginx\n停止Nginx: nginx -s stop\n重载Nginx: nginx -s reload\n检查Nginx: nginx -t\n#####################################"
    else
        echo "依赖包安装失败，请检查yum源或者网络问题！！！"
        exit 1
    fi
else
    echo "检测网络连接异常，请检查网络再操作！"
    exit 1
fi

```