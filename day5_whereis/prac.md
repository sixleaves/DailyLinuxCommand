# whereis

> whereis命令是一个搜索命令
>
> 一个只能搜索二进制文件和源代码文件的命令
>
> whereis搜索的原理和find命令不同，whereis是基于数据库。



## 主要参数

### -b

> 搜索二进制文件路径



### -s

> 搜索源代码文件路径



### -m

> 搜索对应的说明文件路径



## 使用例子

`whereis svn`

> 该命令默认查找svn二进制文件的路径




## OSX使用

- osx下whereis只能定位二进制文件




## 使用注意

- whereis是依赖于数据接口搜索，find是直接搜索磁盘。linux系统会将系统内所有文件都记录在一个数据库文件中。

- whereis只能查找二进制文件和源代码文件，find不限。

- whereis在OSX下只能用于查找二进制文件，并且只去标准二进制目录下找/usr/bin目录下

  ​



## 练习

- 使用whereis查找whereis这个命令的路径。


