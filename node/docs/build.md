## 部署

注意`pm2`仅在node环境下运行，注意检查node

1） nohup
```bash
nohup node server &
```

2) PM2
使用 npm 安装 pm2：
```bash
sudo npm install -g pm2
```
使用 pm2 启动 Wiki.js 服务器：
```bash
pm2 start server
```
要确保 pm2 在系统重启后自动启动 Wiki.js 服务器，运行以下命令：
```bash
pm2 startup
```
然后按照终端中显示的说明操作。

保存当前 pm2 进程列表：
```bash
pm2 save
```
现在，Wiki.js 服务器将由 pm2 管理并在后台持续运行。即使在系统重启后，pm2 也会自动启动 Wiki.js 服务器。

要查看 pm2 管理的进程列表，运行以下命令：
```bash
pm2 list
```
要查看 Wiki.js 服务器的日志，运行以下命令：
```bash
pm2 logs
```
要停止 Wiki.js 服务器，运行以下命令：
```bash
pm2 stop server.js
```
要重启 Wiki.js 服务器，运行以下命令：
```bash
pm2 restart server.js
```

3) forever

使用 npm 安装 forever：
```bash
sudo npm install -g forever
```
使用 forever 启动 Wiki.js 服务器：
```bash
forever start server.js
```
这将在后台启动 Wiki.js 服务器，并确保它持续运行。

要查看由 forever 管理的进程列表，运行以下命令：
```bash
forever list
```
要查看 Wiki.js 服务器的日志，运行以下命令：
```bash
forever logs server.js
```
或者，你可以查看特定进程的日志：
```bash
forever logs<process_id>
```
将<process_id>` 替换为实际的进程 ID。

要停止 Wiki.js 服务器，运行以下命令：
```bash
forever stop server.js
```
或者，你可以停止特定进程：
```bash
forever stop<process_id>
```
将<process_id>` 替换为实际的进程 ID。

要重启 Wiki.js 服务器，运行以下命令：
```bash
forever restart server.js
```