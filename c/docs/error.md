## 系统找不到动态库libmathlib.so
### 问题
```bash
[root@RainYun-x6pWTQo0 demo]# gcc -shared -fPIC -o libmathlib.so mathlib.c
[root@RainYun-x6pWTQo0 demo]# ls
libmathlib.so  main.c  mathlib.c  mathlib.h
[root@RainYun-x6pWTQo0 demo]# gcc -o main main.c -L. -lmathlib
[root@RainYun-x6pWTQo0 demo]# ls
libmathlib.so  main  main.c  mathlib.c  mathlib.h
[root@RainYun-x6pWTQo0 demo]# ./main
./main: error while loading shared libraries: libmathlib.so: cannot open shared object file: No such file or directory
[root@RainYun-x6pWTQo0 demo]# 
```
### 解决

1. 将库文件的目录添加到LD_LIBRARY_PATH环境变量中，动态链接器会在这个目录下查找库文件，执行`export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:.`

```bash
[root@RainYun-x6pWTQo0 demo]# export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:.
[root@RainYun-x6pWTQo0 demo]# ./main
Add: 15.00
Subtract: 5.00
Multiply: 50.00
Divide: 2.00
[root@RainYun-x6pWTQo0 demo]# 

```
2. 另一种方法是将库文件复制到系统的默认库搜索路径之一如/usr/local/lib-[参考](https://www.cnblogs.com/bigfi/p/9487427.html)
```bash
sudo cp libmathlib.so /usr/local/lib/
```
更新动态链接器的缓存：
```bash
sudo ldconfig
```
