# shell的学习

```bash
单引号，不能识别特殊符号
双引号，能识别特殊符号
```

![image-20230308213728312](C:\Users\cao'yang'lin\AppData\Roaming\Typora\typora-user-images\image-20230308213728312.png)

# Shell的作用域

![image-20230308214039639](C:\Users\cao'yang'lin\AppData\Roaming\Typora\typora-user-images\image-20230308214039639.png)

1、父shell的变量，子shell都可以查看到，但是子shell的变量，父shell不能查看到子shell的变量

2、调用source或者.符号，在当前shell环境加载脚本，因此保留变量

3、用bash命令开启子shell来执行脚本，并不会保留变量

```bash
linux命令
在linux中反引号，中的命令执行结果会被保留下来
[root@localhost bianyi]# name=`ls`
[root@localhost bianyi]# echo $name
ab ab.o a.c a.i a.o a.s b.c b.o Lib.c Lib.h Lib.so main main.cpp main.i program1 program1.c program2 program2.c t1.sh test test01 test01.cpp
#反引号就在1的左边，英文输入法

```

![image-20230308215822176](C:\Users\cao'yang'lin\AppData\Roaming\Typora\typora-user-images\image-20230308215822176.png)

# pstree进程树

![image-20230308214523309](C:\Users\cao'yang'lin\AppData\Roaming\Typora\typora-user-images\image-20230308214523309.png)

# 环境变量的设置

1】用户个人的配置文件 ~/.bash_profile、~/.bashrc 远程登录用户特有文件

2】全局配置文件 /etc/profile、/etc/bashrc，且系统建议最好创建在 /etc/profile.d/，而非直接修改主文件，修改全局配置文件，影响所有登录系统的用户，（优先用户的配置文件）

![image-20230308235651577](C:\Users\cao'yang'lin\AppData\Roaming\Typora\typora-user-images\image-20230308235651577.png)

复制的会话，是兄弟关系而非父子

## 检查系统环境变量的命令

set，输出所有变量，包括全局变量，局部变量

env，只显示全局变量

declare，输出所有的变量，如同set

export，显示和设置环境变量值

### 撤销环境变量

unset变量名，删除变量或函数

### 设置只读变量

readonly,只有shell结束，只读变量失效

```bash
[yuchao@localhost ~]$ readonly password12="123"
[yuchao@localhost ~]$ echo $password12
123
[yuchao@localhost ~]$ password12=89
-bash: password12: 只读变量
```

### 系统保留环境变量关键字

bash内嵌了诸多环境变量，用于定义bash的工作环境

```bash
export |awk -F '[:=]' '{print $3}'
```

### bash多命令执行

```bash
[yuchao@localhost home]$ ls /home/;cd /tmp;cd /home;
ceshi  dockerfile  docker-test-volume  it  mysql  yuchao
[yuchao@localhost home]$ 
```

### 特殊变量学习

### 参数传递

```bash
# 1.$0的展示执行文件名，$1,第一个传递的参数,$2,第二个传递的参数，依次
[yuchao@localhost bin]$ cat t1.sh
# !/bin/bash
echo '特殊变量$1,$0.$2'    

echo "特殊变量$1,$0,$2"                    
[yuchao@localhost bin]$ bash t1.sh caoyang lin jk
特殊变量$1,$0.$2
特殊变量caoyang,t1.sh,lin
[yuchao@localhost bin]$ 

# 2.$* 获取shell脚本的所有参数，不加引号等于"$*"作用是 接收所有参数为单个字符串，“$1 $2”
# 3.$@ 不加引号，效果同上         加双引号时，$*是会把整体看作一份数据，加双引号时$@看作一份一份独立的数据
[yuchao@localhost bin]$ bash t1.sh caoyang lin jk
特殊变量$1,$0.$2
特殊变量caoyang,t1.sh,lin
特殊变量$*
caoyang lin jk
特殊变量$@
caoyang lin jk

$* ——所有参数列表。如"$*"用「"」括起来的情况、以"$1 $2 … $n"的形式输出所有参数。 
$@ ——所有参数列表。如"$@"用「"」括起来的情况、以"$1" "$2" … "$n" 的形式输出所有参数。 
$# ——添加到Shell的参数个数 
$0 ——Shell本身的文件名 
$1～$n ——添加到Shell的各参数值。$1是第1参数、$2是第2参数…
```

### shell for循环开发的知识

实践面试题的区别

```bash
[yuchao@localhost bin]$ cat qubie.sh
#!/bin/bash
echo "print echo param from \"\$*\""
for var in "$*"
do
   echo "$var"
done 
echo "print echo param from \"\$@\""
for var in "$@"
do
  echo "$var"
done
[yuchao@localhost bin]$ bash qubie.sh 1 2 3 4 5 6 7 8 9
print echo param from "$*"
1 2 3 4 5 6 7 8 9    #只循环一次  $*做为一个整体
print echo param from "$@"
1
2
3                    #循环很多次  $@做为几个独立的数据
4
5
6
7
8
9
```

### 特殊状态变量

```bash
$$ ——Shell本身的PID（ProcessID） 
$! ——Shell最后运行的后台Process的PID 
$? ——最后运行的命令的结束代码（返回值） #脚本返回值
$- ——使用Set命令设定的Flag一览 


```

### 脚本控制放回值的玩法

```bash
$? ——最后运行的命令的结束代码（返回值） #脚本返回值
[yuchao@localhost bin]$ bash teshu.sh 78 yuchao ui
must be two args
[yuchao@localhost bin]$ echo $?
119
[yuchao@localhost bin]$ bash teshu.sh 78 yuchao 
没毛病就是俩个参数
[yuchao@localhost bin]$ echo $?
0
nohup ping baidu.com & 1> /dev/null
```

> 获取上一次后台执行的 程序，pid，$!获取

# shell子串

### bash一些基本的内置命令

```shell
echo
eval
exec
export
read
shift
```

