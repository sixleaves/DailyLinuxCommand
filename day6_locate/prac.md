# locate

>locate命令也是linux下的查找命令。目前练习过了两种查找命令，一种是find、一种是whereis。
>
>locate和whereis是属于一种类别的命令，其都是依赖于linux系统自动维护的数据库。
>
>locate命令依赖于updatedb命令进行数据库更新，osx下改命令对应的是/usr/libexec/locate.updatedb



## 命令格式

locate `[参数]`  `[样式]`



## 常用参数

### -i 

> 忽略大小写



### -r

-r `正则表达式` 基于正则表达式搜索定位文件



查找包含/var/lib/dpkg/info的文件

`locate -r /var/lib/dpkg/info`





## OSX

> osx的locate的数据库更新程序位于/usr/libexec/locate.updatedb
>
> 使用locate前需要先执行以下语句
>
> sudo launchctl load -w /System/Library/LaunchDaemons/com.apple.locate.plist
>
> sudo /usr/libexec/locate.updatedb



>为方便使用updatedb，同时和linux统一，可以使用ln命令创建一个软连接到/usr/local/bin下
>
>ln -s /usr/libexec/locate.updatedb /usr/local/bin/updatedb



>osx下的updatedb的配置文件直接写在了这个updatedb可执行脚本中.
>
>在SEARCHPATHS中加入$HOME。使用`sudo vim /usr/libexec/locate.updatedb `打开编辑
>
>同时可以看到，其他事改命令是基于find命令封装

```bash
: ${mklocatedb:=locate.mklocatedb}      # make locate database program

: ${FCODES:=/var/db/locate.database}    # the database

: ${SEARCHPATHS:="/ $HOME"}                   # directories to be put in the database

: ${PRUNEPATHS:="/private/tmp /private/var/folders /private/var/tmp */Backups.backupdb"} # unwanted directories

: ${FILESYSTEMS:="hfs ufs apfs"}        # allowed filesystems

: ${find:=find}
```



> osx下locate命令不用使用-r参数来指定正则表达式



## 练习

使用locate命令，输出prac文件夹下locatefile.txt的文件路径。



## 总结

- locate命令是find命令的封装，同时又做了优化，通过数据库文件直接查找文件，效率高

- 需要用updatedb命令更新数据库，osx下位置位于/usr/libexec目录下。可以用ln做个软连接

  > ln -s /usr/libexec/locate.updatedb /usr/local/bin/updatedb

- 可以自己配置updatedb命令要添加索引的目录。打开updatedb文件查找SEARCHPATHS配置即可。