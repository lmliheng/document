### 常用命令
`git clone <repository_url>`: 克隆远程仓库到本地当前目录

`git init`: 在当前目录中初始化一个新的Git仓库

`git add <file>`: 将文件添加到暂存区。使用git add .将当前目录中的所有更改添加到暂存区。

`git commit -m <commit_message>`: 将暂存区中的更改提交到本地仓库。<commit_message>是对此次提交的简短描述。

`git status`: 显示当前工作区和暂存区的状态。

`git diff`: 显示工作区与暂存区之间的差异。使用git diff --staged查看暂存区与最近一次提交之间的差异。

`git log`: 显示提交历史。使用git log --oneline查看简化的提交历史。

`git remote add origin <repository_url>`: 添加一个远程仓库。<remote_name>通常为origin。

`git push origin <branch_name>`: 将本地分支推送到远程仓库。

例如，git push origin master将本地的master分支推送到名为origin的远程仓库。origin是用来表示远程仓库的别名，而不是实际的仓库名。

可以重命名`git remote rename origin myrepo`
### 检查命令
`git remote -v`命令查看远程仓库的URL

`git branch`查看本地仓库的分支，或者看`李恒@LIHENG2▒▒ MINGW64 ~/Desktop/screen (main)`
### 其他命令
当你克隆一个远程仓库时，Git会自动将远程仓库的URL添加到本地仓库的远程仓库列表中，并将其命名为origin。这个别名可以帮助你在本地仓库中轻松地引用远程仓库。

`git pull<remote_name><branch_name>`: 从远程仓库拉取指定分支的更改并合并到本地分支。例如，git pull origin master从名为origin的远程仓库拉取master分支的更改并合并到本地的master分支。

`git branch`: 列出本地分支。使用git branch -a列出本地和远程分支。

`git checkout<branch_name>`: 切换到指定分支。使用git checkout -b <new_branch_name>创建并切换到新分支。

`git merge<branch_name>`: 将指定分支的更改合并到当前分支。

`git rebase<branch_name>`: 将当前分支的提交重新应用到指定分支的基础上。这可以帮助你整理提交历史并避免合并冲突。

`git stash`: 临时保存当前工作区的更改，以便在稍后恢复。使用git stash apply或git stash pop恢复保存的更改。
### 默认的主分支
在Git中，默认的主分支名称是master

要将本地分支推送到远程仓库的main分支，你可以使用以下命令：
```bash
git push origin main
```
如果你想要将本地的master分支推送到远程仓库的main分支，你可以使用以下命令：
```bash
git push origin master:main
```
这将把本地的master分支推送到远程仓库的main分支,容易出错

切换到另一个分支：
```
git checkout main
```
将branch_name替换为要切换到的分支名称

如果要创建一个新分支并立即切换到它
```
git checkout -b main
```

### 特殊
#### 文件过大
遇到文件大于100MB时使用LFS[Git Large File Storage](https://git-lfs.github.com/).

打开Git Bash并运行以下命令以验证Git LFS是否已成功安装：
```bash
git lfs install
```
如果安装成功应该会看到类似于以下的输出：
```bash
Git LFS initialized.
```