### echo命令

```shell
-n 不换行输出
-e 解析字符串中的特殊符号

\n 换行符
\r 回车
\t 制表符   四个空格
\b 退格

root@hecs-218409:~/shellLearn# echo 你好呀;echo 你还挺可爱;
你好呀
你还挺可爱
root@hecs-218409:~/shellLearn# echo -n 你好呀;echo 你还挺可爱;
你好呀你还挺可爱
root@hecs-218409:~/shellLearn# echo -n 你好呀;echo -n 你还挺可爱;
你好呀你还挺可爱root@hecs-218409:~/shellLearn# 
root@hecs-218409:~/shellLearn# echo "我看你挺\n好的"
我看你挺\n好的
root@hecs-218409:~/shellLearn# echo -e "我看你挺\n好的"
我看你挺
好的

#printf

```

### eval

执行多个命令

```shell
root@hecs-218409:~/shellLearn# eval ls;cd ..
t1.sh

```

### exec

不创建子进程，执行后续命令，且执行完毕后，自动exit

```shell
root@hecs-218409:~/shellLearn# exec date
Thu Mar  9 01:07:10 PM CST 2023

Connection closed.

Disconnected from remote host(云test01) at 13:07:08.

Type `help' to learn how to use Xshell prompt.
[C:\~]$ 

