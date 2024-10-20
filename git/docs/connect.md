## Git bash
本地注册用户
```bash
git config --global user.name liheng
git config --global user.email liheng2137@qq.com
```
生成SSH密钥文件，SSH文件存放在C:/User/用户/.ssh下，id_rsa为私钥，id_rsa.pub为公钥，konws_hosts文件
```bash
ssh-keygen -t rsa -C liheng2137@qq.com
```
在github.com上setting下添加SSH公钥id_rsa.pub所有key部分
测试SSH连接,按照提示写入yes即可
```bash
ssh -T git@github.com
```
若遇到连接异常
尝试手动添加GitHub的公钥到known_hosts文件中,然后再次测试SSH连接
```bash
ssh-keyscan -t ed25519 github.com >> ~/.ssh/known_hosts
```
最后连接成功
```bash
李恒@LIHENG2  MINGW64 ~
$ ssh -T git@github.com
Hi lmliheng! You've successfully authenticated, but GitHub does not provide shell access.
```