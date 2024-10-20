### 工作流

远程仓库为空仓库时使用`git init`产生.git文件并同目录下文件为工作区文件实现本地仓库初始化

远程仓库不为空仓库时，先克隆仓库
```
git clone https://github.com/yourusername/your-repo.git
或者加上特定分支
git clone -b main --single-branch https://github.com/lmliheng/codes.git
```
查看当前工作区的状态
```
git status
```
将未跟踪的文件添加到暂存区
```
git add .
```
将暂存区中的更改提交到本地仓库，双引号下为描述字段
```
git commit -m "Add new files"
```
添加远程仓库（或者用该目录下克隆再初始化init）
```
git remote add origin https://github.com/yourusername/your-repo.git
```
我的默认分支一般是master，可设置
如果要创建一个新分支main并立即切换到它
```
git checkout -b main
```
将本地分支推送到远程仓库
```
git push origin main
```

### 补充
使用git status命令查看当前工作区的状态。如果有未跟踪的文件，请使用git add <file>命令将它们添加到暂存区。使用git add .将当前目录中的所有更改添加到暂存区

使用git commit -m<commit_message>"命令将暂存区中的更改提交到本地仓库。<commit_message>是对此次提交的简短描述。

使用git remote add origin <repository_url>命令添加远程仓库（如果尚未添加）。<remote_name>通常为origin。

使用git push origin <branch_name>命令将本地分支推送到远程仓库。例如，git push origin master将本地的master分支推送到名为origin的远程仓库。