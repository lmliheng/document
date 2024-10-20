### 连接

查看版本
```bash
psql -V
```

查看PostgreSQL配置文件：
```bash
sudo vim /etc/postgresql/<version>/main/postgresql.conf
查找：sudo find / -type f -name "postgresql.conf" 2>/dev/null
```

登录PostgreSQL：
你可以尝试以PostgreSQL的用户身份登录数据库来进一步验证服务状态。首先切换到PostgreSQL用户：
```bash
sudo su - postgres
```
或者
psql -U 用户名 -h 主机名 -p 端口号，输入密码后将进入psql命令行界面
例如：
```bash
psql -U postgres -h localhost -p 5432
```

然后尝试直接进入PostgreSQL的交互式终端：
```bash
psql
```

查看数据库状态：
```bash
\conninfo
```

