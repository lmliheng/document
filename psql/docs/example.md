### 备份
```bash
[root@RainYun-gst9yeON ~]# sudo -u postgres psql
could not change directory to "/root"
psql (9.2.24, server 14.12)
WARNING: psql version 9.2, server version 14.0.
         Some psql features might not work.
Type "help" for help.

postgres=# ALTER USER postgres WITH PASSWORD 'postgres';
ALTER ROLE
postgres=# CREATE DATABASE wiki;
CREATE DATABASE
postgres=# \l
                                  List of databases
   Name    |  Owner   | Encoding |   Collate   |    Ctype    |   Access privileges   
-----------+----------+----------+-------------+-------------+-----------------------
 postgres  | postgres | UTF8     | en_US.UTF-8 | en_US.UTF-8 | 
 template0 | postgres | UTF8     | en_US.UTF-8 | en_US.UTF-8 | =c/postgres          +
           |          |          |             |             | postgres=CTc/postgres
 template1 | postgres | UTF8     | en_US.UTF-8 | en_US.UTF-8 | =c/postgres          +
           |          |          |             |             | postgres=CTc/postgres
 wiki      | postgres | UTF8     | en_US.UTF-8 | en_US.UTF-8 | 
(4 rows)

postgres=# \q
[root@RainYun-gst9yeON ~]# psql -U postgres -h localhost -p 5432 -d wiki < /root/wiki_backup.sql
```

### 注意创建数据库
执行创建数据库操作前空一格
```bash
postgres-# CREATE DATABASE template;
ERROR:  syntax error at or near "CREATE"
LINE 2: CREATE DATABASE template;
        ^
postgres=#  CREATE DATABASE template;
CREATE DATABASE
postgres=# 

```
