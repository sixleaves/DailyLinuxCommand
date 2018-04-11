# file

> 该命令用来识别文件类型，也可用来辨别一些文件的编码格式。
>
> 它是通过查看文件的头部信息来获取文件类型，而不是像Windows通过扩展名来确定文件类型的。



## 主要参数

### -b

> 只显示文件格式和编码



### --mime

> 输出mime类型和mime编码的字符串



## 使用例子

### 查看1.text文件格式

`file 1.text `



### 输出mime类型的字符串

`file --mime 1.text`



## OSX使用

- OSX下使用大写的I代替i来表示mime参数，所以上述命令统一层mime参数。



## 使用注意



## 练习

- 使用file命令查看目录下所有的文件类型
- 使用file命令输出文件的mime类型和mime编码


