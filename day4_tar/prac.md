# tar命令

> tar命令用来创建档案，既可以用tar命令将文件和目录打包成一个文件。最常使用的功能就是压缩和解压

>tar本身并不具备压缩和解压功能，通过调用压缩和解压来实现



## 压缩类型常用参数

### -Z

使用compress压缩，压缩后格式为XXX.tar.Z

### -j

使用bzip2压缩，压缩后格式为XXX.tar.bz2

### -z

使用gzip压缩，压缩后格式为XXX.tar.gz



## 解压常用参数

### -z

使用gzip解压，接的解压文件为XXX.tar.gz

### -j

使用bzip2解压

### -Z

使用uncompress解压



## 动作

tar最常用动作有两个，一个是解压，一个是压缩。

### -x

解压动作

### -c

压缩动作

### -u

更新原压缩包中的文件

### -r

向压缩包文件末尾追加文件



动作后再接上对应要调用的压缩或者解压的格式参数，tar就会去调用



## 必须的参数

### -v

加上这个参数可以看到解压和压缩的过程

### -f

必须要加，而且是接在所有参数最后。表示要解压或者压缩的文档名字





## 完整的命令

tar 动作参数+ 算法类型(Z|z|j)+显示过程(v) + 文件名(f)  具体文件名



## 压缩常见命令

tar -cZvf jpg.tar.Z *.jpg

tar -cjvf jpg.tar.bz2 *.jpg

tar -czvf jpg.tar.gz *.jpg



## 解压常见命令

tar -xZvf jpg.tar.Z

tar -xjvf jpg.tar.bz2

tar -xzvf jpg.tar.gz



##  更新常见命令

tar -uf all.tar logo.gif 

>  这条命令是更新原来tar包all.tar中logo.gif文件，-u是表示更新文件的意思。 



## 追加常见命令

> tar -rf all.tar *.gif 这条命令是将所有.gif的文件增加到all.tar的包里面去。-r是表示增加文件的意思。 





## 其他常见命令

### 查看压缩包

tar -tf xxx.gz

### 解压tar

tar -xvf xxx.tar