```

### shell子串的花式用法

```shell
${变量}                                    返回变量值
${#变量}                                   返回变量长度，字符长度--------
${变量:start}                              返回变量offset数值之后的字符
${变量:start:length}                       提取offset之后的length限制的字符
${变量#word}                               从变量开头删除最短匹配的word字符
${变量##word}                               从变量开头，删除最长匹配的word
${变量%word}                               从变量结尾删除最短的word
${变量%%word}                              从变量结尾开始删除最长匹配的word
${变量/pattern/string}                     用string代替第一个匹配的pattern
${变量//pattern/string}                    用string代替所有的pattern

指定字符内容截取
a*c 匹配开头为a,中间任意的字符，结尾为c的字符串
a*C 匹配开头为a,中间任意的字符，结尾为C的字符串
```

### 子串的实际案例

> music_name="大约在冬季"
>
> 

```bash
root@hecs-218409:~# echo ${name#yu}
chao
root@hecs-218409:~# echo ${name##yu}
chao
root@hecs-218409:~# echo $name
yuchao
root@hecs-218409:~# unset name
root@hecs-218409:~# echo $name

root@hecs-218409:~# name="yuchao180"
root@hecs-218409:~# 
root@hecs-218409:~# echo $name
yuchao180
root@hecs-218409:~# echo ${#name}
9
root@hecs-218409:~# 
root@hecs-218409:~# #echo ${name:3}
root@hecs-218409:~# echo ${name:3}
hao180
root@hecs-218409:~# echo ${name:5}
o180
root@hecs-218409:~# echo ${name:2:4}
chao
```

### 计算变量长度的各种玩法

```shell
#解释wc命令参数用法
root@hecs-218409:~# echo $name |wc -w
1
root@hecs-218409:~# echo $name |wc -c
10
root@hecs-218409:~# echo $name |wc -L
9

#利用数值运算expr命令
root@hecs-218409:~/shellLearn# expr length "${name}"
9

#awk统计长度，length函数
root@hecs-218409:~/shellLearn# echo "${name}" | awk '{print length($0)}'
9

#最快的统计方式
echo ${#name}

```

```shell
字符串长度统计方法怎么多，谁最快
time命令，统计命令执行的时长
for循环的shell编程知识
语法
for number（变量） in {1..100}(序列1~100) 
do
     你要做什么事
done
写在一行的就这样
for num in {1..100};do echo $num; done

for port in $(seq 1 6);\
docker run -p 637${port}:6379 -p 1667${port}:16379 --name redis-${port} \
-v /mydata/redis/node-${port}/data:/data \
-v /mydata/redis/node-${port}/conf/redis.conf:/etc/redis/redis.conf \
-d --net redis --ip 172.38.0.1${port} redis:5.0.9-alpine3.11 redis-server /etc/redis/redis.conf

root@hecs-218409:~/shellLearn# for n in {1..3};do str1=`seq -s ":" 10` ;echo $str1; done 
1:2:3:4:5:6:7:8:9:10
1:2:3:4:5:6:7:8:9:10
1:2:3:4:5:6:7:8:9:10
#结合time命令

```

### 实际联系

> 如何删除匹配的子串

```shell
root@hecs-218409:~/ShellLearn# name2="abcABC123ABCabc"
root@hecs-218409:~/ShellLearn# echo ${name2#a*c}
ABC123ABCabc
root@hecs-218409:~/ShellLearn# echo ${name2##a*c}

#利用%形式
root@hecs-218409:~/ShellLearn# echo ${name2%a*c}
abcABC123ABC
root@hecs-218409:~/ShellLearn# echo ${name2%%a*c}

root@hecs-218409:~/ShellLearn#

#没有匹配就原样输出
root@hecs-218409:~/ShellLearn# echo ${name2%%a*C}
abcABC123ABCabc

#替换
root@hecs-218409:~/ShellLearn# echo $str1
Hello,man,i am your brother
root@hecs-218409:~/ShellLearn# echo ${str1/man/boy}
Hello,boy,i am your brother

root@hecs-218409:~/ShellLearn# echo ${str1/o/O}
HellO,man,i am your brother
root@hecs-218409:~/ShellLearn# echo ${str1//o/O}
HellO,man,i am yOur brOther
root@hecs-218409:~/ShellLearn# 

```

### 删除文件名的案例

准备数据

![image-20230312004641583](C:\Users\cao'yang'lin\AppData\Roaming\Typora\typora-user-images\image-20230312004641583.png)

1.去掉所有文件的_finish后缀

```shell
思路
1.单个文件
root@hecs-218409:~/ShellLearn/sub_str# mv chaochao_1_finish.jpg chaochao_1.jpg
root@hecs-218409:~/ShellLearn/sub_str# ll

2.利用变量的子串功能，去掉后缀
root@hecs-218409:~/ShellLearn/sub_str# f=chaochao_1_finish.png
root@hecs-218409:~/ShellLearn/sub_str# echo $f
chaochao_1_finish.png
root@hecs-218409:~/ShellLearn/sub_str# 
root@hecs-218409:~/ShellLearn/sub_str# 
root@hecs-218409:~/ShellLearn/sub_str# 
root@hecs-218409:~/ShellLearn/sub_str# echo ${f//_finish/}
chaochao_1.png
root@hecs-218409:~/ShellLearn/sub_str# 

3.利用反引号的功能,修改文件名
root@hecs-218409:~/ShellLearn/sub_str# mv $f `echo ${f//_finish/}`
root@hecs-218409:~/ShellLearn/sub_str# ll
total 8
drwxr-xr-x 2 root root 4096 Mar 12 00:59 ./
drwxr-xr-x 3 root root 4096 Mar 12 00:42 ../
-rw-r--r-- 1 root root    0 Mar 12 00:44 chaochao_1.jpg
-rw-r--r-- 1 root root    0 Mar 12 00:44 chaochao_1.png
-rw-r--r-- 1 root root    0 Mar 12 00:44 chaochao_2_finish.jpg
-rw-r--r-- 1 root root    0 Mar 12 00:44 chaochao_2_finish.png
-rw-r--r-- 1 root root    0 Mar 12 00:44 chaochao_3_finish.jpg
-rw-r--r-- 1 root root    0 Mar 12 00:44 chaochao_3_finish.png
-rw-r--r-- 1 root root    0 Mar 12 00:44 chaochao_4_finish.jpg
-rw-r--r-- 1 root root    0 Mar 12 00:44 chaochao_4_finish.png
-rw-r--r-- 1 root root    0 Mar 12 00:44 chaochao_5_finish.jpg
-rw-r--r-- 1 root root    0 Mar 12 00:44 chaochao_5_finish.png


4.批量文件名替换，只修改所有的jpg文件
root@hecs-218409:~/ShellLearn/sub_str# for name in `ls *sh.png` ;do mv $name `echo ${name//_finish/}` ;done
root@hecs-218409:~/ShellLearn/sub_str# ll
total 8
drwxr-xr-x 2 root root 4096 Mar 12 01:06 ./
drwxr-xr-x 3 root root 4096 Mar 12 00:42 ../
-rw-r--r-- 1 root root    0 Mar 12 00:44 chaochao_1.jpg
-rw-r--r-- 1 root root    0 Mar 12 00:44 chaochao_1.png
-rw-r--r-- 1 root root    0 Mar 12 00:44 chaochao_2.jpg
-rw-r--r-- 1 root root    0 Mar 12 00:44 chaochao_2.png
-rw-r--r-- 1 root root    0 Mar 12 00:44 chaochao_3.png
-rw-r--r-- 1 root root    0 Mar 12 00:44 chaochao_4.png
-rw-r--r-- 1 root root    0 Mar 12 00:44 chaochao_5.png

```

### 特殊Shell扩展变量

变量的处理

```shell
如果parameter变量值为空，返回word字符串,赋值给result变量
result=${parameter:-word}

如果para变量为空，则word替代变量值，且返回其值
result=${parameter:=word}

如果para变量为空，word当作stderr输出，否则输出变量值
用于设置变量为空导致错误时，返回的错误信息
${parameter:?word}

如果para变量为空，什么都不做，否则word返回
${parameter:+word}
```

### 实际案例

> 判断变量如果值为空，就返回后面字符的信息，可以通过result变量去接受

```shell
root@hecs-218409:~# echo $chao

root@hecs-218409:~# result=${chaoge:-heiheihei}
root@hecs-218409:~# echo $result
heiheihei

```

### 实际应用

数据备份，删除过期数据的脚本

```shell
find xargs 搜索,且删除
#删除七天以上的过期数据
find 需要搜索的目录  -name 你要搜索的名字  -type 文件类型  -mtime+ 7|xargs rm -f


cat del_data.sh

#shell语法
find ${path} -name `*.tar.gz` -type f -mtime +7|xargs rm -f
```

### 父子Shell

```shell
type看是否是内置的
root@hecs-218409:~/ShellLearn/shellXiTong# type java
java is /usr/lib/jvm/java-8-openjdk-amd64/bin/java
root@hecs-218409:~/ShellLearn/shellXiTong# type cd
cd is a shell builtin


ps -f --forest
root@hecs-218409:~/ShellLearn/shellXiTong# ps -f --forest
UID          PID    PPID  C STIME TTY          TIME CMD
root        6991    6903  0 21:30 pts/0    00:00:00 -bash
root        7023    6991  0 21:36 pts/0    00:00:00  \_ bash
root        7038    7023  0 21:42 pts/0    00:00:00      \_ ps -f --forest

#nohup 英文全称 no hang up（不挂起），用于在系统后台不挂断地运行命令，退出终端不会影响程序的运行。

#黑洞文件
就是直接丢弃 这是他的驱动实现的特性
如果我们想保存正确的结果，错误的结果直接丢向垃圾站，既不保存为文件，也不在标准输出打印又该怎么做呢？
command 1>> right.txt 2> /dev/null
直接将错误输出重定向到/dev/null就好了，他好像就是一个无底洞，丢进去的东西就不见了。
root@hecs-218409:~/ShellLearn/shellXiTong# sada 2> /dev/null


#重定向
>>是追加
> 覆盖，重写
1> 和 2>  
他们两个用于将一个文件正确的输出，和错误的输出分开保存。
1> 将正确的输出重定向到某个文件
2> 将错误的输出重定向到某个文件

root@hecs-218409:~/ShellLearn/shellXiTong# echo "sb" >>./a.txt
root@hecs-218409:~/ShellLearn/shellXiTong# ll
total 12
drwxr-xr-x 2 root root 4096 Mar 12 21:51 ./
drwxr-xr-x 4 root root 4096 Mar 12 21:31 ../
-rw-r--r-- 1 root root    3 Mar 12 21:51 a.txt
root@hecs-218409:~/ShellLearn/shellXiTong# cat a.txt
sb

```

## Shell数学运算与双小括号

```shell
#有关于逻辑运算，真，假，真为1，假为0
root@hecs-218409:~/ShellLearn# echo $((8>7))
1  
root@hecs-218409:~/ShellLearn# echo $((8<7))
0

#逻辑与的用法
root@hecs-218409:~/ShellLearn# echo $((8<7&&3>4))
0
root@hecs-218409:~/ShellLearn# echo $((8<7&&3<4))
0
root@hecs-218409:~/ShellLearn# echo $((8>7&&3<4))
1
#逻辑或的用法
root@hecs-218409:~/ShellLearn# echo $((8<7||3<4))
1

#取出运算结果时，必须加$符号

root@hecs-218409:~/ShellLearn# #加减乘除
root@hecs-218409:~/ShellLearn# echo $((3+4))
7
root@hecs-218409:~/ShellLearn# echo $((3*4))
12
root@hecs-218409:~/ShellLearn# echo $((3/4))
0
root@hecs-218409:~/ShellLearn# echo $((3-4))
-1
#幂运算
root@hecs-218409:~/ShellLearn# echo $((3**3))
27
#取模

root@hecs-218409:~# echo $((7%4))
3

#结合变量计算
root@hecs-218409:~# num=5
root@hecs-218409:~# ((num*3))
root@hecs-218409:~# 
root@hecs-218409:~# echo $num
5
root@hecs-218409:~# ((num=num*3))
root@hecs-218409:~# echo $num
15
root@hecs-218409:~# num1=5
root@hecs-218409:~# num1=$((num1*3))
root@hecs-218409:~# echo $num1
15


```

```shell
#复杂的数学运算
root@hecs-218409:~# ((a=2+2**3-4%3))
root@hecs-218409:~# echo $a
9
root@hecs-218409:~# #明确(()) 这个shell扩展计算的语法，在括号里面支持变量的赋值定义操作

```

### 特殊符号的运算

```shell
++
--
```

```shell
read -p "请输入number:" firstnum
print_usage(){
 printf "请输入纯数字:"
 exit -1
}


#上面的代码都是对用户输入的判断
read -p "Please input your operater: " operator
#对运算符进行判断,then要换行，不换行必定报错
if [ "${operator}"!="+"&&"${operator}"!="-"&&"${operator}"!="*"&&"${operator}"!="/" ] 
    then 
    echo "只允许输入加减乘除"
	exit 2
fi
#第二个变量
read -p "Please input your second number: " secondnum

#最后进行数值运算
echo "${firstnum}${operator}${secondnum}结果是:$((${firstnum}${operator}${secondnum}))"

```

```shell
请输入number:34
Please input your operater: +
t2.sh: line 16: [: missing `]'
Please input your second number: 6
34+6结果是:40

```

> 简单的玩法，非常简单的就能计算脚本开发

```shell
root@hecs-218409:~/ShellLearn/shellXiTong# cat t3.sh
#!/bin/bash
echo $(($1))
--------------------------------------------------------------------
root@hecs-218409:~/ShellLearn/shellXiTong# bash t3.sh 3*7
21
root@hecs-218409:~/ShellLearn/shellXiTong# bash t3.sh "7*8"
56
root@hecs-218409:~/ShellLearn/shellXiTong# bash t3.sh "7 * 8"
56
```

> let命令运算
>
> Let命令的执行，效果等同于双小括号
>
> 但是，双小括号效率更高

let实例

```shell
num=8
root@hecs-218409:~/ShellLearn/shellXiTong# let num=num+8
root@hecs-218409:~/ShellLearn/shellXiTong# echo $num
16
```

> 开发，检测nginx服务是否运行的脚本

脚本开发的思路

1.先想好该脚本的功能，作用

2.先写伪代码

### while循环

```bash
while true;do echo "超哥太吊了";sleep 1;done;
超哥太吊了
超哥太吊了
超哥太吊了

```



```
脚本开发的思路
 1.先定义变量，用于存储些变化的值
 2.先安装服务
 3.启动服务
 4.修改配置文件
 5.重启服务
 
```

### expr命令

简单的计算器执行命令

## 实践

```shell
#expr命令并不是很好用，基于空格传入参数
一些特殊的符号是有特殊的含义的，需要转义符
root@hecs-218409:~/ShellLearn/shellXiTong# expr 4 * 5
expr: syntax error: unexpected argument ‘a.txt’
root@hecs-218409:~/ShellLearn/shellXiTong# expr 4 \* 5
20
#逻辑判断
root@hecs-218409:~/ShellLearn/shellXiTong# expr 5 \> 6
0

```

## expr模式匹配

```shell
root@hecs-218409:~/ShellLearn/shellXiTong# expr length 1234567*()asduisam
18
root@hecs-218409:~/ShellLearn/shellXiTong# expr yc.jpg ":" ".*\.jpg"
6
root@hecs-218409:~/ShellLearn/shellXiTong# expr yc.jpgggggg ":" ".*\.jpg"
6
root@hecs-218409:~/ShellLearn/shellXiTong# expr yc.jgggggg ":" ".*\.jpg"
0
```

### expr命令判断文件名的后缀是否合法

```shell
root@hecs-218409:~/ShellLearn/shellXiTong# cat t5.sh
#!/bin/bash

if expr "$1" ":" ".*\.jpg" &> /dev/null
   then 
	   echo "这确实是以jpg结尾的文件!!"
   else
	   echo "这不是jpg文件!!!"
fi

root@hecs-218409:~/ShellLearn/shellXiTong# bash t5.sh ca.jpg
这确实是以jpg结尾的文件!!
root@hecs-218409:~/ShellLearn/shellXiTong# touch 吉尼太没.png
root@hecs-218409:~/ShellLearn/shellXiTong# bash 吉尼太没.png
root@hecs-218409:~/ShellLearn/shellXiTong# bash t5.sh 吉尼太没.png
这不是jpg文件!!!

```

> 找出长度不大于5的单词

```shell
root@hecs-218409:~/ShellLearn/shellXiTong# cat lengthword.sh
#!/bin/bash

#利用for循环
for str1 in I am YU chao,I teach you to learn linux.
do
	if [ `expr length $str1` -lt 5 ]
	then 
		echo $str1
	fi
done
root@hecs-218409:~/ShellLearn/shellXiTong# bash lengthword.sh
I
am
YU
you
to

```

## bc命令

> bc计算器
>
> awk支持数值计算
>
> 中括号运算

bc命令当作计算器来用的，命令行的计算器

```shell
root@hecs-218409:~/ShellLearn/shellXiTong# bc
bc 1.07.1
Copyright 1991-1994, 1997, 1998, 2000, 2004, 2006, 2008, 2012-2017 Free Software Foundation, Inc.
This is free software with ABSOLUTELY NO WARRANTY.
For details type `warranty'. 
34-89
-55
3.5-9.78
-6.28
4.67/9.56
0
```

> bc命令结合管道符来计算数学

```shell
root@hecs-218409:~/ShellLearn/shellXiTong# echo "4*4"
4*4
root@hecs-218409:~/ShellLearn/shellXiTong# echo "4*4" |bc
16

root@hecs-218409:~/ShellLearn/shellXiTong# num=8
root@hecs-218409:~/ShellLearn/shellXiTong# result=`echo $num*4 |bc`
root@hecs-218409:~/ShellLearn/shellXiTong# echo $result
32

```

## bc案例

```shell
计算出1~1000的总和
数学公式
1+2+3+4+5......
root@hecs-218409:~/ShellLearn/shellXiTong# echo {1..100} |tr " " "+"
1+2+3+4+5+6+7+8+9+10+11+12+13+14+15+16+17+18+19+20+21+22+23+24+25+26+27+28+29+30+31+32+33+34+35+36+37+38+39+40+41+42+43+44+45+46+47+48+49+50+51+52+53+54+55+56+57+58+59+60+61+62+63+64+65+66+67+68+69+70+71+72+73+74+75+76+77+78+79+80+81+82+83+84+85+86+87+88+89+90+91+92+93+94+95+96+97+98+99+100

root@hecs-218409:~/ShellLearn/shellXiTong# echo {1..100} |tr " " "+" |bc
5050

#双括号
root@hecs-218409:~/ShellLearn/shellXiTong# echo $((`seq -s "+" 100`))
5050

```

### awk计算

awk支持if条件判断，数组，等等

```shell
root@hecs-218409:~# echo "3.2 2.2" | awk '{print $1+$2}'
5.4

```

## 中括号计算

```shell
root@hecs-218409:~# res=$[3+5]
root@hecs-218409:~# echo $res
8

```

## read

```shell
read
root@hecs-218409:~# read -t 5 -p "请输入你的名字，年龄"
请输入你的名字，年龄root@hecs-218409:~# read -t 15 -p "请输入你的名字，年龄" yourname yourage
请输入你的名字，年龄chaohcao 18
root@hecs-218409:~# echo $yourname $yourage
chaohcao 18

```

## Shell的条件判断

> 得出真和假的概念
>
> shell提供条件测试的语法
>
> []中括号

![image-20230313134258861](C:\Users\cao'yang'lin\AppData\Roaming\Typora\typora-user-images\image-20230313134258861.png)

## test条件测试

test命令评估一个表达式,它的结果为真，还是假，如果条件为真状态码就为0否则就是不为0

```
test命令的参数
-e 判断该文件是否存在，（普通文件，目录），存在就为真否则就为假

```

```shell
drwxr-xr-x 4 root root 4096 Mar 12 23:01 ./
drwx------ 6 root root 4096 Mar 13 16:37 ../
drwxr-xr-x 2 root root 4096 Mar 13 12:32 shellXiTong/
drwxr-xr-x 2 root root 4096 Mar 12 22:58 sub_str/
#当结果为假
root@hecs-218409:~/ShellLearn# test -e sb.py
root@hecs-218409:~/ShellLearn# echo $?
1
#当结果为真
root@hecs-218409:~/ShellLearn# test -e shellXiTong
root@hecs-218409:~/ShellLearn# echo $?
0

```

## test的语法大全

![image-20230313164446549](C:\Users\cao'yang'lin\AppData\Roaming\Typora\typora-user-images\image-20230313164446549.png)

## test命令实践

-e判断文件是否存在。存在为真，否则为假

```shell
test 测试参数 要测试的对象 对结果进行判断执行的逻辑动作

root@hecs-218409:~/ShellLearn# test -e heihei.txt && echo "这个存在"
root@hecs-218409:~/ShellLearn# test -e heihei.txt && echo "这个存在" ||touch "heihei.txt"
root@hecs-218409:~/ShellLearn# ll
total 16
drwxr-xr-x 4 root root 4096 Mar 13 16:53 ./
drwx------ 6 root root 4096 Mar 13 16:37 ../
-rw-r--r-- 1 root root    0 Mar 13 16:53 heihei.txt
drwxr-xr-x 2 root root 4096 Mar 13 12:32 shellXiTong/
drwxr-xr-x 2 root root 4096 Mar 12 22:58 sub_str/
root@hecs-218409:~/ShellLearn# test -e heihei.txt && echo "这个存在" ||touch "heihei.txt"
这个存在




```

-f  判断文件是否是普通文件类型

```shell
drwxr-xr-x 4 root root 4096 Mar 13 16:53 ./
drwx------ 6 root root 4096 Mar 13 16:37 ../
-rw-r--r-- 1 root root    0 Mar 13 16:53 heihei.txt
drwxr-xr-x 2 root root 4096 Mar 13 12:32 shellXiTong/
drwxr-xr-x 2 root root 4096 Mar 12 22:58 sub_str/
root@hecs-218409:~/ShellLearn# test -f heihei.txt && echo ok ||echo no
ok
root@hecs-218409:~/ShellLearn# test -f sub_str.txt && echo ok ||echo no
no
root@hecs-218409:~/ShellLearn# test -f sub_str && echo ok ||echo no
no

```

-d  判断是否是目录类型

```shell
drwxr-xr-x 4 root root 4096 Mar 13 16:53 ./
drwx------ 6 root root 4096 Mar 13 16:37 ../
-rw-r--r-- 1 root root    0 Mar 13 16:53 heihei.txt
drwxr-xr-x 2 root root 4096 Mar 13 12:32 shellXiTong/
drwxr-xr-x 2 root root 4096 Mar 12 22:58 sub_str/
root@hecs-218409:~/ShellLearn# test -d sub_str && echo ok ||echo no
ok
root@hecs-218409:~/ShellLearn# test -d heihei.txt && echo ok ||echo no
no

```

-z  希望字符串为空，就为真，否则就为假

```shell
root@hecs-218409:~/ShellLearn# test -z "" && echo ok || echo no
ok
root@hecs-218409:~/ShellLearn# test -z " " && echo ok || echo no
no

```

-n  反过来的，希望字符串是有内容的，就为真，否则为假

```shell
root@hecs-218409:~/ShellLearn# test -n " " && echo ok || echo no
ok
root@hecs-218409:~/ShellLearn# test -n "" && echo ok || echo no
no

```

## 中括号的条件测试

比如比较字符串、判断文件是否存在及是否可读等，通常用"[]"来表示条件测试。

注意：这里的空格很重要。要确保方括号的空格。笔者就曾因为空格缺少或位置不对，而浪费好多宝贵的时间。

if ....; then
....
elif ....; then
....
else
....
fi

```shell
[ -f "somefile" ] ：判断是否是一个文件
[ -x "/bin/ls" ] ：判断/bin/ls是否存在并有可执行权限
[ -n "$var" ] ：判断$var变量是否有值
[ "$a" = "$b" ] ：判断$a和$b是否相等
-r file　　　　　用户可读为真
-w file　　　　　用户可写为真
-x file　　　　　用户可执行为真
-f file　　　　　文件为正规文件为真
-d file　　　　　文件为目录为真
-c file　　　　　文件为字符特殊文件为真
-b file　　　　　文件为块特殊文件为真
-s file　　　　　文件大小非0时为真
-t file　　　　　当文件描述符(默认为1)指定的设备为终端时为真
```

```shell
root@hecs-218409:~/ShellLearn# [ -f "heihei.txt"  ] && echo "吴彦祖好帅" ||echo "吴彦祖不存在"
吴彦祖好帅
```

```shell
root@hecs-218409:~/ShellLearn# [ -d "shellXiTong"  ] && echo "目录存在" ||echo "目录不存在"
目录存在

```

## 双中括号

> [[  条件表达式  ]]
>
> 验证文件是否有权限，写入权限
>
> 注意:root 是个不讲道理的，超级用户
>
> 需要切换普通用户
>
> 

```shell
#想要查看文件内容时，先测试下是否有查看的权限，否则就报错
[[ -r "大玩宽面.txt" ]] && cat 大玩宽面.txt ||echo "你没有权限看什么?"
[[ -w "大玩宽面.txt" ]] && echo "你看这个面，它又大又圆" > 大玩宽面.txt ||echo "你没有权限写什么?"
```

## 变量测试

> 对变量测试

```shell
root@hecs-218409:~/ShellLearn# name=heihei.txt
root@hecs-218409:~/ShellLearn# [ -f "$name"  ] && echo "鸡你太没" || echo "我是个好人"
鸡你太没
root@hecs-218409:~/ShellLearn# 

```

那就是看大神写的脚本

















## 字符串的判断

```shell
str1 = str2　　　　　　当两个串有相同内容、长度时为真
str1 != str2　　　　　 当串str1和str2不等时为真
-n str1　　　　　　　 当串的长度大于0时为真(串非空)
-z str1　　　　　　　 当串的长度为0时为真(空串)
str1　　　　　　　　  当串str1为非空时为真
```



```bash
root@hecs-218409:~/ShellLearn# cat str_001.sh
#!/bin/bash
 if [ "syu" = "u" ]
 then 
	 echo "sb"
 fi
#if [ ! "syu" = "u" ]  取反
```

## 中括号的数值比较

```shell
#必须要加转义符
root@hecs-218409:~# [ 2 < 1 ] && echo yes || echo no;
-bash: 1: No such file or directory
no
root@hecs-218409:~# [ 2 \< 1 ] && echo yes || echo no;
no
root@hecs-218409:~# [ 2 \> 1 ] && echo yes || echo no;
yes

```

## 双中括号

对单中括号的补充，双中括号还支持正则处理

在双中括号就不需要转义符了

```shell
root@hecs-218409:~# [[ 5 > 6  ]] && echo yes ||echo no;
no
root@hecs-218409:~# [[ 5 < 6  ]] && echo yes ||echo no;
yes

```

在工作中，用的最多的就是单中括号，双中括号属于特殊场景的扩展语法

## 逻辑判断符号

```shell
&&              -a                  与 运算，两边都为真，结果才为真
||              -o                  或运算，两边有一个为真，结果就为真

```

中括号逻辑比较

```shell
root@hecs-218409:~/ShellLearn# [ -f "$file01" -a -f "$file02" ] && echo yes || echo no
no
root@hecs-218409:~/ShellLearn# [ -f "$file01" -o -f "$file02" ] && echo yes || echo no
yes
root@hecs-218409:~/ShellLearn# [ -f "$file01" || -f "$file02" ] && echo yes || echo no
-bash: [: missing `]'
-f: command not found
no

```

## 双中括号

```shell
root@hecs-218409:~/ShellLearn# [[ -n "$a" && "a" = "b"  ]] && echo yes || echo no
no

```

## 逻辑运算的实战脚本

1.脚本

接受用户输入，判断它是否等于某个数字

```shell
root@hecs-218409:~/ShellLearn# cat test_and_or.sh
#!bin/bash

read -p "plase input a char :" var1

#逻辑条件测试
[ "$var1" -eq "1" ] && {
      echo $var1
      exit 0
}

[ "$var1" = "2" ] && {
     echo $var1
     exit 0
}

# 只能输入的是一或者2，否则就报错
[ "$var1" != "2" -a "$var1" != "1" ] && {
     echo "脚本出错，必须输入1或者2"
     exit 1
}

```

## 安装lnmp/lamp脚本开发

```shell
root@hecs-218409:~/ShellLearn/test_scripts# echo "echo LAMP is installed" > ./lamp.sh
root@hecs-218409:~/ShellLearn/test_scripts# echo "echo LNMP is installed" > ./lnmp.sh
root@hecs-218409:~/ShellLearn/test_scripts# chmod +x lamp.sh
root@hecs-218409:~/ShellLearn/test_scripts# chmod +x lnmp.sh

```

```shell
root@hecs-218409:~/ShellLearn/test_scripts# cat lamp_or_lnmp.sh
#!/bin/bash

#先判断脚本目录是否存在
path=/root/ShellLearn/test_scripts

#条件判断

[ ! -d "$path" ] && mkdir $path -p

#开发脚本的正常逻辑
cat <<END
    1.[install lamp]
    2.[install lnmp]
    3.[exit]
    pls input the num your want;

END


read num

#根据该num变量进行逻辑处理
expr $num + 1 &> /dev/null

#判断上条命令的结果
#限制用户输入的必须是数字
[ $? -ne 0 ] && {
	echo "The num your input must be {1|2|3}"
        exit 1
}
#对输入的数字，是1，2，3判断
[ "$num" -eq 1 ] && {
   echo "Starting installing lamp....wait"
   sleep 2;
   #执行lamp.sh的安装脚本
   [ -x "$path/lamp.sh"  ] || {
        echo "The file does not exist or cannot be exec:"
        exit 1
   } 
	  
   source $path/lamp.sh
   exit $?
}

#开发选择2的情况,安装lnmp
[ "$num" -eq 2 ] && {
   echo "Starting installing lnmp....wait"
   sleep 2;
   #执行lamp.sh的安装脚本
   [ -x "$path/lnmp.sh"  ] || {
        echo "The file does not exist or cannot be exec:"
        exit 1
   } 
           
   $path/lnmp.sh
   exit $?
}

#退出
[ "$num" -eq 3  ] && {
   echo "byebye"
   exit 3
}

#限制用户必须输入的是1,2,3
#[[]]支持正则表达式
[[ ! "$num" =~ [1-3] ]] && {
     echo "The num you input must be {1|2|3}"
     echo "你这个大笨蛋，必须按照说明来"
     exit 4
}

```

## if语句开发

> 单分支if
>
> if           <条件表达式>
>
> ​       then
>
> ​            代码........
>
> fi
>
> 简化
>
> if   <条件表达式>; then
>
> ​     代码 ..........
>
> fi

## 双if语句

![image-20230314142500334](C:\Users\cao'yang'lin\AppData\Roaming\Typora\typora-user-images\image-20230314142500334.png)

## if-else处理

```shell
if <条件表达式>
   then
     当条件成立
else  #else是不需要then的
   否则
fi

```

## 多分支处理

语法   if   elif 的嵌套，不超过三层

```shell
if <>
   then
      代码
elif <>
   then
elif <>
   then
else
fi
```

## if实践

1.单分支

2.if分支的嵌套

3.开发一个内存监控的脚本

4.开发rsync启停脚本

5.作业，nginx

## 单分支if

```shell
root@hecs-218409:~/ShellLearn/test_scripts# cat if_1.sh
#!/bin/bash
if [ -f /etc/hosts  ] 
then
	echo "yes"

fi

if [[ -f /etc/hosts ]];then
	echo "[[]] is ok "
fi

if test -f /etc/hosts ;then
	echo "test it's ok"
fi


```

## 开发系统监控脚本

> 开发shell脚本
>
> 1.检测linux剩余可用内存，当可用内存小于10G,就发邮件
>
> 2.并且该脚本加入crontab,每三分钟检查一次内存

思路

1.获取当前内存情况

2.配置邮件告警,用Linux发送邮件，邮件内容是内存情况

3.开发脚本,判断剩余内存是否小于10G

4.脚本加入crontab，写规则

## 开发过程

```shell
root@hecs-218409:~/ShellLearn/test_scripts# free -m | awk 'NR==2 {print $NF}'
3132
#定时任务
root@hecs-218409:~/ShellLearn/test_scripts# crontab -l
no crontab for root

root@hecs-218409:~/ShellLearn/test_scripts# cat free_1.sh
#!/bin/bash

FreeMem=`free -m | awk 'NR==2 {print $NF}' `
CHARS="Current memory is $FreeMem"
if [ "$FreeMem" -lt "1000" ]
then 
	echo $CHARS | tee /tmp/messages.txt
	mail -s "date  "
fi
```

## if实战研发

```shell
root@hecs-218409:~/ShellLearn/test_scripts# bash if_read.sh 4 5
yes,4 less than 5
root@hecs-218409:~/ShellLearn/test_scripts# bash if_read.sh 5 5
yes,5 equal 5
root@hecs-218409:~/ShellLearn/test_scripts# bash if_read.sh 6 5
yes,6 grather than 5
root@hecs-218409:~/ShellLearn/test_scripts# cat if_read.sh
#!/bin/bash

a=$1
b=$2
if [ "$a" -lt "$b" ]
then 
	echo "yes,$a less than $b"
	exit 0
fi

if [ "$a" -eq "$b" ]
then 
	echo "yes,$a equal $b"
        exit 0
fi


if [ "$a" -gt "$b" ]; then
	echo "yes,$a grather than $b"
	exit 0;
fi

```

## 多分支脚本

```shell
root@hecs-218409:~/ShellLearn/test_scripts# bash if_read.sh 6 5
yes,6 grather than 5
root@hecs-218409:~/ShellLearn/test_scripts# bash if_read.sh 3 5
yes,3 less than 5
root@hecs-218409:~/ShellLearn/test_scripts# bash if_read.sh 5 5
yes,5 equal 5
```

```shell
root@hecs-218409:~/ShellLearn/test_scripts# cat if_read.sh
#!/bin/bash

a=$1
b=$2
if [ "$a" -lt "$b" ]
then 
	echo "yes,$a less than $b"
	exit 0
elif [ "$a" -eq "$b" ]
then 
	echo "yes,$a equal $b"
        exit 0
elif [ "$a" -gt "$b" ]; then
	echo "yes,$a grather than $b"
	exit 0;
fi

```

## 开发mysql监控脚本

```shell
root@hecs-218409:~/ShellLearn/test_scripts# netstat -tunlp

```

> 远程监控mysql端口

```shell
#namp 端口扫描
```

> 进程检测

```shell
ps -ef | grep mysql
```

## 通过编程语言连接MySQL







## while循环

```shell
#!/bin/bash
echo "sb";
while  test -e heihei.txt #变量
do
        echo "250"
done

```

## 别名

```shell
root@hecs-218409:~# alias
alias egrep='egrep --color=auto'
alias fgrep='fgrep --color=auto'
alias grep='grep --color=auto'
alias l='ls -CF'
alias la='ls -A'
alias ll='ls -alF'
alias ls='ls --color=auto'
root@hecs-218409:~# 

```

## shell函数开发

简化版本的函数定义与使用

```shell
1.先定义函数
2.使用函数

```

## shell函数定义的语法

```shell
function 函数ming(){
   函数体
   return 返回值
}

##偷懒的方法,可以丢掉（）
function 函数名{
   函数体
   return
}

##超级懒
函数名(){
  函数体
  return 返回值
}
#执行函数名
函数名()
```

## 执行函数的基础概念

```shell
root@hecs-218409:~/ShellLearn# cat -n t3.sh
     1	#!/bin/bash
     2	function  chaochao(){
     3	
     4	  echo "我准备创建一个文件，且写入信息"
     5	  echo "爱的魔力转圈圈" >> music.txt
     6	  return 0
     7	}
     8	chaochao
     9	

```

> 场景2
>
> 函数的定义和执行，分开在不同的文件中

```shell
查看set
null
source 文件.sh 
查看set
root@hecs-218409:~/ShellLearn# set | grep "fy"
fy () 
root@hecs-218409:~/ShellLearn# 
#退出了
#就没了
#在加载source
root@hecs-218409:~/ShellLearn# set | grep "fy"
fy () 
root@hecs-218409:~/ShellLearn# fy
我能飞

```



```shell
root@hecs-218409:~/ShellLearn# bash t5.sh
我能飞
root@hecs-218409:~/ShellLearn# cat t5.sh
#!/bin/bash

source t4.sh
fy

```

## 函数脚本传入参数

```shell
root@hecs-218409:~/ShellLearn# bash t5.sh
我能飞
兄台你传入的参数,,,一共是0
root@hecs-218409:~/ShellLearn# bash t5.sh s 6 7
我能飞
兄台你传入的参数s,6,7,一共是3

root@hecs-218409:~/ShellLearn# cat t5.sh
#!/bin/bash

source t4.sh
fy
helloChuan $1 $2 $3

root@hecs-218409:~/ShellLearn# cat t4.sh
#!/bin/bash

fy(){
   echo "我能飞"
}

helloChuan(){
   echo "兄台你传入的参数$1,$2,$3,一共是$#"


}
```



## 函数实战开发

> 1.检测url是否正常开发，要求是函数开发形式

```shell
root@hecs-218409:~/ShellLearn# vim check_url_func.sh
root@hecs-218409:~/ShellLearn# bash check_url_func.sh www.baidu.com
www.baidu.com is running...
root@hecs-218409:~/ShellLearn# cat  check_url_func.sh
#!/bin/bash

#针对脚本功能，做一个帮助提示
if [ "$#" -ne 1 ]
then
	echo "Usage : $0 url"
	exit 1
fi

#利用wget命令测试url是否正常
wget --spider -q -o /dev/null --tries=1 -T 5 $1

#对状态码进行判断，是否正常
if [ "$?" -eq 0 ]
then
	echo "$1 is running..."
else
	echo "$1 is down...."
fi

```

> 函数开发

```shell
root@hecs-218409:~/ShellLearn# cat function_test001.sh
#!/bin/bash

usage(){
  echo "Usage: $0 url"
  exit 1
}

#功能检测url
check_url(){

	wget --spider -q -o /dev/null --tries=1 -T 5 $1
	if [ "$?" -eq 0 ]
then
	echo "$1 is running..."
else
	echo "$1 is down...."
fi
}

#参照c语言开发形式，设立一个main函数
main(){
	if [ "$#" -ne 1 ]
then    
	usage
	
fi
   check_url

}

main $*

```



### openJDK的安装

![image-20230309200538824](C:\Users\cao'yang'lin\AppData\Roaming\Typora\typora-user-images\image-20230309200538824.png)







