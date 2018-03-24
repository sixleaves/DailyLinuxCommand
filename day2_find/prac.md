#### 1.列出当前目录及子目录下所有文件和文件夹

>  find .

#### 2.在/home目录下查找以.txt结尾的文件名;(忽略大小写：-iname)

> find /home -name "*.txt"

#### 3.当前目录及子目录下查找所有以.txt和.pdf结尾的文件

> find . -name "*.txt" -o -name "*.pdf"

#### 4.匹配文件路径或者文件

> find /usr/ -path "*local*"

#### 5.找出当前目录下不是以.txt结尾的文件

> find . ! -name "*.txt"

#### 6.向下最大深度限制为3的所有文件

> find . -maxdepth 3 -type f

#### 7.搜索大于10KB的文件

> find . -type f -size +10k

#### 8.列出当前目录下所有文件的详细信息

>  find . -type f -exec ls -l {} \;

#### 9. 找出当前目录下所有.txt文件并以“File:文件名”的形式打印出来

> find . -type f -name "*.txt" -exec printf "File: %s\n" {} \;

#### 10.用 grep 命令在所有的普通文件中搜索 hostname 这个词

> find . -type f | xargs grep "hostname"

