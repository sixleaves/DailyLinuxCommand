# ln命令

ln 命令, linux 中用来创建快捷方式的命令.



### 硬链接

>  ln 命令默认创建的是硬连接, 只能和文件相关联.



### 软链接 

>-s参数, 创建的是软链接.软链接可以是文件也可以是目录.



### 区别

> 硬链接的 inode 值不变.文件的inode 值, inode值可以理解为指针.所以可以理解硬链接为指针.而 linux 会为每一个文件维护有一个引用计数值,当文件的引用计数为0才会释放文件.所以删除硬链接并不一定会导致文件真的被删除.除非删除了所有指向该文件的硬链接.
>
> 软链接的 inode 值是不一样的, 其存储的是文件或者目录的绝对地址. 而不是其inode 值.访问软链接的时候,直接使用绝对路径替代它.
