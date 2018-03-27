# whereis

> whereis命令是一个搜索命令
>
> 一个只能搜索二进制文件和源代码文件的命令



## 参数

### -b

> 搜索二进制文件路径



### -s

> 搜索源代码文件路径



### -m

> 搜索对应的说明文件路径



> whereis svn
>
> 该命令默认查找svn二进制文件的路径



## 原理

whereis搜索的原理和find命令不同，whereis是基于数据库。



## 区别

- whereis是依赖于数据接口搜索，find是直接搜索磁盘。linux系统会将系统内所有文件都记录在一个数据库文件中。
- whereis只能查找二进制文件和源代码文件，find不限。



## OSX和linux

- osx下whereis只能定位二进制文件
- linux的可以使用-b指定搜索二进制文件，-m搜索对应的说明文档，-s搜索对应的源文件


