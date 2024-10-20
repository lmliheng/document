# Hello , 我是恒

## 文档

参考[官方文档](http://www.postgres.cn/docs/14/index.html)



## 一键部署
一键部署psql14：`curl -O https://heng1.oss-cn-beijing.aliyuncs.com/psql_install.sh && bash psql_install.sh`

修改密码：
```bash
[root@RainYun-mjzwJWoB ~]# sudo -u postgres psql -c "ALTER USER postgres WITH PASSWORD 'postgres';"
could not change directory to "/root"
ALTER ROLE
[root@RainYun-mjzwJWoB ~]# 
```

脚本配置默认账号：`postgres`,修改后密码：`postgres`


## 检查软件路径
```bash
[root@RainYun-Q7c3pCXM pgsql-14]# cd /var/lib/pgsql/14
[root@RainYun-Q7c3pCXM 14]# ls
backups  data  initdb.log
[root@RainYun-Q7c3pCXM 14]# cd /usr/pgsql-14
[root@RainYun-Q7c3pCXM pgsql-14]# ls
bin  lib  share
```

