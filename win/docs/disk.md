## 磁盘分区
用户一般会按照 "C盘装系统，其他盘装软件、资料"思想分区
```
由于SSD（固态硬盘）的价格相对较高，许多高端电脑采用了SSD+HDD（机械硬盘）的组合方式来平衡性能和存储需求。这种组合方式的主要优势在于：
启动和加载速度快：SSD具有极快的读写速度，尤其是相对于传统的HDD而言。因此，将操作系统和常用程序安装在SSD上可以显著提高系统的启动速度、程序加载速度和响应时间。
存储容量大：虽然SSD的价格较高，但其存储容量相对较小。通过将大量数据存储在HDD上，用户可以充分利用HDD的大容量存储优势，而不必为SSD的高昂价格而犹豫。
数据安全性：由于SSD的写入次数有限，长期大量写入可能会导致其性能下降甚至损坏。而HDD在这方面相对更加稳定，适合长期存储重要数据。
在这种组合中，128GB或256GB的SSD通常被用作系统盘，用于安装操作系统、驱动程序和常用软件。这样可以确保这些程序能够以最快的速度运行，提升用户体验。而HDD则被用作数据盘，用于存放文档、图片、视频、游戏等大量数据文件。
然而，随着技术的进步和成本的降低，SSD的价格已经逐渐下降，使得越来越多的用户能够负担得起更大容量的SSD。现在，许多新购买的电脑已经配备了大容量SSD，甚至有些电脑已经完全放弃了HDD，转而采用全SSD配置。这种配置可以提供更加出色的性能和响应速度，满足现代用户的需求。
```
很多用户需要写文字、做设计，对数据的安全性有一定的要求，这就决定了给硬盘分区依然有巨大的市场需求
Windows 系统内置工具——磁盘管理,即可实现管理磁盘分区


### 磁盘管理工具

#### 打开
`win+x`或者`win+r并输入diskmgmt.msc`

#### 磁盘管理工具操作

##### 新建卷
1. 右键点击C符盘，选择压缩卷，输入压缩空间（单位MB）
2. 点击压缩后，可以看到C符盘`右侧`多出一个未分配的空间。这个空间还不是分区，如果要往里面存储读写数据，就必须将它新建成一个分区
3. 未分配空间上点击右键，选择【新建简单卷】，输入新分区的大小。之后选择驱动器号如D,E等（就是在卷名后面加上（驱动号））,也可以不选择驱动号
4. 格式化，并最好选择NTFS文件系统，可以自定义卷标（就是卷名），单位大小默认
5. 创建完成后，在C盘右侧可以看到新建卷

##### 合并卷
只能从右往左合并分区，相邻分区才能合并
```
因为分区只是系统强加给磁盘的概念，无论划分成多少个分区，它们都在完整的一块磁盘上，并没有物理界限。系统记录一个分区的起点，通过调整分区的终点位置来确定分区的大小。终点位置可以变动，但起点位置一旦确定就不能改变，除非分区被删除，起点位置才会被清除。
```
略
