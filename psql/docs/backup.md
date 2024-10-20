## 备份与还原
PostgreSQL（psql）数据库迁移到另一台服务器

在源服务器上使用pg_dump命令备份数据库。创建一个SQL文件，其中包含数据库的结构和数据
```bash
pg_dump -U 用户名 -h 源服务器主机名 -p 源服务器端口号 -F t 数据库名 > 备份文件名.sql
如下
pg_dump -U postgres -h localhost -p 5432 -F t mydb > mydb_backup.sql
```
这将在当前目录下创建一个名为mydb_backup.sql的文件，其中包含mydb数据库的结构和数据

将备份文件传输到目标服务器，在目标服务器上创建新数据库：

在目标服务器上，使用psql命令行界面创建一个新的数据库，恢复备份文件：

使用pg_restore命令将备份文件恢复到新创建的数据库中。以下是一个示例命令：
```bash
pg_restore -U 目标服务器用户名 -h 目标服务器主机名 -p 目标服务器端口号 -d 新数据库名 -1 /path/to/备份文件名.sql
如下
pg_restore -U postgres -h localhost -p 5432 -d mydb_new -1 /home/user/mydb_backup.sql
```
这将把备份文件中的数据和结构恢复到新创建的数据库中。

最后验证数据迁移，查询数据以确保数据迁移成功
