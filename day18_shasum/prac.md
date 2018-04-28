

[TOC]

# shasum

### 命令介绍

>shasum和md5命令一样, 都是摘要命令，不是加密命令。所谓的摘要命令就类似于是给一个文件计算一个唯一标识，就相当于人类的指纹。shasum命令按哈希大小分为160位、224位、256位、384位、512位、512224位、512256位。



- 命令格式

>`shasum [option] [FILE]`



- 命令功能

>用来计算文件指纹，用于鉴定文件的完整性，或用于唯一识别身份。



- 依赖知识

> - 哈希算法

### 今日练习

- **生成一个文件 best.txt 的 shasum 160位值(又称为sha-1)**.

>
>
>结果: 6cccfaa42458d2a27d69216db29a36f4ab1b979e  best.txt

**注意这边计算结果只有40位那是因为换算成了16进制，每4位对应一位16进制**



- **检查文件 worst.txt 是否被修改过**.

>1.生成worst.txt的shasum值，存放位worst.txt.sha1
>
>> 
>>
>> 结果(worst.txt.sha1的输出): 
>>
>> `1ab11e078cc93b23259d91ead4e1d89c0564eddb  worst.txt  `
>
>2.不对worst.txt操作, 计算worst.txt的sha1值并和worst.txt.sha1比较
>
>>
>>
>>结果(执行完命令的输出):
>>
>>```bash
>>shasum: worst.txt: no properly formatted SHA1 checksum lines found
>>
>>worst.txt: OK
>>
>>```
>
>
>
>3.对worst.txt进行操作, 随便添加字符。再次重复
>
>> 
>>
>> 结果:
>>
>> ```bash
>> shasum: worst.txt: no properly formatted SHA1 checksum lines found
>>
>> worst.txt: FAILED
>>
>> shasum: WARNING: 1 computed checksum did NOT match
>>
>> ```



### 主要参数

- `-a`  

  > 用来指定选择那种sha算法，默认是sha1，但是为了可读性，一般我会写名sha -a 1
  >
  > 改值还可以指定为以下集中
  >
  > sha -a 256、sha -a 512、sha -a 51224、sha -a 512256

- `-b`

  > 表示以二进制的方式读取

- `-c`

  > 从指定文件中读取 sha校验和，并进行校验




### OSX使用

- shasum为osx命令，其可以通过-a参数指定位sha的那种算法。linux下有sha1sum、sha256sum、sha512sum。对应的就是shasum -a 1、shasum -a 256、shasum -a 512

  ​

### 使用注意

- 注意osx下用-a参数指明使用哪个sha算法



### 答案

- **生成一个文件 best.txt 的 shasum 160位值(又称为sha-1)**

  > shasum -a 512 best.txt

- **检查文件 worst.txt 是否被修改过**.

  >- 生成worst.txt的shasum值，存放位worst.txt.sha1
  >
  >> shasum -a 1 worst.txt > worst.txt.sha1
  >
  >> cat > worst.txt.sha1
  >
  >- 不对worst.txt操作, 计算worst.txt的sha1值并和worst.txt.sha1比较
  >
  >> shasum -a 1 worst.txt -c worst.txt.sha1
  >
  >- 对worst.txt进行操作, 随便添加字符。再次重复
  >
  >> echo "test" >> worst.txt
  >
  >> shasum -a 1 worst.txt -c worst.txt.sha1

  ​