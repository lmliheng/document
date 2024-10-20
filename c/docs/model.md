## 库开发
需要：`模块代码`加上`对应头文件`

主文件调用如`#include "mathlib.h"`无需声明路径

### 动态库
编译为名为`libmathlib.so`的共享库（动态库）
```bash
gcc -shared -fPIC -o libmathlib.so mathlib.c
```
将库文件的目录添加到LD_LIBRARY_PATH环境变量中，动态链接器会在这个目录下查找库文件
```bash
export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:.\
```

### 静态库

```bash
gcc -c mathlib.c
ar rcs libmathlib.a mathlib.o
gcc -o main main.c libmathlib.a
```
或者
```bash
gcc -c mathlib.c
gcc -o main main.c -L. -lmathlib -static
```






