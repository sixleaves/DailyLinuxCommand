[TOC]



# crontab

> crontab是linux下用来定时执行任务的命令。其对应的服务是cron服务，该服务是用来控制linux系统，linux下默认是启动的。crond进程每分钟会自动检测是否有要自信的任务。

## 主要参数

### -e

> `crontab -e`表示编辑crontab的配置文件。可以在配置文件里新增定时任务

### -l

> `crontab -l`列出crontab配置文件里的计划任务



## 例子

### 添加计划任务

- 执行`crontab -e`打开配置文件
- 新增一行计划任务。格式为`分 时 日 月 星期几 任务`

> 默认格式为* * * * * 任务

### 增加每天12点报时

`0 12 * * * say 12点了`



### 每分钟说hello

`* * * * * say hello`



### 每天0点执行指定脚本

`0 0 * * * sh backup.sh`



### 每个星期一的上午8点到11点的第3和第15分钟执行

`3,15 8-11 * * 1 command`



### 每一小时重启smb

`* */1 * * * /etc/init.d/smb restart`



### 晚上11点到早上7点之间，每隔一小时重启smb

`* 23-7/1 * * * /etc/init.d/smb restart`



## OSX

> osx下crontab默认没有启用，一般使用launchctl命令来替代

### osx开启crontab

- 启动cron服务，`launchctl load -w /System/Library/LaunchDaemons/com.vix.cron.plist`
- 创建crontab文件, `touch /etc/crontab`

经过以上两步，即可在osx中正常的使用cron服务



## 使用注意

### 环境变量

> 手动执行任务没有问题。添加到crontab中却不能执行，可以试下导入环境变量。
>
> `0 * * * * . /etc/profile;/bin/sh backup.sh`
>
> 先导入profile里的环境变量，再执行backup脚本

### 清理系统用户邮件日志

>每次执行任务的输出，cron都会通过电子邮件发给当前系统用户，因此会几类大量日志信息。可以使用`/dev/null 2>&1`将标准输出和标准错误输出都定向到/dev/null。(该语句表示先将标准输出重定向到/dev/null，然后将标准错误重定向到标准输出，由于标准输出已经重定向到了/dev/null，因此标准错误也会重定向到/dev/null，这样日志输出问题就解决了)
>
>`0 */3 * * * /usr/local/apache2/apachectl restart >/dev/null 2>&1`



## 练习

将prac的脚本添加到crontab中定时执行，1分钟执行一次。



