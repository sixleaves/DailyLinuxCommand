# xargs

> xargs命令是用来将参数列表转换成小块分段传递给其他命令，避免参数列表过长。
>
> 其等效于unix shell中的反引号，但更加灵活易用，并可以正确处理输入中有空格等特殊字符的情况。对于大量输出的命令如find、locate、grep非常有用



## 主要参数

### -I

> replace_str指定替换的字符串



### -0

> 表示使用'\0'来代替空白分隔符。传递给xargs的参数列表默认按空白符分隔。



### -r

> 表示如果没有参数传入就不执行，默认是执行的。



### -n

> 指定每行参数的数量n。



### 使用例子

#### 使用-n参数将单行转换为多行输出

有如下内容的example.txt文件

> a b c 
> d e
> f

执行`cat example.txt | xargs -n 2`

表示将cat出来的内容按照空格分割成列表传逐个递给xargs命令。并且一两个为一行进行输出

> a b
> c d
> e f



### 使用-r参数保证xargs不报错

>mkdir empty_dir
>
>cd empty_dir
>
>ls | xargs rm

-r参数只在linux系统下有效。osx下无效



### -0参数配合-print0使用

这个参数主要是用来将xargs命令的分割符更改为NUL既'\0'.需要和-print0配合使用。

创建一个`a \ b` 的文件名, 使用ls命令列出传递给rm删除

`touch a \ b`

`ls a\ b | xargs rm`

>rm: a: No such file or directory
>rm: b: No such file or directory

正确的是执行

`ls a\ b | xargs -I{} rm {}`

或者是

`find . -name "a b" -type f -print0 | xargs -0 rm`





## OSX使用

- OSX中的xargs没有-r参数



## 使用注意

- -0 需要和-print0配合使用。print0让输出以null分隔
- -n 指定每一行xargs要传递的参数
- -r 不通用



## 练习

- 使用find命令查找指定目录下的文件目录，并使用xargs将列表传递给rm删除。







