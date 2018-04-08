# sed

```bash
 sed [-Ealn] command [file ...]
 sed [-Ealn] [-e command] [-f command_file] [-i extension] [file ...]
```



> sed有称为stream editor，流编辑器，是一种文本处理工具。sed核心就是玩正则表达式。
>
> sed编辑器逐行处理文件（或输入），并将结果发送到屏幕。具体过程如下：首先sed把当前正在处理的行保存在一个临时缓存区中（也称为模式空间），然后处理临时缓冲区中的行，完成后把该行发送到屏幕上。sed每处理完一行就将其从临时缓冲区删除，然后将下一行读入，进行处理和显示。处理完输入文件的最后一行后，sed便结束运行。sed把每一行都存在临时缓冲区中，对这个副本进行编辑，所以不会修改原文件。

**/是sed命令参数的界定符, 就是用来分割命令参数和文本.其实就是分隔命令和命令所传递参数的作用**



### 正则基础

- ^ 表示一行开头.eg: `/^#/`表示以#开头的匹配
- $ 表示一行结尾.eg: `/}$/`表示以}结尾的匹配
- `\<`表示词首.    eg: `\<abc`表示以abc为首的词
- `\>`表示词尾.    eg: `abc\>`表示以abc结尾的词
- `.`表示任何单个字符
- `*`表示某个字符出现0次或多次
- `[]`字符集合。`[abc]`表示匹配a或b或c.`[a-zA-Z]`表示匹配所有26个字符.`[^a]`表示非a的字符



### 文本定位

> 用于决定哪些行可以被编辑。地址既行号，其形式可以是数字、正则或者二者结合。
>
> 默认处理全部文件的所有行。
>
> 地址是数字表示行号，用$表示最后一行的行号。
>
> 地址需要和子命令参数配合使用

`sed -n '3p' datafile` 打印前三行。p子命令表示打印

`sed -n '100,200p'datafile` 打印100到200行



- /pattern/    查询包含模式的行,如/disk/或/[a-z]/


- /pattern/pattern/   查询包含两个模式的行,如/disk/disks/


- /pattern/,x  在给定行号上查询包含模式的行,如/disk/,3


- x,/pattern/  通过行号和模式查询匹配行,如 3,/disk/



## 主要参数

### sed选项参数

#### -n

> 取消默认的标准输出



#### -f

> 指定脚本的文件名



### -e

> 用于串行的执行sed的子命令





### 常用子命令



#### a\

> 新增命令。a 的后面可以接字串，而这些字串会在新的一行出现(目前的下一行)

`sed '1a drink tea' ab  #第一行后增加字符串"drink tea"`



`sed -i '$a bye' ab         #在文件ab中最后一行直接输入"bye"`

这个-i不是子命令, 而是sed命令参数，表示直接修改文件，不输出



#### d

> 删除子命令，用于删除行。

` sed '1d' ab              #删除第一行 `

`sed '$d' ab              #删除最后一行`

`sed '1,2d' ab           #删除第一行到第二行`

#### s

> 改命令。用一个字符串替换另一个字符串
>
> `sed 's/要替换的字符串/新字符串/g' datafile`
>
> g表示全局替换

`sed 's/[ ][ ]*/ /g' file_name`



#### p

> 打印命令，用于打印指定行数，和-n选项参数配合使用。可以当成grep式的命令



### 其他子命令

#### i\

> 插入命令.和a唯一的区别是i\命令插入在前



#### c\

> 和s命令一样，是替换命令

`sed '1c Hi' ab                #第一行代替为Hi`



## 使用例子

参照见子命令说明



## OSX使用

无



## 使用注意

- 注意`a\` 、`i\`、`c\`等子命令的使用，在mac下使用这三个子命令需要时候，添加的文本需要换行，子命令一行，文本一行。

```bash
sed '$a\
helloworld \
' file.txt
```





## 进阶使用(新增)

> 这一模块主要总结复杂命令的原理和复杂的组合使用

### pattern space 和Hold space

> pattern space也陈为pattern buffer，简称PS。当sed按行读取文件的时候, 当前读取的行被插入到pattern buffer中, pattern buffer就如同一个内存，用来暂存信息。当你调用p子命令打印的时候或者sed默认的打印都是打印pattern space的内容。



> hold buffer更像是磁盘，用来长期的存储。所以你可以先将某些数据存储到hold buffer，然后去处理其他的行，并在这一过程中复用hold buffer中将之前存储的数据。
>
> 通常我们不会直接操作hold buffer，而是将hold buffer数据追加到pattern buffer。



- g:  ps = hs
- G: ps += hs
- h: hs = ps
- H: hs += ps
- x : swap(ps, hs)

**ps表示pattern space，hs表示hold space. g命令把ps当成被赋值的变量（记住gps）**

**sed子命令可以通过分号分隔，然后串行执行**

eg:`sed -n '1!G;h;$p'`

>这个sed命令包含三个子命令, 1!G, h, $p 
>
>1!G表示第一行，1!表示除了第一行 p表示打印最后一行
>
>- 1.第一行被读取并且被自动插入到PS
>- 2.在第一行, 第一个命令不会执行，h子命令拷贝第一行到HS
>- 3.读取到第二行直接将hs中的覆盖掉
>- 4.在第二行，我们先执行G命令，既ps += hs，将hs中的数据附加到ps中，并且用换行符分隔。ps中这时候将包含第二行、新的一行(\n)、第一行
>- 5.然后h子命令将，ps中的内容再赋给hs，现在hs也有了一份一样的拷贝
>- 6.我们接着处理第三行，返回第三点继续

最终最后一行会被p子命令打印出来，并且hs中已经附加了ps，ps会被用p命令打印。这个功能就是最终将一个文件反序打印。



## 练习

- 将HTML.txt的标签都删除。保留文本节点。(练习s子命令)

- 打印hao_pets.txt 1到3行。(练习p子命令)

- 打印hao_pets.txt包含name的行。(练习p子命令和正则)

- 删除hao_pets.txt 的最后一行。(练习d子命令)

- 新增hello world到hao_pets.txt的最后一行。(练习a子命令)

- 将hao_pets.txt逆序打印(练习G、h、p的综合使用)

- 练习正则表达式(可以参考以下提供的连接，练习正则)

  ​

## 参考

https://coolshell.cn/articles/9104.html

http://man.linuxde.net/sed

http://www.cnblogs.com/emanlee/p/3307642.html

https://blog.csdn.net/sun_wangdong/article/details/71078083

https://qianngchn.github.io/wiki/4.html#a%E5%91%BD%E4%BB%A4

https://stackoverflow.com/questions/12833714/the-concept-of-hold-space-and-pattern-space-in-sed/12834372