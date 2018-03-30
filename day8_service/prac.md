# service

> service命令是linux下用来管理服务的命令。其原理是到/etc/init.d/目录下寻找服务名对应的脚本文件。然后执行该脚本文件，并传递相关动作(stop, start等)



## 关键参数

### stop

> 停止服务

### start

>开启服务



## 使用例子

### 启动mysql服务

`service mysql start`



## OSX 使用

> osx下没有servcice命令，使用launchctl命令来管理服务。可以使用lunchy这个命令来替代service

### 安装lunchy

`gem install lunchy`

### 启动mysql服务

`lunchy start mysql`

>可以看到lunchy和service比较类似，可以对齐进行进行二次封装，统一成service形式。
>
>在/usr/local/bin下新建一个service文件，输入如下内容
>
>```bash
>#!/bin/bash
>
>/usr/local/bin/lunchy $2 $1
>```
>
>改为为可执行文件, 并开放最大权限 `chmod /usr/local/bin/service`
>
>重启终端，可以愉快使用linux的service命令了!

## 练习

- 尝试封装service命令，使其能够在osx上使用。
- 使用linux系统启动mysql服务





