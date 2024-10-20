## Make
### Makefile
```Makefile
CC = gcc
CFLAGS = -I./includes -Wall
OBJFILES = objs/bootstrap.o objs/cmd_utils.o objs/install_utils.o objs/shell_utils.o objs/ExamAll.o objs/PrintColor.o objs/FileInfo.o
TARGET = cil

all: $(OBJFILES) $(TARGET)

objs:
	@mkdir -p objs

objs/bootstrap.o: src/bootstrap.c includes/*.h
	$(CC) $(CFLAGS) -c $< -o $@

objs/cmd_utils.o: src/Utils/cmd_utils.c includes/cmd_utils.h
	$(CC) $(CFLAGS) -c $< -o $@

objs/install_utils.o: src/Utils/install_utils.c includes/install_utils.h
	$(CC) $(CFLAGS) -c $< -o $@

objs/shell_utils.o: src/Utils/shell_utils.c includes/shell_utils.h
	$(CC) $(CFLAGS) -c $< -o $@

objs/ExamAll.o: src/LoginShell/ExamAll.c includes/ExamAll.h
	$(CC) $(CFLAGS) -c $< -o $@

objs/PrintColor.o: src/Library/PrintColor.c includes/PrintColor.h
	$(CC) $(CFLAGS) -c $< -o $@

objs/FileInfo.o: src/FileManagement/FileInfo.c includes/FileInfo.h
	$(CC) $(CFLAGS) -c $< -o $@

$(TARGET): $(OBJFILES)
	$(CC) $(OBJFILES) -o $(TARGET)

clean:
	rm -f $(OBJFILES) $(TARGET)
```
构建
```bash
make
```
清理
```bash
make clean
```

### Cmake
参考[文档](https://doc.agsn.site/cps/obj/#cmake)和[官方文档](https://cmake.org/cmake/help/latest/)



## gcc手动编译

```bash
gcc -I../include src/bootstrap.c src/Utils/cmd_utils.c src/Utils/install_utils.c src/Utils/shell_utils.c src/LoginShell/ExamAll.c src/FileManagement/FileSize.c -o cil
```