## Node

### 安装Node.js：
使用包管理器（如apt或yum）安装Node.js：sudo apt-get install nodejs（适用于Debian/Ubuntu）或sudo yum install nodejs（适用于CentOS/RHEL）

使用Node Version Manager（nvm）安装Node.js：安装nvm：curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.38.0/install.sh | bash

重启终端并运行nvm ls以查看可用的Node.js版本。

安装特定版本的Node.js，例如：nvm install 14.17.0

使用特定版本的Node.js：nvm use 14.17.0

创建新的Node.js项目：使用npm init命令创建一个新的Node.js项目，该命令将引导您完成项目设置过程

安装Node.js模块：使用npm install<module_name>命令安装模块，例如：npm install express

要将模块添加到项目的package.json文件中，使用npm install<module_name> --save

要安装全局模块，使用npm install -g<module_name>

运行Node.js应用程序：使用node <file_name>命令运行Node.js应用程序，例如：node app.js

查看Node.js版本：使用`node -v`命令查看当前安装的Node.js版本。

查看Node.js模块：`npm list -g`命令查看全局安装的Node.js模块。

更新Node.js模块：`npm update<module_name>`

卸载Node.js模块：`npm uninstall<module_name>`

卸载全局模块`npm uninstall -g<module_name>`

安装特定版本npm:`npm install -g npm@<version>`,匹配node版本
```bash
C:\Users\李恒\Desktop\code\react\Mangement_Info_font>npx create-react-app student-info-management
npm WARN cli npm v10.5.0 does not support Node.js v16.20.2. This version of npm supports the following node versions: `^18.17.0 || >=20.5.0`. You can find the latest version at https://nodejs.org/.

C:\Users\李恒\Desktop\code\react\Mangement_Info_font>npm install -g npm@8

removed 69 packages, and changed 103 packages in 2s

11 packages are looking for funding
  run `npm fund` for details

C:\Users\李恒\Desktop\code\react\Mangement_Info_font>npm -v
8.19.4
```