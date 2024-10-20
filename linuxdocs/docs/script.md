## 脚本格式转化
shell 脚本文件是从Windows环境复制到Linux的，因此包含了Windows风格的换行符（CRLF，即回车+换行，表现为 ^M）。Linux期望的是LF（换行）作为行结束符
使用 dos2unix 工具来转换文件的格式，或者直接使用 vim、sed 等编辑器去除Windows的换行符。或者编辑删除换行操作
```Bash
sudo yum install dos2unix # 如果没有安装，先安装
dos2unix hello.sh
```

## 脚本输出格式
文字颜色等需求
[参考1](https://www.cnblogs.com/ananmy/p/15627095.html)
[参考2](https://blog.csdn.net/Dreamhai/article/details/103432525)

```bash
echo -e "\e[96m注意使用source ~/.bashrc激活环境变量\e[0m"
echo -e "\e[32m检查nvm安装情况：nvm --version\e[0m"
echo -e "\e[32m列出node版本：nvm list\e[0m"
```


## 脚本运行参数

1. 参数`-n`，不执行脚本，仅检查语法

2. 参数`-v`，在执行脚本前，先将脚本文件内容输出到屏幕上

3. 参数`-x`，将使用到的脚本内容显示到屏幕上
