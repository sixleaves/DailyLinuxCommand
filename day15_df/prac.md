

[TOC]



# df

### 命令介绍

>df命令用来查看磁盘的剩余空间



- 命令格式

>`df [选项][文件]`



- 命令功能

>显示指定磁盘文件的可用空间。如果没有文件名被指定，则所有当前被挂载的文件系统的可用空间将被显示。



- 依赖知识

> - inux中df命令的输出清单的第1列是代表文件系统对应的设备文件的路径名，第2列给出分区包含的数据块的数目；第3，4列分别表示已用的和可用的数据块数目。用户也许会感到奇怪的是，第3，4列块数之和不等于第2列中的块数。这是因为缺省的每个分区都留了少量空间供系统管理员使用。即使遇到普通用户空间已满的情况，管理员仍能登录和留有解决问题所需的工作空间。
> - Mounted on列表示文件系统的挂载点。

### 今日练习

- 显示磁盘使用情况

> df

- 以可读方式显示磁盘使用情况

>df -h  以易读方式显示
>
>df -H 以易读方式显示, 采用1000而不是1024进行单位换算
>
>df -lh 显示本地的分区的磁盘空间使用率, 不会现实远程的。



### 主要参数

- `-h`  以易读方式显示


- `-H` 以易读方式显示, 采用1000而不是1024进行单位换算
- `-l` 显示本地的分区的磁盘空间使用率, 不会现实远程的

### OSX使用

- 无

### 使用注意

- 无