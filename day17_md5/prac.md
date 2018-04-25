# md5sum
- 命令格式: `md5 (选项) (参数)`

- 命令功能: md5sum 用来**验证网络文件传输的完整性，防止文件被人篡改**。

- 依赖知识

  > MD5 全称是报文摘要算法（Message-Digest Algorithm 5），此算法对任意长度的信息逐位进行计算，产生一个二进制长度为 128 位（十六进制长度就是 32 位）的“指纹”（或称“报文摘要”），不同的文件产生相同的报文摘要的可能性是非常非常之小的。

## 今日练习
- **生成一个文件 best.txt 的 md5 值**.

  `[lisanaaa@localhost prac]$ md5sum best.txt`
  `880cf2f27abd7f5d306b617f576084e5  best.txt`

- **检查文件 worst.txt 是否被修改过**.


1. 首先生成 md5 文件

`[lisanaaa@localhost prac]$ md5sum worst.txt > worst.txt.md5`

2. 不对 worst.txt 文件作操作，校验文件是否变化

`[lisanaaa@localhost prac]$ md5sum worst.txt -c worst.txt.md5`

`md5sum: worst.txt: no properly formatted MD5 checksum lines found`
`worst.txt: OK`

3. 对 worst.txt 文件作操作(删掉文件最后的句号)，校验文件是否变化

`[lisanaaa@localhost prac]$ md5sum worst.txt -c worst.txt.md5`

`md5sum: worst.txt: no properly formatted MD5 checksum lines found`
`worst.txt: FAILED `

`md5sum: WARNING: 1 of 1 computed checksum did NOT match`

4. 如果不想有任何输出，则`md5sum testfile --status -c testfile.md5`，这时候通过返回值来检测结果。

`[lisanaaa@localhost prac]$ md5sum worst.txt --status -c worst.txt.md5`
`md5sum: worst.txt: no properly formatted MD5 checksum lines found`

5. 检测的时候如果检测文件非法则输出信息的选项:

`[lisanaaa@localhost prac]$ md5sum worst.txt -w -c worst.txt.md5`
`md5sum: worst.txt: 1: improperly formatted MD5 checksum line`
`md5sum: worst.txt: no properly formatted MD5 checksum lines found`
`worst.txt: FAILED`
`md5sum: WARNING: 1 of 1 computed checksum did NOT match`



## 主要选项

### -b

二进制模式读取文件。



### -t

把输入的文件当作文本文件。



### -c

从指定文件中读取 MD5 校验和，并进行校验。



### --status

校验正确时不输出任何信息。



### -w

校验不正确时给出相应的警告⚠️信息。



## 主要参数

### 文件

指定保存着 **文件名和校验和** 的文本文件。



## OSX 使用

利用终端命令  把字符串转换成  md5



## OSX 使用例子

### 把字符串转换成  md5

`-> md5 -s hello`

`-> MD5 ("hello") = 5d41402abc4b2a76b9719d911017c592`

> 将字符串 ‘hello’ 转为 md5加密🔐码



