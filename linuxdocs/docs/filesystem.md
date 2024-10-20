### 缓存释放
检查缓存
```bash
[root@linuxbaike ~]# free -m
              total        used        free      shared  buff/cache   available
Mem:           1839         305         510           0        1023        1381
Swap:          1024           0        1024
```
```bash
sync
```
执行sync命令是为了确保文件系统的完整性，手动执行sync命令，将所有未写的系统缓冲区写到磁盘中，包含已修改的 i-node、已延迟的块 I/O 和读写映射文件。

```bash
echo 3 > /proc/sys/vm/drop_caches
```
/proc是一个虚拟文件系统，通过对它的读写操作做为与kernel实体间进行通信的一种手段。
通过调整/proc/sys/vm/drop_caches来释放内存。