# Linux 基础操作

## Linux 体系结构

- 体系结构主要分为用户态（用户上层活动）和 内核态
- 内核：本质是一段管理计算机硬件设备的程序
- 内核为上层用户态提供访问资源的接口
- 系统调用：内核的访问接口，是一种不能再简化的操作
- man 2 syscalls 可以查看到所有的系统调用
- 共用函数库：系统调用的组合，对系统调用的封装
- Shell：命令解释器，可编程（可以运行符合shell语法的文本文件，称为shell 脚本）

- cat /etc/shells 查看本机支持的 shell

- chsh -s + shell路径 用于切换shell



## 文件权限

7：表示rwx，拥有读、写和执行的权限 

6：表示rw-，拥有读和写的权限 

5：表示rx，拥有读取和执行的权限 

4：表示r--，拥有只读权限 

3：表示-wx，拥有写入和执行的权限 

2：表示-w-，拥有只写权限 

1：表示 - x，仅拥有执行权限 

0：表示---，无权限

```shell
chmod 777 participants
```

说明：第1个7设置用户的权限，第2个7设置组的权限，第3个7设置其他所有者的权限。

participants 文件名

r=4，w=2，x=1，-=0



## 快捷操作

- ctrl-c：发送 SIGINT 信号给前台进程组中的所有进程。常用于终止正在运行的程序；
- ctrl-z：发送 SIGTSTP信号给前台进程组中的所有进程，常用于挂起一个进程；
- ctrl-d：不是发送信号，而是表示一个特殊的二进制值，表示 EOF，作用相当于在终端中输入exit后回车；
- ctrl-\：发送 SIGQUIT 信号给前台进程组中的所有进程，终止前台进程并生成 core 文件；
- ctrl-s：中断控制台输出；
- ctrl-q：恢复控制台输出；
- ctrl-l：清屏



## 常见命令

### find

```shell
# 从当前目录开始往下查找
find -name "target.java"
# 全局搜索
find / -name "target.java"
# 查找用户目录下以 target 打头的文件
find ~ -name "target*"
# 查找用户目录下以 target 打头的文件（忽略大小写）
find ~ -iname "target*"
```

### 管道操作符“|”

- 可将指令连接起来，前一个指令的输出作为后一个指令的输入

- 会把前一个指令的正确输出作为后一个指令的输入，错误输出无法处理

### grep

使用正则表达式搜索文本 , 并把匹配的行打印出来

- **查找文件file.log中“passport”字段：**

> grep “passport” file.log

- **查找文件file.log中“passport”字段，并且统计出出现次数：**

> grep “passport” file.log |wc –l
>
> grep “passport” file.log –c



### awk

- 语法：awk [options] 'cmd' file

- 一次读取一行文本，按输入分隔符进行切片，切成多个组成部分

- 将切片直接保存在内建的变量中，$1,$2,...($0表示行的全部)

- 支持对单个切片的判断，支持循环判断，默认分隔符为空格

```shell
awk '{print $1,$4}' netstat.txt
# 打印出第一个空为tcp 第二个空为1的行
awk '$1=="tcp" && $2==1{print $0}' netstat.txt
# 按逗号分隔行内容
awk -F ","'{print $2}' test.txt
```





### top和ps命令：探测进程

**ps命令**,默认只会显示运行在当前控制台下的属于当前用户的进程。

- ps –A和ps –e可以显示所有进程
- ps -ef 显示完整格式的所有进程
- 指定进程名，ps -ef | grep“java”找出进程名中包括java的所有进程

**top命令**

![1](img\linux\1.png)

- 第一行显示了当前时间、系统的运行时间、登录的用户数和系统的平均负载（平均负载有3个值：最近1min 5min 15min）。
- 第二行显示了进程的概要信息，有多少进程处于运行、休眠、停止或者僵化状态。
- 第三行是CPU的概要信息。
- 第四行是系统内存的状态。

**ps和top命令的区别：**

- ps看到的是命令执行瞬间的进程信息，而top可以持续的监视。
- ps只是查看进程，而top还可以监视系统性能，如平均负载，cpu和内存的消耗。
- top可以操作进程,如改变优先级(命令r)和关闭进程(命令k)。
- ps主要是查看进程的，关注点在于查看需要查看的进程。
- top主要看cpu，内存使用情况，及占用资源最多的进程由高到低排序，关注点在于资源占用情况。

### sed命令：

sed 命令是利用脚本来处理文本文件。sed 可依照脚本的指令来处理、编辑文本文件。sed 主要用来自动编辑一个或多个文件、简化对文件的反复操作、编写转换程序等。

```shell
# 将文件的第二行和第三行裁剪出来
sed –n ‘2,3p’ test.txt

# 把 Str 打头的行并将 Str 替换成 String，只输出不修改
sed 's/^Str/String/' replace.java
# -i 修改文件内容
sed -i 's/^Str/String/' replace.java
# 把 . 结尾的行的 . 替换成 ;
sed -i 's/\.$/\;/' replace.java
# 把 Jack 替换成 me，只替换第一个
sed -i 's/Jack/me/' replace.java
# 把 Jack 替换成 me，全文替换
sed -i 's/Jack/me/g' replace.java
# 把空行删除
sed -i '/^ *$/d' replace.java
# 把包含 Integer 的行删除
sed -i '/Integer/d' replace.java
```



### sort命令：

sort命令可以实现对文件进行排序。

- 正序排序：**sort -n test.txt**
- 反序排序：**sort –nr test.txt**

根据每行字符串字典序



### tail和head命令：

- **tail –n 2 file.log** 可以查看文件的最后2行。
- **tail –f file.log**可以实时查看文件的后边追加的部分。
- **head –n 2 file.log**可以查看文件的开始2行。



### Unix中的inode

-  inode能描述文件占用的块数
- inode描述了文件大小和指向数据块的指针
- 通过inode实现文件的逻辑结构和物理结构的转换