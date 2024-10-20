## linux部署PHP(使用nginx)
### nginx配置
nginx的server块配置
```bash
   server {
            listen  80;
            server_name php.liheng.work; # 更改为你自己的域名

            root /home/site/navagsnsite; # 更改为你项目的根目录

            index index.php index.html index.htm;

      # 静态文件处理
        location / {
                try_files $uri $uri/ =404; }

         # PHP 请求处理
         location ~ \.php$ {

            fastcgi_pass 127.0.0.1:9000;
            fastcgi_index index.php;
            fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
            include fastcgi_params;
                    }
                  # 错误页面
 }

```
### 使用PHP-PFM
确保PHP-FPM配置文件中的listen指令设置为正确的地址和端口。编辑PHP-FPM配置文件（通常位于/etc/php-fpm.d/www.conf 或 /etc/php/7.4/fpm/pool.d/www.conf），找到listen指令
```bash
listen = 127.0.0.1:9000
```
使PHP-FPM监听IP地址127.0.0.1上的端口9000,请确保这与Nginx配置文件中的fastcgi_pass指令相匹配

重启PHP-FPM服务以应用更改：
```bash
sudo systemctl restart php-fpm
```
确保PHP-FPM服务已启动并正在运行：
```bash
sudo systemctl status php-fpm
```


