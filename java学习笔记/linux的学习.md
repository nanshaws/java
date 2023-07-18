# Linux的学习

# man -f  [指令]

用来查找指令和指令的作用的

```bash
man -f cd
man -f grep
```

![image-20230128201103966](C:\Users\cao'yang'lin\AppData\Roaming\Typora\typora-user-images\image-20230128201103966.png)

# man date展示man里面的信息的

![image-20230128201233267](C:\Users\cao'yang'lin\AppData\Roaming\Typora\typora-user-images\image-20230128201233267.png)

![image-20230128201304690](C:\Users\cao'yang'lin\AppData\Roaming\Typora\typora-user-images\image-20230128201304690.png)

date （1）代表在shell环境中可以执行的指令或可执行文件

依次类推

# man -k [指令]

找出所有包含这个指令字的文档

# info [指令]

和man指令一样，不过它会显示一部分页面

 File：代表这个 info page 的资料是来自 info.info 档案所提供的；

  Node：代表目前的这个页面是属亍 Top 节点。 意思是 info.info 内吨有径多信息，而 Top 仅是 info.info 档案内的一个节点内容而已；

  Next：下一个节点的名称为 Getting Started，你也可以挄『N』到下个节点去； 

 Up：回到上一层的节点总揽画面，你也可以挄下『U』回到上一层； 

 Prev：前一个节点。但由亍 Top 是 info.info 的第一个节点，所以上面没有前一个节点的信息。

![image-20230128203106283](C:\Users\cao'yang'lin\AppData\Roaming\Typora\typora-user-images\image-20230128203106283.png)

# bc指令（计算机）

![image-20230128203856055](C:\Users\cao'yang'lin\AppData\Roaming\Typora\typora-user-images\image-20230128203856055.png)

# who指令，netstat -a 指令 shutdown和reboot指令

 观察系统的使用状态： 如果要看目前有谁在在线，可以下达『who』这个指令，而如果要看网绚的联机状态，可以下达 『 netstat -a 』这个指令，而要看背景执行的程序可以执行『 ps -aux 』这个指令。使用这些指令可以让你稍微了览主机目前的使用状态！当然啰，就可以让你判断是否可以关机了 （这些指令在后面 Linux 常用指令中会提及喔！） 

 通知在线使用者关机的时刻： 要关机前总得给在线的使用者一些时间来结束他们的工作，所以，这个时候你可以使用 shutdown 的特别指令来达到此一功能。 

 正确的关机指令使用： 例如 shutdown 不 reboot 两个指令！

 将数据同步写入硬盘中的指令： sync

  惯用的关机指令： shutdown 

 重新启劢，关机： reboot, halt, poweroff

# 切换执行等级： init

 run level 0：关机

  run level 3：纯文本模式

  run level 5：含有图形接口模式

  run level 6：重新启劢

```bash
init 0 
```

关机（代码上面）

# 文件怎么看

![image-20230129110102038](C:\Users\cao'yang'lin\AppData\Roaming\Typora\typora-user-images\image-20230129110102038.png)

​                                      连接数

![image-20230129111628489](C:\Users\cao'yang'lin\AppData\Roaming\Typora\typora-user-images\image-20230129111628489.png)

![image-20230129112815299](C:\Users\cao'yang'lin\AppData\Roaming\Typora\typora-user-images\image-20230129112815299.png)

进入目录要x的权限（x是可执行文件），r是进入文档的权限，w是可写文件

# 修改权限

 chgrp ：改变档案所属群组

  chown ：改变档案拥有者 

 chmod ：改变档案的权限, SUID, SGID, SBIT 等等的特怅

```bash
chown it:root nihao.txt
```

```bash
chmod 444 hao.txt
chmod u=rrr mk 
```

![image-20230129122331452](C:\Users\cao'yang'lin\AppData\Roaming\Typora\typora-user-images\image-20230129122331452.png)

![image-20230129122439838](C:\Users\cao'yang'lin\AppData\Roaming\Typora\typora-user-images\image-20230129122439838.png)

![image-20230129124552114](C:\Users\cao'yang'lin\AppData\Roaming\Typora\typora-user-images\image-20230129124552114.png)

![image-20230129124821298](C:\Users\cao'yang'lin\AppData\Roaming\Typora\typora-user-images\image-20230129124821298.png)

# cp指令

![image-20230129120926664](C:\Users\cao'yang'lin\AppData\Roaming\Typora\typora-user-images\image-20230129120926664.png)

复制执行者的属性与权限

# cd 目录所需要的权限至少要x权限和r权限

\# 因为具有 r 的权限可以查询档名。不过权限不足(没有 x)，所以会有一堆问号。

![image-20230129132441370](C:\Users\cao'yang'lin\AppData\Roaming\Typora\typora-user-images\image-20230129132441370.png)

![image-20230129132601003](C:\Users\cao'yang'lin\AppData\Roaming\Typora\typora-user-images\image-20230129132601003.png)

目录(directory)： 就是目录啰～第一个属性为 [ d ]，例如 [drwxrwxrwx]。

连结档(link)： 就是类似 Windows 系统底下的快捷方式啦！ 第一个属性为 [ l ](英文 L 的小写)，例如 [lrwxrwxrwx] ；

以避免一些特殊字符比较好！例如底下这些： * ? > < ; & ! [ ] | \ ' " ` ( ) { }

# 注意w权限很大

负责文件的写，删操作

# 目录放置规则

![image-20230129143040801](C:\Users\cao'yang'lin\AppData\Roaming\Typora\typora-user-images\image-20230129143040801.png)

1. cd /var/log (absolute)

2. cd ../var/log (relative) 因为你在 /home 底下，所以要回到上一层 (../) 后，才能继续往 /var 来移动的！ 特别注意这两个特殊的目录：

  . ：代表当前的目彔，也可以使用 ./ 来表示；

  .. ：代表上一层目彔，也可以 ../ 来代表。

```bash
[root@www ~]# cd [相对路径戒绝对路径]
# 最重要癿就是目弽癿绝对路径不相对路径，还有一些特殊目弽癿符号啰！
[root@www ~]# cd ~vbird
# 代表去到 vbird 这个用户癿家目弽，亦卲 /home/vbird
[root@www vbird]# cd ~
# 表示回到自己癿家目弽，亦卲是 /root 这个目弽
[root@www ~]# cd
# 没有加上任何路径，也还是代表回到自己家目弽癿意忠喔！
[root@www ~]# cd ..
# 表示去到目前癿上层目弽，亦卲是 /root 癿上层目弽癿意忠；
[root@www /]# cd -
# 表示回到刚刚癿那个目弽，也就是 /root 啰～
[root@www ~]# cd /var/spool/mail
# 这个就是绝对路径癿写法！直接挃定要去癿完整路径名称！
[root@www mail]# cd ../mqueue
# 这个是相对路径癿写法，我们由/var/spool/mail 去到/var/spool/mqueue 就
这样写！

```

# pwd (显示目前所在的目录)

```bash
-P ：显示出确实的路径，而非使用链接 (link) 路径。
范例：单纯显示出目前的工作目录：
[root@www ~]# pwd
/root <== 显示出目录啦～
范例：显示出实际的工作目录，而非链接文件本身的目录名而已
[root@www ~]# cd /var/mail <==注意，/var/mail 是一个连结档
[root@www mail]# pwd
/var/mail <==列出目前的工作目弽
[root@www mail]# pwd -P
/var/spool/mail <==忟么回事？有没有加 -P 差徆多～
[root@www mail]# ls -ld /var/mail
lrwxrwxrwx 1 root root 10 Sep 4 17:54 /var/mail -> spool/mail
# 看到这里应该知道为啥了吧？因为 /var/mail 是连结档，连结到
/var/spool/mail
# 所以，加上 pwd -P 癿选项后，会丌以连结文件癿数据显示，而是显示正确的
完整路径啊！
```

```bash
[root@www ~]# mkdir [-mp] 目录名称
选项不参数：
-m ：配置文件案的权限喔！直接讴定，丌需要看预讴权限 (umask) 癿脸色～
-p ：帮劣你直接将所需要癿目弽(包吨上层目弽)递弻建立起杢！
范例：请到/tmp 底下尝试建立数个新目弽看看：
[root@www ~]# cd /tmp
[root@www tmp]# mkdir test <==建立一名为 test 的新目录
[root@www tmp]# mkdir test1/test2/test3/test4
mkdir: cannot create directory `test1/test2/test3/test4':
No such file or directory <== 没办法直接建立此目录啊！
[root@www tmp]# mkdir -p test1/test2/test3/test4
# 加了这个 -p 的选项，可以自行帮你建立多层目录！
范例：建立权限为 rwx--x--x 的目录
[root@www tmp]# mkdir -m 711 test2
[root@www tmp]# ls -l
drwxr-xr-x 3 root root 4096 Jul 18 12:50 test
drwxr-xr-x 3 root root 4096 Jul 18 12:53 test1
```

```bash
[root@www ~]# rmdir [-p] 目录名称
选项不参数：
-p ：连同上层『空癿』目录也一起删除
范例：将亍 mkdir 范例中建立的目录(/tmp 底下)删除掉！
[root@www tmp]# ls -l <==看看有多少目录存在？
drwxr-xr-x 3 root root 4096 Jul 18 12:50 test
drwxr-xr-x 3 root root 4096 Jul 18 12:53 test1
drwx--x--x 2 root root 4096 Jul 18 12:54 test2
[root@www tmp]# rmdir test <==可直接删除掉，没问题
[root@www tmp]# rmdir test1 <==因为尚有内容，所以无法删除！
rmdir: `test1': Directory not empty
[root@www tmp]# rmdir -p test1/test2/test3/test4
[root@www tmp]# ls -l <==您看看，底下癿输出中 test 不 test1 丌见
了！
drwx--x--x 2 root root 4096 Jul 18 12:54 test2
# 瞧！利用 -p 这个选项，立刻就可以将 test1/test2/test3/test4 一次删除～
# 不过要注意的是，这个 rmdir 仅能『删除空的目录』喔！
```

```bash
范例：先用 root 的身份列出搜寻的路径为何？
[root@www ~]# echo $PATH
/usr/kerberos/sbin:/usr/kerberos/bin:/usr/local/sbin:/usr/local/bin:/sbin
:/bin:/usr/sbin:/usr/bin:/root/bin <==这是同一行！
范例：用 vbird 的身份列出搜寻的路径为何？
[root@www ~]# su - vbird
[vbird@www ~]# echo $PATH
/usr/kerberos/bin:/usr/local/bin:/bin:/usr/bin:/home/vbird/bin
# 仔绅看，一般用户 vbird 癿 PATH 中，幵丌包含任何『sbin』的目录存在喔！
```

```bash
[root@www ~]# mv /bin/ls /root
# mv 为移动，可将档案在不同的目录间进行移动作业
```

将 ls 由/bin/ls 移动成为/root/ls（上面）

```bash
[root@www ~]# ls [-aAdfFhilnrRSt] 目录名称
[root@www ~]# ls [--color={never,auto,always}] 目录名称
[root@www ~]# ls [--full-time] 目录名称
选项不参数：
-a ：全部的档案，连同隐藏档( 开头为 . 的档案) 一起列出来(常用)
-A ：全部的档案，连同隐藏档，但不包括 . 不 .. 这两个目录
-d ：仅列出目录本身，而不是列出目录内的档案数据(常用)
-f ：直接列出结果，而不进行排序 (ls 预讴会以档名排序！)
-F ：根据档案、目录等信息，给予附加数据结构，例如：
 *:代表可执行文件； /:代表目录； =:代表 socket 档案； |:代表 FIFO 档案；
-h ：将档案容量以人类较易读的方式(例如 GB, KB 等等)列出来；
-i ：列出 inode 号码，inode 癿意义下一章将会介绍；
-l ：长数据串行出，包吨档案癿属性不权限等等数据；(常用)
-n ：列出 UID 与 GID 而非使用者与群组的名称 (UID 不 GID 会在账号管理提
到！)
-r ：将排序结果反向输出，例如：原本档名由小到大，反向则为由大到小；
-R ：连同子目录内容一起列出杢，等亍该目录下癿所有档案都会显示出来；
-S ：以档案容量大小排序，而不是用档名排序；
-t ：依时间排序，而不是用档名。
--color=never ：不要依据档案特性给予颜色显示；
--color=always ：显示颜色
--color=auto ：让系统自行依据设定来判断是否给予颜色
--full-time ：以完整时间模式 (包含年、月、日、时、分) 输出
--time={atime,ctime} ：输出 access 时间或改变权限属性时间 (ctime)
 而非内容变更时间 (modification time)
```

# rm -rf bianyi(目录)强制删除目录里面的所有包括目录

rm -r 依次删除目录里面的东西包括目录

rm -f 强制删除

配合使用

rm -rf

-i ：互动模式，在删除前会询问使用者是否删除

rm -ri 互动删除

```bash
[root@www ~]# mv [-fiu] source destination
[root@www ~]# mv [options] source1 source2 source3 .... directory
选项不参数：
-f ：force 强制癿意忠，如果目标档案已经存在，丌会询问而直接覆盖；
-i ：若目标档案 (destination) 已经存在时，就会询问是否覆盖！
-u ：若目标档案已经存在，丏 source 比较新，才会更新 (update)
范例一：复制一档案，建立一目弽，将档案移劢到目弽中
[root@www ~]# cd /tmp
[root@www tmp]# cp ~/.bashrc bashrc
[root@www tmp]# mkdir mvtest
[root@www tmp]# mv bashrc mvtest
# 将某个档案移劢到某个目弽去，就是这样做！
范例二：将刚刚癿目弽名称更名为 mvtest2
[root@www tmp]# mv mvtest mvtest2 <== 这样就更名了！简单～
# 其实在 Linux 底下还有个有趣癿挃令，名称为 rename ，
# 该挃令与职迚行多个档名癿同时更名，幵非针对单一档名变更，不 mv 丌同。
请 man rename。
范例三：再建立两个档案，再全部移劢到 /tmp/mvtest2 弼中
[root@www tmp]# cp ~/.bashrc bashrc1
[root@www tmp]# cp ~/.bashrc bashrc2
[root@www tmp]# mv bashrc1 bashrc2 mvtest2
# 注意到这边，如果有多个杢源档案戒目弽，则最后一个目标文件一定是『目
弽！』
# 意忠是说，将所有癿数据移劢到该目弽癿意忠！

```

```bash
mv tc ../cmake01
```

![image-20230129205818253](C:\Users\cao'yang'lin\AppData\Roaming\Typora\typora-user-images\image-20230129205818253.png)

mv更改名字

```bash
mv tc hj
```

![image-20230129210059525](C:\Users\cao'yang'lin\AppData\Roaming\Typora\typora-user-images\image-20230129210059525.png)

 cat 由第一行开始显示档案内容 

 tac 从最后一行开始显示，可以看出 tac 是 cat 的倒着写！

  nl 显示的时候，顺道输出行号！

  more 一页一页的显示档案内容 

 less 不 more 类似，但是比 more 更好的是，他可以往前翻页！ 

 head 叧看头几行 

 tail 叧看尾巴几行 

 od 以二进制的方式读取档案内容！

```bash
[root@www ~]# cat [-AbEnTv]
选项不参数：
-A ：相弼亍 -vET 的整合选项，可列出一些特殊字符而不是空白而已；
-b ：列出行号，仅针对非空白行做行号显示，空白行不标行号！
-E ：将结尾的断行字符 $ 显示出来；
-n ：打印出行号，连同空白行也会有行号，与-b 的选项不同；
-T ：将 [tab] 按键以 ^I 显示出来；
-v ：列出一些看不出来的特殊字符
范例一：检阅 /etc/issue 这个档案的内容
[root@www ~]# cat /etc/issue
CentOS release 5.3 (Final)
Kernel \r on an \m
范例二：承上题，如果还要加印行号呢？
[root@www ~]# cat -n /etc/issue
 1 CentOS release 5.3 (Final)
 2 Kernel \r on an \m
 3
# 看到了吧！可以印出行号呢！这对亍大档案要找某个特定的行时，有点用处！
# 如果不想要编排空白行的行号，可以使用『cat -b /etc/issue』，自己测试看
看：
范例三：将 /etc/xinetd.conf 癿内容完整的显示出来(包含特殊字符)
[root@www ~]# cat -A /etc/xinetd.conf
#$
....(中间省略)....
```

```bash
less 文件（一般我使用这个），或者vim 文件
```

 空格键 ：向下翻劢一页； 

 [pagedown]：向下翻劢一页； 

 [pageup] ：向上翻劢一页； 

 /字符串 ：向下搜寻『字符串』的功能； 

 ?字符串 ：向上搜寻『字符串』的功能； 

 n ：重复前一个搜寻 (与 / 或 ? 有关！) 

 N ：反向癿重复前一个搜寻 (与 / 或 ? 有关！) 

 q ：离开 less 这个程序；

# od

```bash
[root@www ~]# od [-t TYPE] 档案
选项戒参数：
-t ：后面可以接各种『类型 (TYPE)』癿输出，例如：
 a ：利用默讣癿字符杢输出；
 c ：使用 ASCII 字符杢输出
 d[size] ：利用十迚制(decimal)杢输出数据，每个整数占用 size bytes ；
 f[size] ：利用浮点数(floating)杢输出数据，每个数占用 size bytes ；
 o[size] ：利用八迚制(octal)杢输出数据，每个整数占用 size bytes ；
 x[size] ：利用十六迚制(hexadecimal)杢输出数据，每个整数占用 size 
bytes ；
范例一：请将/usr/bin/passwd 癿内容使用 ASCII 方式杢展现！
[root@www ~]# od -t c /usr/bin/passwd
0000000 177 E L F 001 001 001 \0 \0 \0 \0 \0 \0 \0 \0 \0
```



# touch 文件







```bash
ll -l --time=atime  CMakeLists.txt
```

![image-20230130104222695](C:\Users\cao'yang'lin\AppData\Roaming\Typora\typora-user-images\image-20230130104222695.png)

# 默认权限与umask又关

![image-20230130111432461](C:\Users\cao'yang'lin\AppData\Roaming\Typora\typora-user-images\image-20230130111432461.png)



因为 umask 为 022 ，所以 user 并没有被拿掉任何权限，不过 group  与 others 的权限被拿掉了 2 (也就是 w 这个权限)，那么当使用者：

 建立档案时：(-rw-rw-rw-) - (-----w--w-) ==> -rw-r--r-- 

 建立目录时：(drwxrwxrwx) - (d----w--w-) ==> drwxr-xr-x

拿权限，有什么数字就默认拿什么权限

```bash
[root@www ~]# umask 002
[root@www ~]# touch test3
[root@www ~]# mkdir test4
[root@www ~]# ll
-rw-rw-r-- 1 root root 0 Sep 27 00:36 test3
drwxrwxr-x 2 root root 4096 Sep 27 00:36 test4
```

```bash
[root@www ~]# chattr [+-=][ASacdistu] 档案或目录名称
选项与参数：
+ ：增加某一个特殊参数，其他原本存在参数则不动。
- ：移除某一个特殊参数，其他原本存在参数则不动。
= ：设定一定，且仅有后面接的参数
A ：当设定了 A 这个属性时，若你有存取此档案(或目录)时，他的访问时间
atime
 将不会被修改，可避免 I/O 较慢的机器过度的存取磁盘。这对速度较慢的计
算机有帮助
S ：一般档案是异步写入磁盘的(原理请参考第五章 sync 的说明)，如果加上 S 
这个
 属性时，当你进行任何档案的修改，该更动会『同步』写入磁盘中。
a ：当设定 a 之后，这个档案将只能增加数据，而不能删除也不能修改数据，只
有 root
 才能设定这个属性。
c ：这个属性设定之后，将会自动的将此档案『压缩』，在读取的时候将会自动
解压缩，
 但是在储存的时候，将会先进行压缩后再储存(看来对于大档案似乎蛮有用
的！)
d ：当 dump 程序被执行的时候，设定 d 属性将可使该档案(或目录)不会被
dump 备份
i ：这个 i 可就很厉害了！他可以让一个档案『不能被删除、改名、设定连结也
无法
 写入或新增资料！』对于系统安全性有相当大的帮助！叧有 root 能设定此属
性
s ：当档案设定了 s 属性时，如果这个档案被删除，他将会被完全的移除出这个
硬盘
 空间，所以如果误删了，完全无法救回来了喔！
u ：不 s 相反的，当使用 u 来配置文件案时，如果该档案被删除了，则数据内容
其实还
 存在磁盘中，可以使用来救援该档案喔！
注意：属性设定常见的是 a 与 i 的设定值，而且很多设定值必须要身为 root 才
能设定
范例：请尝试到/tmp 底下建立档案，幵加入 i 癿参数，尝试删除看看。
[root@www ~]# cd /tmp
[root@www tmp]# touch attrtest <==建立一个空档案
[root@www tmp]# chattr +i attrtest <==给予 i 癿属性
[root@www tmp]# rm attrtest <==尝试删除看看
rm: remove write-protected regular empty file `attrtest'? y
rm: cannot remove `attrtest': Operation not permitted <==操作丌讲可
# 看到了吗？呼呼！连 root 也没有办法将这个档案删除呢！赶紧解除设定！
范例：请将该档案的 i 属性取消！
[root@www tmp]# chattr -i attrtest
```

# 显示隐藏档案属性

```bash
[root@www ~]# lsattr [-adR] 档案与目录
选项不参数：
-a ：将隐藏文件的属性也显示出来；
-d ：如果接的是目录，仅列出目录本身的属性而非目录内的文件名；
-R ：连同子目录的数据也一并列出来！
[root@www tmp]# chattr +aij attrtest
[root@www tmp]# lsattr attrtest
----ia---j--- attrtest
```

#  which (寻找『执行档』)

```bash
which ifconfig
```

![image-20230130115731773](C:\Users\cao'yang'lin\AppData\Roaming\Typora\typora-user-images\image-20230130115731773.png)

#  whereis (寻找特定档案)

![image-20230130120127784](C:\Users\cao'yang'lin\AppData\Roaming\Typora\typora-user-images\image-20230130120127784.png)

locate和whereis都是从数据库里面查找的，所以使用前要updatedb更新一下数据库

# find则是从硬盘里查找

```bash
[root@www ~]# find [PATH] [option] [action]
选项与参数：
1. 与时间有关的选项：共有 -atime, -ctime 与 -mtime ，以 -mtime 说明
 -mtime n ：n 为数字，意义为在 n 天之前的『一天之内』被更改过内容的档
案；
 -mtime +n ：列出在 n 天之前(不含 n 天本身)被更动过内容的档案档名；
 -mtime -n ：列出在 n 天之内(含 n 天本身)被更动过内容的档案档名。
 -newer file ：file 为一个存在的档案，列出比 file 还要新的档案档名
范例一：将过去系统上面 24 小时内有更动过内容 (mtime) 的档案列出
[root@www ~]# find / -mtime 0
# 那个 0 是重点！0 代表目前的时间，所以，从现在开始到 24 小时前，
# 有变动过内容的档案都会被列出来！那如果是三天前的 24 小时内？
# find / -mtime 3 有变动过的档案都被列出的意思！
范例二：寻找 /etc 底下的档案，如果档案日期比 /etc/passwd 新就列出
[root@www ~]# find /etc -newer /etc/passwd
# -newer 用在分辨两个档案之间的新旧关系是很有用的！
```

```bash
[root@www ~]# find / -name passwd
# 利用这个 -name 可以搜寻档名啊！
```

```
[root@www ~]# find / -size +1000k
# 虽然在 man page 提到可以使用 M 不 G 分别代表 MB 不 GB，
# 不过，俺即试不出来这个功能～所以，目前应该是仅支持到 c 不 k 吧！
```





![image-20230130150905932](C:\Users\cao'yang'lin\AppData\Roaming\Typora\typora-user-images\image-20230130150905932.png)

# gzip解压缩

```bash
范例二：由亍 man.config 是文本文件，请将范例一的压缩文件的内容读出来！
[root@www tmp]# zcat man.config.gz
# 由于 man.config 这个原本的档案是是文本文件，因此我们可以尝试使用 zcat 
去读取！
# 此时屏幕上会显示 man.config.gz 解压缩之后的档案内容！
范例三：将范例一的档案解压缩
[root@www tmp]# gzip -d man.config.gz
# 不要使用 gunzip 这个挃令，不好背！使用 gzip -d 来进行解压缩！
# 与 gzip 相反， gzip -d 会将原本的 .gz 删除，产生原本的 man.config 档案。
范例四：将范例三解开的 man.config 用最佳的压缩比压缩，并保留原本的档案
[root@www tmp]# gzip -9 -c man.config > man.config.gz
```

```bash
gzip -d man.config.gz
```

# tar

```bash
[root@www ~]# tar [-j|-z] [cv] [-f 建立的檔名] filename... <==打包与压缩
[root@www ~]# tar [-j|-z] [tv] [-f 建立的檔名] <==察看檔名
[root@www ~]# tar [-j|-z] [xv] [-f 建立的檔名] [-C 目录] <==解压缩
选顷与参数：
-c ：建立打包档案，可搭配 -v 来察看过程中被打包的档名(filename)
-t ：察看打包档案的内容含有哪些档名，重点在察看『档名』就是了；
-x ：解打包或解压缩的功能，可以搭配 -C (大写) 在特定目录解开
 特别留意癿是， -c, -t, -x 不可同时出现在一串挃令列中。
-j ：透过 bzip2 癿支持进行压缩/解压缩：此时档名最好为 *.tar.bz2
-z ：透过 gzip 的支持进行压缩/解压缩：此时档名最好为 *.tar.gz
-v ：在压缩/解压缩的过程中，将正在处理的文件名显示出来！
-f filename：-f 后面要立刻接要被处理的档名！建议 -f 单独写一个选顷啰！
-C 目录 ：这个选顷用在解压缩，若要在特定目录解压缩，可以使用这个选
顷。
其他后续练习会使用到的选顷介绍：
-p ：保留备份数据的原本权限不属性，常用亍备份(-c)重要癿配置文件
-P ：保留绝对路径，亦即允讲备份数据中吨有根目录存在乊意；
--exclude=FILE：在压缩癿过程中，丌要将 FILE 打包！

```

 压 缩：tar -jcv -f filename.tar.bz2 要被压缩的档案或目录名称

 查 询：tar -jtv -f filename.tar.bz2 

 解压缩：tar -jxv -f filename.tar.bz2 -C 欲解压缩的目录

1.压缩：

　　tar -zcvf /home/xahot.tar.gz /xahot

例子：把/xahot文件夹打包后生成一个/home/xahot.tar.gz的文件

```bash
tar -zcvf /home/xahot.tar.gz /xahot
```

2.解压：

　　tar -xvf /tmp/etc.tar    

```bash
tar -xvf /tmp/etc.tar
```

```
  进入文件：vim /etc/profile      
  输入i进入编辑模式，在下面插入
  export JAVA_HOME=/usr/local/jdk-11.0.8
  export CLASSPATH=.:$JAVA_HOME/jre/lib:$JAVA_HOME/lib:$JAVA_HOME/lib/tools.jar
  export PATH=$PATH:$JAVA_HOME/bin:$JAVA_HOME/jre/bin
```

# vim的使用

u 复原前一个动作。(常用) 这个要按了esc之后才能使用，除开编辑模式使用

[Ctrl]+r 重做上一个动作。(常用)

yy 复制游标所在的那一行(常用)

/word 向光标之下寻找一个名称为 word 的字符串。例如要在档案内搜寻 vbird 这个字符串，就输入 /vbird 即可！ (常用)

:1,$s/word1/word2/g 从第一行到最后一行寻找 word1 字符串，并将该字符串取代为 word2 ！(常用)

gg 移动到这个档案的第一行，相当亍 1G 啊！ (常用)

G 移动到这个档案的最后一行(常用)

n+<enter> 为数字。光标向下移动 n 行(常用)

# 同时编辑两个文件

vim     1.txt     2.txt

:files查看文件个

:n 移动到下一个文件

![image-20230130222336474](C:\Users\cao'yang'lin\AppData\Roaming\Typora\typora-user-images\image-20230130222336474.png)

# 安装java

```bash
yum -y install java-11.0.8-openjdk* 。

#手动安装
tar -zxvf jdk-8u202-linux-x64.tar.gz
#这是java的bin目录，接下来，我们配置环境变量
/root/java/jdk1.8.0_202/bin
#jdk1.8.0_241环境变量
export JAVA_HOME=/root/java/jdk1.8.0_202
export PATH=$PATH:$JAVA_HOME/bin
export CLASSPATH=.:$JAVA_HIOME/jre/lib/rt.jar:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar
[root@localhost java]# source /etc/profile

```

# 成功安装java

```java
[root@hecs-218409 etc]# source profile
[root@hecs-218409 etc]# java -version
java version "1.8.0_202"
Java(TM) SE Runtime Environment (build 1.8.0_202-b08)
Java HotSpot(TM) 64-Bit Server VM (build 25.202-b08, mixed mode)

```

# 安装mysql

```bash
yum install -y mysql
```

# 查找java和mysql的位置

```bash
find / -name "java"
```

```
:wq!     :wq
```

\1. 你的 Linux 系统默认支持癿语系数据：这不 /etc/sysconfig/i18n 有关； 2. 你的终端界面 (bash) 的语系： 这不 LANG 这个变数有关； 3. 你的档案原本的编码； 4. 开吪终端机的软件，例如在 GNOME 底下的窗口接口。





# tab键命令补全

![image-20230130225854072](C:\Users\cao'yang'lin\AppData\Roaming\Typora\typora-user-images\image-20230130225854072.png)

# 指令取别名，和删除别名

```bash
alias lm='ls -al'
unalias lm
```



# linux的复制与粘贴

用鼠标选中即是复制。. 　　单击鼠标滚轮即为粘贴。.

# linux执行文件

```bash
./sh01.sh
sh sh01.sh
```

当前目录的什么文件。

# bash第一个Helloworld

```bash
echo -e "Hello World! \a \n"
```

#  vim 会有额外的语法检验机制

安装Linux时，默认分为三个区，分别是/boot分区、根分区和[swap分区](https://baike.baidu.com/item/swap分区/7613378?fromModule=lemma_inlink).这三个分区分别对应的盘符是hda1、hda2、hda3。

- **sda1 解释 sd代表是scsi硬盘 a代表是第一块硬盘 1代表是第一个主分区**
- sdb1 解释 sd代表是scsi硬盘 b代表是第二块硬盘 1代表是第一个主分区**

# echo取出变量，输出变量值

```bash
[root@www ~]# echo $variable
[root@www ~]# echo $PATH
/usr/local/sbin:/usr/local/bin:/sbin:/bin:/usr/sbin:/usr/bin:/root/bin
[root@www ~]# echo ${PATH}
```

```bash
[root@www ~]# myname=VBird   //设置变量


[root@www ~]# unset str; var=${str=newvar}
[root@www ~]# echo var="$var", str="$str"
var=newvar, str=newvar <==因为 str 丌存在，所以 var/str 均为 newvar

[root@www ~]# str="oldvar"; var=${str=newvar}//不存在才可以这样赋值，都是局部变量
[root@www ~]# echo var="$var", str="$str"
var=oldvar, str=oldvar <==因为 str 存在，所以 var 等于 str 的内容

[root@www ~]# echo $myname   //输出变量
VBird <==出现了！因为这个变量已经被设定了！
```

```bash
双引号内的特殊字符如 $ 等，可以保有原本的特性，如下所示：
『var="lang is $LANG"』则『echo $var』可得『lang is en_US』
单引号内的特殊字符则仅为一般字符 (纯文本)，如下所示：
『var='lang is $LANG'』则『echo $var』可得『lang is $LANG』
\逃脱字符  ，可以使特殊符号失效
```

![image-20230131134925048](C:\Users\cao'yang'lin\AppData\Roaming\Typora\typora-user-images\image-20230131134925048.png)

![image-20230131135210182](C:\Users\cao'yang'lin\AppData\Roaming\Typora\typora-user-images\image-20230131135210182.png)

# 取消变量的方法为使用 unset ：『unset 变量名称』例如取消 myname 的设定： 『unset myname』

![image-20230131135706855](C:\Users\cao'yang'lin\AppData\Roaming\Typora\typora-user-images\image-20230131135706855.png)

```bash
unset id
#添加
id="$PATH":/HOME/BIN
```

![image-20230131140423666](C:\Users\cao'yang'lin\AppData\Roaming\Typora\typora-user-images\image-20230131140423666.png)

```bash
范例一：设定一发量 name ，且内容为 VBird
[root@www ~]# 12name=VBird
-bash: 12name=VBird: command not found <==屏幕会显示错诨！因为不
能以数字开头！
[root@www ~]# name = VBird <==还是错诨！因为有空白！
[root@www ~]# name=VBird <==OK 的啦！
范例二：承上题，若变量内容为 VBird's name 呢，就是发量内容含有特殊符号
时：
[root@www ~]# name=VBird's name 
# 单引号不双引号必须要成对，在上面的设定中仅有一个单引号，因此当你按下
enter 后，
# 你还可以继续输入变量内容。这与我们所需要癿功能不同，失败啦！
# 记得，失败后要复原请按下 [ctrl]-c 结束！
[root@www ~]# name="VBird's name" <==OK 的啦！
# 指令是由左边向右找→，先遇到的引号先有用，因此如上所示，单引号会失
效！
[root@www ~]# name='VBird's name' <==失败的啦！
# 因为前两个单引号已成对，后面就多了一个不成对的单引号了！因此也就失败
了！
[root@www ~]# name=VBird\'s\ name <==OK 的啦！
# 利用反斜杠 (\) 跳脱特殊字符，例如单引号与空格键，这也是 OK 的啦！
范例三：我要在 PATH 这个发量当中『累加』:/home/dmtsai/bin 这个目录
[root@www ~]# PATH=$PATH:/home/dmtsai/bin
[root@www ~]# PATH="$PATH":/home/dmtsai/bin
[root@www ~]# PATH=${PATH}:/home/dmtsai/bin
# 上面这三种格式在 PATH 里头的设定都是 OK 的！但是底下的例子就不见得
啰！
范例四：呈范例三，我要将 name 的内容多出 "yes" 呢？
[root@www ~]# name=$nameyes 
# 知道了吧？如果没有双引号，那么发量成了啥？name 癿内容是 $nameyes 这
个变量！
# 呵呵！我们可没有设定过 nameyes 这个变量吶！所以，应该是底下这样才
对！
[root@www ~]# name="$name"yes
[root@www ~]# name=${name}yes <==以此例较佳！
范例五：如何让我刚刚设定的 name=VBird 可以用在下个 shell 的程序？
[root@www ~]# name=VBird
[root@www ~]# bash <==进入到所谓的子程序
[root@www ~]# echo $name <==子程序：再次的 echo 一下；
 <==嘿嘿！幵没有刚刚设定的内容喔！
[root@www ~]# exit <==子程序：离开这个子程序
[root@www ~]# export name
[root@www ~]# bash <==进入到所谓的子程序
[root@www ~]# echo $name <==子程序：在此执行！
VBird <==看吧！出现设定值了！
[root@www ~]# exit <==子程序：离开这个子程序
```

```
环境发量的功能
环境发量可以帮我们达到很多功能～包括家目录的发换啊、提示字符的显示啊、执行文件搜寻的路径啊
等等的， 还有很多很多啦！那么，既然环境变量有那么多的功能，问一下，目前我的 shell 环境中， 有
多少默认的环境变量啊？我们可以利用两个指令来查阅，分别是 env 与 export 呢！
```

![image-20230131170047880](C:\Users\cao'yang'lin\AppData\Roaming\Typora\typora-user-images\image-20230131170047880.png)

![image-20230131170104230](C:\Users\cao'yang'lin\AppData\Roaming\Typora\typora-user-images\image-20230131170104230.png)

# ？可以说是判断符（判断变量存不存在）

```bash
那如果我叧是想知道，如果旧变量不存在时，整个测试就告知我『有错误』，此时就能够使用问号 『 ? 』的帮忙啦！ 底下这个测试练习一下先！ 测试：若 str 不存在时，则 var 的测试结果直接显示 "无此变量" [root@www ~]# unset str; var=${str?无此变量} -bash: str: 无此变量 <==因为 str 不存在，所以输出错误信息
```



```bash
测试：若 str 不存在时，则 var 的测试结果直接显示 "无此变量"
[root@www ~]# unset str; var=${str?无此发数}
-bash: str: 无此变量 <==因为 str 不存在，所以输出错误讯息


测试：若 str 存在时，则 var 癿内容会不 str 相同！
[root@www ~]# str="oldvar"; var=${str?novar}
[root@www ~]# echo var="$var", str="$str"
var=oldvar, str=oldvar <==因为 str 存在，所以 var 等于 str 的内容
```

# history指令

```bash
[root@www ~]# history [n]
[root@www ~]# history [-c]
[root@www ~]# history [-raw] histfiles
选项不参数：
n ：数字，意思是『要列出最近的 n 笔命令行表』的意思！
-c ：将目前的 shell 中的所有 history 内容全部消除
-a ：将目前新增的 history 指令新增入 histfiles 中，若没有加 histfiles ，
 则预设写入 ~/.bash_history
-r ：将 histfiles 的内容读到目前这个 shell 的 history 记忆中；
-w ：将目前的 history 记忆内容写入 histfiles 中！
范例一：列出目前内存内的所有 history 记忆
[root@www ~]# history
# 前面省略
1017 man bash
1018 ll
1019 history
1020 history
# 列出的信息当中，共分两栏，第一栏为该指令在这个 shell 当中的代码，
# 另一个则是指令本身的内容喔！至于会秀出几笔指令记录，则与 HISTSIZE 有
关！
范例二：列出目前最近的 3 笔资料
[root@www ~]# history 3
1019 history
1020 history
1021 history 3
范例三：立刻将目前的资料写入 histfile 当中
[root@www ~]# history -w
# 在默讣的情况下，会将历史记录写入 ~/.bash_history 当中！
[root@www ~]# echo $HISTSIZE
1000
```

# 利用history来执行命令

```bash
[root@www ~]# !number
[root@www ~]# !command
[root@www ~]# !!
选项不参数：
number ：执行第几笔指令的意思；
command ：由最近的指令向前搜寻『指令串开头为 command』的那个指令，
幵执行；
!! ：就是执行上一个指令(相当于按↑按键后，按 Enter)
[root@www ~]# history
 66 man rm
 67 alias
 68 man history
 69 history
[root@www ~]# !66 <==执行第 66 笔指令
[root@www ~]# !! <==执行上一个指令，本例中亦即 !66
[root@www ~]# !al <==执行最近以 al 为开头的指令(上头列出的第 67 个)

```

# issue内的各代码意义（编辑用户进Linux系统的开机信息）

# bash 的进站与欢迎讯息： /etc/issue, /etc/motd

![image-20230131230044651](C:\Users\cao'yang'lin\AppData\Roaming\Typora\typora-user-images\image-20230131230044651.png)

![image-20230131230649973](C:\Users\cao'yang'lin\AppData\Roaming\Typora\typora-user-images\image-20230131230649973.png)

![image-20230131230551662](C:\Users\cao'yang'lin\AppData\Roaming\Typora\typora-user-images\image-20230131230551662.png)

# bash的子程序理解

Linux 里面登录之后取得 一个 bash 后这是父程序，

在这个bash环境运行里面运行另外一个bash 那么 在这个新的bash环境下面运行的程序就是子程序了

登录Linux的时候是login shell ，子程序不需要输入密码的时候是non-login shell

bash 环境配置文件主要分为哪两种类型的读取？分别读取哪些重要档案？

 (1)login shell：主要读取 /etc/profile 及 ~/.bash_profile

 (2)non-logni shell：主要读取 ~/.bashrc 而已。

# bash的环境配置文件

![image-20230131230943631](C:\Users\cao'yang'lin\AppData\Roaming\Typora\typora-user-images\image-20230131230943631.png)

# 连续命令中， ;, &&, || 有何不同？

分号可以让两个 command 连续运作，不考虑 command1 的输出状态， && 则前一个指令必 需要没有错误讯息，亦即回传值需为 0 则 command2 才会被执行， || 则与 && 相反！

如何秀出在 /bin 底下任何以 a 为开头的档案文件名的详细资料？ 

ls -l /bin/a* 

 如何秀出 /bin 底下，文件名为四个字符的档案？ 

ls -l /bin/???? 

 如何秀出 /bin 底下，档名开头不是 a-d 的档案？ 

ls -l /bin/[^a-d]



# cut命令

![image-20230201103345969](C:\Users\cao'yang'lin\AppData\Roaming\Typora\typora-user-images\image-20230201103345969.png)

```bash
[root@moli_linux1 ~]$ echo "abcde12345" | cut -b 1-5,10
abcde5

[root@www ~]# echo $PATH | cut -d ':' -f 5
# 如同上面的数字显示，我们是以『 : 』作为分割符，因此会出现 /usr/local/bin
# 那么如果想要列出第 3 不第 5 呢？，就是这样：
[root@www ~]# echo $PATH | cut -d ':' -f 3,5
范例二：将 export 输出的讯息，取得第 12 字符以后的所有字符串
[root@www ~]# export
declare -x HISTSIZE="1000"
declare -x INPUTRC="/etc/inputrc"
declare -x KDEDIR="/usr"
declare -x LANG="zh_TW.big5"
.....(其他省略).....
# 注意看，每个数据都是排列整齐的输出！如果我们不想要『 declare -x 』时，
# 就得这么做：
[root@www ~]# export | cut -c 12-
HISTSIZE="1000"
INPUTRC="/etc/inputrc"
KDEDIR="/usr"
LANG="zh_TW.big5"
.....(其他省略).....
# 知道怎么回事了吧？用 -c 可以处理比较具有格式的输出数据！
# 我们还可以挃定某个范围的值，例如第 12-20 的字符，就是 cut -c 12-20 等
等！
范例三：用 last 将显示的登入者的信息中，仅留下用户大名
[root@www ~]# last
root pts/1 192.168.201.101 Sat Feb 7 12:35 still logged in
root pts/1 192.168.201.101 Fri Feb 6 12:13 - 18:46 (06:33)
root pts/1 192.168.201.254 Thu Feb 5 22:37 - 23:53 (01:16)
# last 可以输出『账号/终端机/杢源/日期时间』的数据，并且是排列整齐的
[root@www ~]# last | cut -d ' ' -f 1
# 由输出的结果我们可以収现第一个空白分隑癿字段代表账号，所以使用如上挃
令：
# 但是因为 root pts/1 之间空格有好几个，并非仅有一个，所以，如果要找出
# pts/1 其实不能以 cut -d ' ' -f 1,2 喔！输出的结果会不是我们想要的。
```

# **“| ”管道符用法**

上一条命令的输出，作为下一条命令参数

方式：command1 | command2

Linux所提供的管道符“|”将两个命令隔开，管道符左边命令的输出就会作为管道符右边命令的输入。连续使用管道意味着第一个命令的输出会作为 第二个命令的输入，第二个命令的输出又会作为第三个命令的输入，依此类推

# grep指令

```bash
[root@www ~]# grep [-acinv] [--color=auto] '搜寻字符串' filename
选项与参数：
-a ：将 binary 档案以 text 档案的方式搜寻数据
-c ：计算找到 '搜寻字符串' 的次数
-i ：忽略大小写的不同，所以大小写视为相同
-n ：顺便输出行号
-v ：反向选择，亦即显示出没有 '搜寻字符串' 内容的那一行！
--color=auto ：可以将找到的关键词部分加上颜色的显示喔！
范例一：将 last 当中，有出现 root 的那一行就取出来；
[root@www ~]# last | grep 'root'
范例二：不范例一相反，只要没有 root 的就取出！
[root@www ~]# last | grep -v 'root'
范例三：在 last 的输出讯息中，只要有 root 就取出，并且仅取第一栏
[root@www ~]# last | grep 'root' |cut -d ' ' -f1
# 在取出 root 之后，利用上个指令 cut 的处理，就能够仅取得第一栏啰！
范例四：取出 /etc/man.config 内含 MANPATH 的那几行
[root@www ~]# grep --color=auto 'MANPATH' /etc/man.config
....(前面省略)....
MANPATH_MAP /usr/X11R6/bin /usr/X11R6/man
MANPATH_MAP /usr/bin/X11 /usr/X11R6/man
MANPATH_MAP /usr/bin/mh /usr/share/man
# 神奇的是，如果加上 --color=auto 的选项，找到的关键词部分会用特殊颜色
显示喔！

```

# last命令

Linux last 命令用于显示用户最近登录信息。

单独执行 **last** 指令，它会读取位于 /var/log/目录下，名称为 wtmp 的文件，并把该文件记录登录的用户名，全部显示出来









# sort命令

```bash
[root@www ~]# sort [-fbMnrtuk] [file or stdin]
选项与参数：
-f ：忽略大小写的差异，例如 A 不 a 规为编码相同；
-b ：忽略最前面的空格符部分；
-M ：以月份的名字来排序，例如 JAN, DEC 等等的排序方法；
-n ：使用『纯数字』进行排序(默认是以文字型态来排序的)；
-r ：反向排序；
-u ：就是 uniq ，相同癿数据中，仅出现一行代表；
-t ：分割符，预设是用 [tab] 键来分割；
-k ：以那个区间 (field) 来进行排序的意思
范例一：个人账号都记录在 /etc/passwd 下，请将账号进行排序。
[root@www ~]# cat /etc/passwd | sort
adm:x:3:4:adm:/var/adm:/sbin/nologin
apache:x:48:48:Apache:/var/www:/sbin/nologin
bin:x:1:1:bin:/bin:/sbin/nologin
daemon:x:2:2:daemon:/sbin:/sbin/nologin
# 鸟哥省略很多的输出～由上面的数据看起来， sort 是预设『以第一个』数据杢
排序，
# 而且默讣是以『文字』型态杢排序的喔！所以由 a 开始排到最后啰！
范例二：/etc/passwd 内容是以 : 来分割的，我想以第三栏来排序，该如何？
[root@www ~]# cat /etc/passwd | sort -t ':' -k 3
root:x:0:0:root:/root:/bin/bash
uucp:x:10:14:uucp:/var/spool/uucp:/sbin/nologin
operator:x:11:0:operator:/root:/sbin/nologin
bin:x:1:1:bin:/bin:/sbin/nologin
games:x:12:100:games:/usr/games:/sbin/nologin
# 看到特殊字体的输出部分了吧？怎么会这样排列啊？呵呵！没错啦～
# 如果是以文字型态来排序的话，原本就会是这样，想要使用数字排序：
# cat /etc/passwd | sort -t ':' -k 3 -n
# 这样才行啊！用那个 -n 来告知 sort 以数字来排序啊！
范例三：刟用 last ，将输出癿数据仅取账号，并加以排序
[root@www ~]# last | cut -d ' ' -f1 | sort
```

从小到大，升序

# rpm安装

```bash
[root@www ~]# rpm -ivh package_name
选项与参数：
-i ：install 的意思
-v ：察看更细部的安装信息画面
-h ：以安装信息列显示安装进度
范例一：安装 rp-pppoe-3.5-32.1.i386.rpm
[root@www ~]# rpm -ivh rp-pppoe-3.5-32.1.i386.rpm
Preparing... ####################################### [100%]
 1:rp-pppoe ####################################### 
[100%]
范例二、一口气安装两个以上的软件时：
[root@www ~]# rpm -ivh a.i386.rpm b.i386.rpm *.rpm
# 后面直接接上许多的软件档案！
范例三、直接由网络上面的某个档案安装，以网址来安装：
[root@www ~]# rpm -ivh http://website.name/path/pkgname.rpm
```

# RPM 升级与更新 (upgrade/freshen)

-Uvh 后面接的软件即使没有安装过，则系统将予以直接安装； 

若后面接的软件有安装过旧版，则系统自动更新至新版；

-Fvh 如果后面接的软件不未安装到你的 Linux 系统上，则该软件不会被安装；

亦即只有已安装至你 Linux 系统内的软件会 被『升级』！

# RPM 查询 (query)

```
[root@www ~]# rpm -qa <==已安装软件
[root@www ~]# rpm -q[licdR] 已安装的软件名称 <==已安装软件
[root@www ~]# rpm -qf 存在于系统上面的某个文件名 <==已安装软件
[root@www ~]# rpm -qp[licdR] 未安装的某个文件名 <==查阅 RPM 档案
选项不参数：
查询已安装软件的信息：
-q ：仅查询，后面接的软件名称是否有安装；
-qa ：列出所有的，已经安装在本机 Linux 系统上面的所有软件名称；
-qi ：列出该软件的详细信息 (information)，包含开发商、版本不说明等；
-ql ：列出该软件所有的档案与目录所在完整文件名 (list)；
-qc ：列出该软件的所有配置文件 (找出在 /etc/ 底下的檔名而已)
-qd ：列出该软件的所有说明文件 (找出与 man 有关的档案而已)
-qR ：列出与该软件有关的相依软件所含的档案 (Required 的意思)
-qf ：由后面接的文件名，找出该档案属于哪一个已安装的软件；
查询某个 RPM 档案内含有的信息：
-qp[icdlR]：注意 -qp 后面接的所有参数以上面的说明一致。但用途仅在于找出
 某个 RPM 档案内的信息，而非已安装的软件信息！注意！
```

# RPM 反安装与重建数据库 (erase/rebuilddb)

```bash
[root@www ~]# rpm --rebuilddb <==重建数据库

# 2. 若仅移除 pam-devel 这个之前范例安装上的软件呢？
[root@www ~]# rpm -e pam-devel <==不会出现任何讯息！
```

从范例一我们知道 pam 所提供的函数库是让非常多其他软件使用的，因此你不能移除 pam ，除非将其他相依软件一口气也全部移 除！你当然也能加 --nodeps 来强制移除， 不过，如此一来所有会用到 pam函数库的软件，都将成为无法运作的程序，我想，你的 主机也只好准备停机休假了吧！ 至于范例二中，由于 pam-devel 是依附亍 pam 的开发工具，你可以单独安装与单独移除啦！

比如说：

```bash
[root@localhost ~]# rpm -e icedtea-web-1.7.1-4.el7_9.x86_64
[root@localhost ~]# rpm -Va
```

# yum安装与升级

```bash
yum install pam-devel
yum update pam-devel
yum update
```

```bash
[root@www ~]# yum [option] [查询工作项目] [相关参数]
选项不参数：
 install ：后面接要安装的软件！
 update ：后面接要升级的软件，若要整个系统都升级，就直接 update 即可
范例一：将前一个练习找到的未安装的 pam-devel 安装起来
[root@www ~]# yum install pam-devel
Setting up Install Process
Parsing package install arguments
Resolving Dependencies <==先检查软件的属性相依问题
--> Running transaction check
---> Package pam-devel.i386 0:0.99.6.2-4.el5 set to be updated
--> Processing Dependency: pam = 0.99.6.2-4.el5 for package: pam-devel
--> Running transaction check
---> Package pam.i386 0:0.99.6.2-4.el5 set to be updated
filelists.xml.gz 100% |=========================| 1.6 MB 00:05
filelists.xml.gz 100% |=========================| 138 kB 00:00
-> Finished Dependency Resolution
Dependencies Resolved
=============================================================================
Package Arch Version Repository Size
=============================================================================
Installing:
pam-devel i386 0.99.6.2-4.el5 base 186 k
Updating:
pam i386 0.99.6.2-4.el5 base 965 k
Transaction Summary
=============================================================================
Install 1 Package(s) <==结果发现要安装此软件需要升级另一个相依的软件
Update 1 Package(s)
Remove 0 Package(s)
Total download size: 1.1 M
Is this ok [y/N]: y <==确定要安装！
Downloading Packages: <==先下载！
(1/2): pam-0.99.6.2-4.el5 100% |=========================| 965 kB 00:05
(2/2): pam-devel-0.99.6.2 100% |=========================| 186 kB 00:01
Running rpm_check_debug
Running Transaction Test
Finished Transaction Test
Transaction Test Succeeded
Running Transaction <==开始安装！
 Updating : pam ######################### [1/3]
 Installing: pam-devel ######################### [2/3]
 Cleanup : pam ######################### [3/3]
Installed: pam-devel.i386 0:0.99.6.2-4.el5
Updated: pam.i386 0:0.99.6.2-4.el5
Complete!
```

# yum查询

```bash
[root@www ~]# yum [option] [查询工作项目] [相关参数]
选项与参数：
[option]：主要的选项，包括有：
 -y ：当 yum 要等待用户输入时，这个选项可以自动提供 yes 的响应；
 --installroot=/some/path ：将该软件安装在 /some/path 而不使用默认路径
[查询工作项目] [相关参数]：这方面的参数有：
 search ：搜寻某个软件名称或者是描述 (description) 的重要关键字；
 list ：列出目前 yum 所管理的所有的软件名称与版本，有点类似 rpm -qa；
 info ：同上，不过有点类似 rpm -qai 的执行结果；
 provides：从档案去搜寻软件！类似 rpm -qf 的功能！
范例一：搜寻磁盘阵列 (raid) 相关的软件有哪些？
[root@www ~]# yum search raid
....(前面省略)....
mdadm.i386 : mdadm controls Linux md devices (software RAID arrays)
lvm2.i386 : Userland logical volume management tools
....(后面省略)....
# 在冒号 (:) 左边的是软件名称，史边的则是在 RPM 内的 name 设定 (软件名)
# 瞧！上面的结果，这不就是与 RAID 有关的软件吗？如果想了解 mdadm 的软
件内容呢？
范例二：找出 mdadm 这个软件的功能为何
[root@www ~]# yum info mdadm
Installed Packages <==这说明该软件是已经安装的了
Name : mdadm <==这个软件的名称
Arch : i386 <==这个软件的编译架构
Version: 2.6.4 <==此软件的版本
Release: 1.el5 <==释出的版本
Size : 1.7 M <==此软件的档案总容量
Repo : installed <==容器回报说已安装的
Summary: mdadm controls Linux md devices (software RAID arrays)
Description: <==看到否？这就是 rpm -qi 嘛！
mdadm is used to create, manage, and monitor Linux MD (software RAID)
devices. As such, it provides similar functionality to the raidtools
package. However, mdadm is a single program, and it can perform
almost all functions without a configuration file, though a configuration
file can be used to help with some common tasks.
# 不要跟我说，上面说些啥？自己找字典翻一翻吧！拜托拜托！
范例三：列出 yum 服务器上面提供的所有软件名称
[root@www ~]# yum list
Installed Packages <==已安装软件
Deployment_Guide-en-US.noarch 5.2-9.el5.centos installed
Deployment_Guide-zh-CN.noarch 5.2-9.el5.centos installed
Deployment_Guide-zh-TW.noarch 5.2-9.el5.centos installed
....(中间省略)....
Available Packages <==还可以安装的其他软件
Cluster_Administration-as-IN.noarch 5.2-1.el5.centos base
Cluster_Administration-bn-IN.noarch 5.2-1.el5.centos base
....(底下省略)....
# 上面提供的意义为：『 软件名称 版本 在那个容器内 』
范例四：列出目前朋务器上可供本机进行升级的软件有哪些？
[root@www ~]# yum list updates <==一定要是 updates 喔！
Updated Packages
Deployment_Guide-en-US.noarch 5.2-11.el5.centos base
Deployment_Guide-zh-CN.noarch 5.2-11.el5.centos base
Deployment_Guide-zh-TW.noarch 5.2-11.el5.centos base
....(底下省略)....
# 上面就列出在那个容器内可以提供升级的软件与版本！
范例五：列出提供 passwd 这个档案的软件有哪些
[root@www ~]# yum provides passwd
passwd.i386 : The passwd utility for setting/changing passwords using 
PAM
passwd.i386 : The passwd utility for setting/changing passwords using 
PAM
# 找到啦！就是上面的这个软件提供了 passwd 这个程序！
```

# yum卸载

```bash
[root@www ~]# yum remove pam-devel
Setting up Remove Process
Resolving Dependencies <==同样的，先解决属性相依的问题
--> Running transaction check
---> Package pam-devel.i386 0:0.99.6.2-4.el5 set to be erased
--> Finished Dependency Resolution
Dependencies Resolved
=============================================================================
Package Arch Version Repository Size
=============================================================================
Removing:
pam-devel i386 0.99.6.2-4.el5 installed 495 k
Transaction Summary
=============================================================================
Install 0 Package(s)
Update 0 Package(s)
Remove 1 Package(s) <==还好，幵没有属性相依的问题，单纯移除一个软件
Is this ok [y/N]: y
Downloading Packages:
Running rpm_check_debug
Running Transaction Test
Finished Transaction Test
Transaction Test Succeeded
Running Transaction
 Erasing : pam-devel ######################### [1/1]
Removed: pam-devel.i386 0:0.99.6.2-4.el5
Complete!
```

# yum容器

base容器

```bash
[root@www ~]# vi /etc/yum.repos.d/CentOS-Base.repo
[base]
name=CentOS-$releasever - Base
baseurl=http://ftp.twaren.net/Linux/CentOS/5/os/i386/ #这个网站不要信   #我们使用的是alic的就是阿里的
gpgcheck=1
gpgkey=http://mirror.centos.org/centos/RPM-GPG-KEY-CentOS-5
# 底下其他的容器项目，请自行到高速网络中心去查询后自己处理！
```

 [base]：代表容器的名字！中刮号一定要存在，里面的名称则可以随意取。但是不能有两个相同的容器名称， 否则 yum 会不 晓得该到哪里去找容器相关软件列表档案。 

 name：只是说明一下这个容器的意义而已，重要性不高！ 

 mirrorlist=：列出这个容器可以使用的映射站台，如果不想使用，可以批注到这行； 

 baseurl=：这个最重要，因为后面接的就是容器的实际网址！ mirrorlist 是由 yum 程序自行去捉映像站台， baseurl 则是指定固定的一个容器网址！我们刚刚找到的网址放到这里来啦！ 

 enable=1：就是让这个容器被启劢。如果不想启动可以使用 enable=0 喔！ 

 gpgcheck=1：还记得 RPM 的数字签名吗？这就是指定是否需要查阅 RPM 档案内的数字签名！ 

 gpgkey=：就是数字签名的公钥文件所在位置！使用默认值即可

# 列出yum的所有容器

```bash
yum repolist all
```

![image-20230202110150676](C:\Users\cao'yang'lin\AppData\Roaming\Typora\typora-user-images\image-20230202110150676.png)

一个文件里面可能有很多的容器，在里面base是一个容器，updates是一个容器，extras也是一个容器

![image-20230202110400543](C:\Users\cao'yang'lin\AppData\Roaming\Typora\typora-user-images\image-20230202110400543.png)

# yum清除所有容器

```bash
[root@www ~]# yum clean [packages|headers|all]
选项与参数：
packages：将已下载的软件档案删除
headers ：将下载的软件文件头删除
all ：将所有容器数据都删除！
范例一：删除已下载过的所有容器的相关数据 (含软件本身与列表)
[root@www ~]# yum clean all
```

# 全系统自动升级

```bash
[root@www ~]# vim /etc/crontab
....(前面省略幵保留设定值)....
0 3 * * * root /usr/bin/yum -y update
```

# 容器的概念

简单来说，容器提供的是一种基于各种 Linux 发行版创建容器镜像的方法、一套管理容器生命周期的 API、与该 API 交互的客户端工具、保存快照的功能、在宿主机之间迁移容器实例的能力，等等。

![image-20230203103331309](C:\Users\cao'yang'lin\AppData\Roaming\Typora\typora-user-images\image-20230203103331309.png)

# **二、容器技术的特点**

容器的特点其实我们拿跟它跟硬件抽象层虚拟化hypervisor技术对比就清楚了，我们之前也提到过，传统的虚拟化（虚拟机）技术，创建环境和部署应用都很麻烦，而且应用的移植性也很繁琐，比如你要把vmware里的虚拟机迁移到KVM里就很繁琐（需要做镜像格式的转换）。那么有了容器技术就简单了，总结下容器技术主要有三个特点：

- \1. 极其轻量：只打包了必要的Bin/Lib；
- \2. 秒级部署：根据镜像的不同，容器的部署大概在毫秒与秒之间（比虚拟机强很多）；
- \3. 易于移植：一次构建，随处部署；
- \4. 弹性伸缩：Kubernetes、Swam、Mesos这类开源、方便、好使的容器管理平台有着非常强大的弹性管理能力。

# Linux sudo命令

Linux sudo命令以系统管理者的身份执行指令，也就是说，经由 sudo 所执行的指令就好像是 root 亲自执行。

# printf

```bash
printf 'hhh\n'
```

![image-20230203110822189](C:\Users\cao'yang'lin\AppData\Roaming\Typora\typora-user-images\image-20230203110822189.png)



```bash
#!/bin/bash
# author:菜鸟教程
# url:www.runoob.com
 
# format-string为双引号
printf "%d %s\n" 1 "abc"

# 单引号与双引号效果一样
printf '%d %s\n' 1 "abc"

# 没有引号也可以输出
printf %s abcdef

# 格式只指定了一个参数，但多出的参数仍然会按照该格式输出，format-string 被重用
printf %s abc def

printf "%s\n" abc def

printf "%s %s %s\n" a b c d e f g h i j

# 如果没有 arguments，那么 %s 用NULL代替，%d 用 0 代替
printf "%s and %d \n"
```

# test   （返回一个Boolean类型）

```bash
num1=100
num2=100
if test $[num1] -eq $[num2]
then
    echo '两个数相等！'
else
    echo '两个数不相等！'
fi
```

| -e 文件名 | 如果文件存在则为真                   |
| --------- | ------------------------------------ |
| -r 文件名 | 如果文件存在且可读则为真             |
| -w 文件名 | 如果文件存在且可写则为真             |
| -x 文件名 | 如果文件存在且可执行则为真           |
| -s 文件名 | 如果文件存在且至少有一个字符则为真   |
| -d 文件名 | 如果文件存在且为目录则为真           |
| -f 文件名 | 如果文件存在且为普通文件则为真       |
| -c 文件名 | 如果文件存在且为字符型特殊文件则为真 |
| -b 文件名 | 如果文件存在且为块特殊文件则为真     |



# 代码中的 **[]** 执行基本的算数运算，如：

## 实例

```bash
#!/bin/bash*

a=5
b=6

result=$**[**a+b**]** *# 注意等号两边不能有空格*
**echo** "result 为： $result"
```

结果为:

```bash
result 为： 11
```

# if else流

### fi

if 语句语法格式：

```bash
if condition
then
    command1 
    command2
    ...
    commandN 
fi
```

写成一行（适用于终端命令提示符）：

```bash
if [ $(ps -ef | grep -c "ssh") -gt 1 ]; then echo "true"; fi
```

末尾的 **fi** 就是 **if** 倒过来拼写，后面还会遇到类似的。

### if else

if else 语法格式：

```bash
if condition
then
    command1 
    command2
    ...
    commandN
else
    command
fi
```

### if else-if else

if else-if else 语法格式：

```bash
if condition1
then
    command1
elif condition2 
then 
    command2
else
    commandN
fi
```

# for 循环

与其他编程语言类似，Shell支持for循环。

for循环一般格式为：

```bash
for var in item1 item2 ... itemN
do
    command1
    command2
    ...
    commandN
done
```

当变量值在列表里，for 循环即执行一次所有命令，使用变量名获取列表中的当前取值。命令可为任何有效的 shell 命令和语句。in 列表可以包含替换、字符串和文件名。

in列表是可选的，如果不用它，for循环使用命令行的位置参数。

例如，顺序输出当前列表中的数字：

## 实例

**for** loop **in** 1 2 3 4 5
**do**
  **echo** "The value is: $loop"
**done**

# while 语句

while 循环用于不断执行一系列命令，也用于从输入文件中读取数据。其语法格式为：

```bash
while condition
do
    command
done
while :##这个是死循环,判断也是两个括号
```

以下是一个基本的 while 循环，测试条件是：如果 int 小于等于 5，那么条件返回真。int 从 1 开始，每次循环处理时，int 加 1。运行上述脚本，返回数字 1 到 5，然后终止。

## 实例   let “int++” ，int++

*#!/bin/bash*
int=1
**while(( $int**<=5 ))
**do**
  **echo** $int
  **let** "int++"
**done**

# until 循环

until 循环执行一系列命令直至条件为 true 时停止。

until 循环与 while 循环在处理方式上刚好相反。

一般 while 循环优于 until 循环，但在某些时候—也只是极少数情况下，until 循环更加有用。

until 语法格式:

```
until condition
do
    command
done
```

condition 一般为条件表达式，如果返回值为 false，则继续执行循环体内的语句，否则跳出循环。

以下实例我们使用 until 命令来输出 0 ~ 9 的数字：

## 实例

*#!/bin/bash*

a=0

**until** **[** **!** $a -lt 10 **]**
**do**
  **echo** $a
  a=**`****expr** $a + 1**`**
**done**

```bash
#!/bin/bash
i=1
sum=0
until ((i > 100))
do
    ((sum += i))
    ((i++))
done
echo "The sum is: $sum"
```

# 循环内运算

```bash
((i++))
((sum+=i))  #跟c差不多，但是要加双括号
```

# case ... esac

**case ... esac** 为多选择语句，与其他语言中的 switch ... case 语句类似，是一种多分支选择结构，每个 case 分支用右圆括号开始，用两个分号 **;;** 表示 break，即执行结束，跳出整个 case ... esac 语句，esac（就是 case 反过来）作为结束标记。

可以用 case 语句匹配一个值与一个模式，如果匹配成功，执行相匹配的命令。

**case ... esac** 语法格式如下：

```
case 值 in
模式1)
    command1
    command2
    ...
    commandN
    ;;
模式2)
    command1
    command2
    ...
    commandN
    ;;
esac
```

case 工作方式如上所示，取值后面必须为单词 **in**，每一模式必须以右括号结束。取值可以为变量或常数，匹配发现取值符合某一模式后，其间所有命令开始执行直至 **;;**。

取值将检测匹配的每一个模式。一旦模式匹配，则执行完匹配模式相应命令后不再继续其他模式。如果无一匹配模式，使用星号 * 捕获该值，再执行后面的命令。

下面的脚本提示输入 1 到 4，与每一种模式进行匹配：

## 实例

**echo** '输入 1 到 4 之间的数字:'
**echo** '你输入的数字为:'
**read** aNum
**case** $aNum **in**
  1**)** **echo** '你选择了 1'
  **;;**
  2**)** **echo** '你选择了 2'
  **;;**
  3**)** **echo** '你选择了 3'
  **;;**
  4**)** **echo** '你选择了 4'
  **;;**
  *******)** **echo** '你没有输入 1 到 4 之间的数字'
  **;;**
**esac**

输入不同的内容，会有不同的结果，例如：

```
输入 1 到 4 之间的数字:
你输入的数字为:
3
你选择了 3
```

下面的脚本匹配字符串：

## 实例

*#!/bin/sh*

site="runoob"

**case** "$site" **in**
  "runoob"**)** **echo** "菜鸟教程"
  **;;**
  "google"**)** **echo** "Google 搜索"
  **;;**
  "taobao"**)** **echo** "淘宝网"
  **;;**
**esac**

# 跳出循环

在循环过程中，有时候需要在未达到循环结束条件时强制跳出循环，Shell 使用两个命令来实现该功能：**break** 和 **continue**。

# break 命令

break 命令允许跳出所有循环（终止执行后面的所有循环）。

下面的例子中，脚本进入死循环直至用户输入数字大于5。要跳出这个循环，返回到shell提示符下，需要使用break命令。

## 实例

*#!/bin/bash*
**while** :
**do**
  **echo** -n "输入 1 到 5 之间的数字:"
  **read** aNum
  **case** $aNum **in**
    1**|**2**|**3**|**4**|**5**)** **echo** "你输入的数字为 $aNum!"
    **;;**
    *******)** **echo** "你输入的数字不是 1 到 5 之间的! 游戏结束"
      **break**
    **;;**
  **esac**
**done**

执行以上代码，输出结果为：

```
输入 1 到 5 之间的数字:3
你输入的数字为 3!
输入 1 到 5 之间的数字:7
你输入的数字不是 1 到 5 之间的! 游戏结束
```

# continue

continue 命令与 break 命令类似，只有一点差别，它不会跳出所有循环，仅仅跳出当前循环。

对上面的例子进行修改：

## 实例

*#!/bin/bash*
**while** :
**do**
  **echo** -n "输入 1 到 5 之间的数字: "
  **read** aNum
  **case** $aNum **in**
    1**|**2**|**3**|**4**|**5**)** **echo** "你输入的数字为 $aNum!"
    **;;**
    *******)** **echo** "你输入的数字不是 1 到 5 之间的!"
      **continue**
      **echo** "游戏结束"
    **;;**
  **esac**
**done**

# shell函数

调用函数时使用函数名就行了

![image-20230203143831587](C:\Users\cao'yang'lin\AppData\Roaming\Typora\typora-user-images\image-20230203143831587.png)

函数传参就只要在使用函数名的后面加变量就行了

```bash
dosum(){
in=1
mj=89
echo "$in"
echo "$mj"
}
dosum  mj
```

![image-20230203144256558](C:\Users\cao'yang'lin\AppData\Roaming\Typora\typora-user-images\image-20230203144256558.png)

**[** **function** **]** funname [()]

**{**

  action;

  **[****return** int;**]**

**}**

说明：

- 1、可以带function fun() 定义，也可以直接fun() 定义,不带任何参数。
- 2、参数返回，可以显示加：return 返回，如果不加，将以最后一条命令运行结果，作为返回值。 return后跟数值n(0-255

下面的例子定义了一个函数并进行调用：

## 实例

*#!/bin/bash*
*# author:菜鸟教程*
*# url:www.runoob.com*

demoFun(){
  **echo** "这是我的第一个 shell 函数!"
**}**
**echo** "-----函数开始执行-----"
demoFun
**echo** "-----函数执行完毕-----"

输出结果：

```
-----函数开始执行-----
这是我的第一个 shell 函数!
-----函数执行完毕-----
```

下面定义一个带有return语句的函数：

## 实例

*#!/bin/bash*
*# author:菜鸟教程*
*# url:www.runoob.com*

funWithReturn(){
  **echo** "这个函数会对输入的两个数字进行相加运算..."
  **echo** "输入第一个数字: "
  **read** aNum
  **echo** "输入第二个数字: "
  **read** anotherNum
  **echo** "两个数字分别为 $aNum 和 $anotherNum !"
  **return** $**(($aNum+$anotherNum**))
**}**
funWithReturn
**echo** "输入的两个数字之和为 $? !"

输出类似下面：

```
这个函数会对输入的两个数字进行相加运算...
输入第一个数字: 
1
输入第二个数字: 
2
两个数字分别为 1 和 2 !
输入的两个数字之和为 3 !
```

函数返回值在调用该函数后通过 $? 来获得。

注意：所有函数在使用前必须定义。这意味着必须将函数放在脚本开始部分，直至shell解释器首次发现它时，才可以使用。调用函数仅使用其函数名即可。

------

# 函数参数

在Shell中，调用函数时可以向其传递参数。在函数体内部，通过 $n 的形式来获取参数的值，例如，$1表示第一个参数，$2表示第二个参数...

带参数的函数示例：

## 实例

*#!/bin/bash*
*# author:菜鸟教程*
*# url:www.runoob.com*

funWithParam**(****)****{**
  **echo** "第一个参数为 $1 !"
  **echo** "第二个参数为 $2 !"
  **echo** "第十个参数为 $10 !"
  **echo** "第十个参数为 ${10} !"
  **echo** "第十一个参数为 ${11} !"
  **echo** "参数总数有 $# 个!"
  **echo** "作为一个字符串输出所有参数 $* !"
**}**
funWithParam 1 2 3 4 5 6 7 8 9 34 73

输出结果：

```
第一个参数为 1 !
第二个参数为 2 !
第十个参数为 10 !
第十个参数为 34 !
第十一个参数为 73 !
参数总数有 11 个!
作为一个字符串输出所有参数 1 2 3 4 5 6 7 8 9 34 73 !
```

![image-20230203112751056](C:\Users\cao'yang'lin\AppData\Roaming\Typora\typora-user-images\image-20230203112751056.png)

![image-20230203130411530](C:\Users\cao'yang'lin\AppData\Roaming\Typora\typora-user-images\image-20230203130411530.png)

# 循环流写在.sh文件中

# if后面一定只能接ture或者flase，所以只能接test判断

# bash的=后面和前面加空格是判断，不加空格是赋值

# Linux 磁盘管理

Linux 磁盘管理好坏直接关系到整个系统的性能问题。

Linux 磁盘管理常用三个命令为 **df**、**du** 和 **fdisk**。

- **df**（英文全称：disk free）：列出文件系统的整体磁盘使用量
- **du**（英文全称：disk used）：检查磁盘空间使用量
- **fdisk**：用于磁盘分区

------

## df

df命令参数功能：检查文件系统的磁盘空间占用情况。可以利用该命令来获取硬盘被占用了多少空间，目前还剩下多少空间等信息。

语法：

```
df [-ahikHTm] [目录或文件名]
```

选项与参数：

- -a ：列出所有的文件系统，包括系统特有的 /proc 等文件系统；
- -k ：以 KBytes 的容量显示各文件系统；
- -m ：以 MBytes 的容量显示各文件系统；
- -h ：以人们较易阅读的 GBytes, MBytes, KBytes 等格式自行显示；
- -H ：以 M=1000K 取代 M=1024K 的进位方式；
- -T ：显示文件系统类型, 连同该 partition 的 filesystem 名称 (例如 ext3) 也列出；
- -i ：不用硬盘容量，而以 inode 的数量来显示

### 实例 1

将系统内所有的文件系统列出来！

```
[root@www ~]# df
Filesystem      1K-blocks      Used Available Use% Mounted on
/dev/hdc2         9920624   3823112   5585444  41% /
/dev/hdc3         4956316    141376   4559108   4% /home
/dev/hdc1          101086     11126     84741  12% /boot
tmpfs              371332         0    371332   0% /dev/shm
```

在 Linux 底下如果 df 没有加任何选项，那么默认会将系统内所有的 (不含特殊内存内的文件系统与 swap) 都以 1 Kbytes 的容量来列出来！

### 实例 2

将容量结果以易读的容量格式显示出来

```
[root@www ~]# df -h
Filesystem            Size  Used Avail Use% Mounted on
/dev/hdc2             9.5G  3.7G  5.4G  41% /
/dev/hdc3             4.8G  139M  4.4G   4% /home
/dev/hdc1              99M   11M   83M  12% /boot
tmpfs                 363M     0  363M   0% /dev/shm
```

### 实例 3

将系统内的所有特殊文件格式及名称都列出来

```
[root@www ~]# df -aT
Filesystem    Type 1K-blocks    Used Available Use% Mounted on
/dev/hdc2     ext3   9920624 3823112   5585444  41% /
proc          proc         0       0         0   -  /proc
sysfs        sysfs         0       0         0   -  /sys
devpts      devpts         0       0         0   -  /dev/pts
/dev/hdc3     ext3   4956316  141376   4559108   4% /home
/dev/hdc1     ext3    101086   11126     84741  12% /boot
tmpfs        tmpfs    371332       0    371332   0% /dev/shm
none   binfmt_misc         0       0         0   -  /proc/sys/fs/binfmt_misc
sunrpc  rpc_pipefs         0       0         0   -  /var/lib/nfs/rpc_pipefs
```

### 实例 4

将 /etc 底下的可用的磁盘容量以易读的容量格式显示

```
[root@www ~]# df -h /etc
Filesystem            Size  Used Avail Use% Mounted on
/dev/hdc2             9.5G  3.7G  5.4G  41% /
```

------

## du

Linux du 命令也是查看使用空间的，但是与 df 命令不同的是 Linux du 命令是对文件和目录磁盘使用的空间的查看，还是和df命令有一些区别的，这里介绍 Linux du 命令。

语法：

```
du [-ahskm] 文件或目录名称
```

选项与参数：

- -a ：列出所有的文件与目录容量，因为默认仅统计目录底下的文件量而已。
- -h ：以人们较易读的容量格式 (G/M) 显示；
- -s ：列出总量而已，而不列出每个各别的目录占用容量；
- -S ：不包括子目录下的总计，与 -s 有点差别。
- -k ：以 KBytes 列出容量显示；
- -m ：以 MBytes 列出容量显示；

### 实例 1

只列出当前目录下的所有文件夹容量（包括隐藏文件夹）:

```
[root@www ~]# du
8       ./test4     <==每个目录都会列出来
8       ./test2
....中间省略....
12      ./.gconfd   <==包括隐藏文件的目录
220     .           <==这个目录(.)所占用的总量
```

直接输入 du 没有加任何选项时，则 du 会分析当前所在目录里的子目录所占用的硬盘空间。

### 实例 2

将文件的容量也列出来

```
[root@www ~]# du -a
12      ./install.log.syslog   <==有文件的列表了
8       ./.bash_logout
8       ./test4
8       ./test2
....中间省略....
12      ./.gconfd
220     .
```

### 实例 3

检查根目录底下每个目录所占用的容量

```
[root@www ~]# du -sm /*
7       /bin
6       /boot
.....中间省略....
0       /proc
.....中间省略....
1       /tmp
3859    /usr     <==系统初期最大就是他了啦！
77      /var
```

通配符 * 来代表每个目录。

与 df 不一样的是，du 这个命令其实会直接到文件系统内去搜寻所有的文件数据。

------

## fdisk

fdisk 是 Linux 的磁盘分区表操作工具。

语法：

```
fdisk [-l] 装置名称
```

选项与参数：

- -l ：输出后面接的装置所有的分区内容。若仅有 fdisk -l 时， 则系统将会把整个系统内能够搜寻到的装置的分区均列出来。

### 实例 1

列出所有分区信息

```
[root@AY120919111755c246621 tmp]# fdisk -l

Disk /dev/xvda: 21.5 GB, 21474836480 bytes
255 heads, 63 sectors/track, 2610 cylinders
Units = cylinders of 16065 * 512 = 8225280 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disk identifier: 0x00000000

    Device Boot      Start         End      Blocks   Id  System
/dev/xvda1   *           1        2550    20480000   83  Linux
/dev/xvda2            2550        2611      490496   82  Linux swap / Solaris

Disk /dev/xvdb: 21.5 GB, 21474836480 bytes
255 heads, 63 sectors/track, 2610 cylinders
Units = cylinders of 16065 * 512 = 8225280 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disk identifier: 0x56f40944

    Device Boot      Start         End      Blocks   Id  System
/dev/xvdb2               1        2610    20964793+  83  Linux
```

### 实例 2

找出你系统中的根目录所在磁盘，并查阅该硬盘内的相关信息

```
[root@www ~]# df /            <==注意：重点在找出磁盘文件名而已
Filesystem           1K-blocks      Used Available Use% Mounted on
/dev/hdc2              9920624   3823168   5585388  41% /

[root@www ~]# fdisk /dev/hdc  <==仔细看，不要加上数字喔！
The number of cylinders for this disk is set to 5005.
There is nothing wrong with that, but this is larger than 1024,
and could in certain setups cause problems with:
1) software that runs at boot time (e.g., old versions of LILO)
2) booting and partitioning software from other OSs
   (e.g., DOS FDISK, OS/2 FDISK)

Command (m for help):     <==等待你的输入！
```

输入 m 后，就会看到底下这些命令介绍

```
Command (m for help): m   <== 输入 m 后，就会看到底下这些命令介绍
Command action
   a   toggle a bootable flag
   b   edit bsd disklabel
   c   toggle the dos compatibility flag
   d   delete a partition            <==删除一个partition
   l   list known partition types
   m   print this menu
   n   add a new partition           <==新增一个partition
   o   create a new empty DOS partition table
   p   print the partition table     <==在屏幕上显示分割表
   q   quit without saving changes   <==不储存离开fdisk程序
   s   create a new empty Sun disklabel
   t   change a partition's system id
   u   change display/entry units
   v   verify the partition table
   w   write table to disk and exit  <==将刚刚的动作写入分割表
   x   extra functionality (experts only)
```

离开 fdisk 时按下 `q`，那么所有的动作都不会生效！相反的， 按下`w`就是动作生效的意思。

```
Command (m for help): p  <== 这里可以输出目前磁盘的状态

Disk /dev/hdc: 41.1 GB, 41174138880 bytes        <==这个磁盘的文件名与容量
255 heads, 63 sectors/track, 5005 cylinders      <==磁头、扇区与磁柱大小
Units = cylinders of 16065 * 512 = 8225280 bytes <==每个磁柱的大小

   Device Boot      Start         End      Blocks   Id  System
/dev/hdc1   *           1          13      104391   83  Linux
/dev/hdc2              14        1288    10241437+  83  Linux
/dev/hdc3            1289        1925     5116702+  83  Linux
/dev/hdc4            1926        5005    24740100    5  Extended
/dev/hdc5            1926        2052     1020096   82  Linux swap / Solaris
# 装置文件名 启动区否 开始磁柱    结束磁柱  1K大小容量 磁盘分区槽内的系统

Command (m for help): q
```

想要不储存离开吗？按下 q 就对了！不要随便按 w 啊！

使用 `p` 可以列出目前这颗磁盘的分割表信息，这个信息的上半部在显示整体磁盘的状态。

------

### 磁盘格式化

磁盘分割完毕后自然就是要进行文件系统的格式化，格式化的命令非常的简单，使用 `mkfs`（make filesystem） 命令。

语法：

```
mkfs [-t 文件系统格式] 装置文件名
```

选项与参数：

- -t ：可以接文件系统格式，例如 ext3, ext2, vfat 等(系统有支持才会生效)

### 实例 1

查看 mkfs 支持的文件格式

```
[root@www ~]# mkfs[tab][tab]
mkfs         mkfs.cramfs  mkfs.ext2    mkfs.ext3    mkfs.msdos   mkfs.vfat
```

按下两个[tab]，会发现 mkfs 支持的文件格式如上所示。

### 实例 2

将分区 /dev/hdc6（可指定你自己的分区） 格式化为 ext3 文件系统：

```
[root@www ~]# mkfs -t ext3 /dev/hdc6
mke2fs 1.39 (29-May-2006)
Filesystem label=                <==这里指的是分割槽的名称(label)
OS type: Linux
Block size=4096 (log=2)          <==block 的大小配置为 4K 
Fragment size=4096 (log=2)
251392 inodes, 502023 blocks     <==由此配置决定的inode/block数量
25101 blocks (5.00%) reserved for the super user
First data block=0
Maximum filesystem blocks=515899392
16 block groups
32768 blocks per group, 32768 fragments per group
15712 inodes per group
Superblock backups stored on blocks:
        32768, 98304, 163840, 229376, 294912

Writing inode tables: done
Creating journal (8192 blocks): done <==有日志记录
Writing superblocks and filesystem accounting information: done

This filesystem will be automatically checked every 34 mounts or
180 days, whichever comes first.  Use tune2fs -c or -i to override.
# 这样就创建起来我们所需要的 Ext3 文件系统了！简单明了！
```

------

## 磁盘检验

fsck（file system check）用来检查和维护不一致的文件系统。

若系统掉电或磁盘发生问题，可利用fsck命令对文件系统进行检查。

语法：

```
fsck [-t 文件系统] [-ACay] 装置名称
```

选项与参数：

- -t : 给定档案系统的型式，若在 /etc/fstab 中已有定义或 kernel 本身已支援的则不需加上此参数
- -s : 依序一个一个地执行 fsck 的指令来检查
- -A : 对/etc/fstab 中所有列出来的 分区（partition）做检查
- -C : 显示完整的检查进度
- -d : 打印出 e2fsck 的 debug 结果
- -p : 同时有 -A 条件时，同时有多个 fsck 的检查一起执行
- -R : 同时有 -A 条件时，省略 / 不检查
- -V : 详细显示模式
- -a : 如果检查有错则自动修复
- -r : 如果检查有错则由使用者回答是否修复
- -y : 选项指定检测每个文件是自动输入yes，在不确定那些是不正常的时候，可以执行 # fsck -y 全部检查修复。

### 实例 1

查看系统有多少文件系统支持的 fsck 命令：

```
[root@www ~]# fsck[tab][tab]
fsck         fsck.cramfs  fsck.ext2    fsck.ext3    fsck.msdos   fsck.vfat
```

### 实例 2

强制检测 /dev/hdc6 分区:

```
[root@www ~]# fsck -C -f -t ext3 /dev/hdc6 
fsck 1.39 (29-May-2006)
e2fsck 1.39 (29-May-2006)
Pass 1: Checking inodes, blocks, and sizes
Pass 2: Checking directory structure
Pass 3: Checking directory connectivity
Pass 4: Checking reference counts
Pass 5: Checking group summary information
vbird_logical: 11/251968 files (9.1% non-contiguous), 36926/1004046 blocks
```

如果没有加上 -f 的选项，则由于这个文件系统不曾出现问题，检查的经过非常快速！若加上 -f 强制检查，才会一项一项的显示过程。

------

## 磁盘挂载与卸除

Linux 的磁盘挂载使用 `mount` 命令，卸载使用 `umount` 命令。

磁盘挂载语法：

```
mount [-t 文件系统] [-L Label名] [-o 额外选项] [-n]  装置文件名  挂载点
```

### 实例 1

用默认的方式，将刚刚创建的 /dev/hdc6 挂载到 /mnt/hdc6 上面！

```
[root@www ~]# mkdir /mnt/hdc6
[root@www ~]# mount /dev/hdc6 /mnt/hdc6
[root@www ~]# df
Filesystem           1K-blocks      Used Available Use% Mounted on
.....中间省略.....
/dev/hdc6              1976312     42072   1833836   3% /mnt/hdc6
```

磁盘卸载命令 `umount` 语法：

```
umount [-fn] 装置文件名或挂载点
```

选项与参数：

- -f ：强制卸除！可用在类似网络文件系统 (NFS) 无法读取到的情况下；
- -n ：不升级 /etc/mtab 情况下卸除。

卸载/dev/hdc6

# 一、service unit 常用命令，以 mysql 服务为例

```shell
# 开机启动
systemctl enable mysqld

# 关闭开机启动
systemctl disable mysqld

# 启动服务
systemctl start mysqld

# 停止服务
systemctl stop mysqld

# 重启服务
systemctl restart mysqld

# 查看服务状态
systemctl status mysqld
systemctl is-active sshd.service

# 结束服务进程(服务无法停止时)
systemctl kill mysqld
```

# 二、服务启动的配置文件

配置文件主要放在 /usr/lib/systemd/system 目录，也可能在 /etc/systemd/system 目录

```shell
# 查看 sshd 服务启动文件
systemctl cat sshd.service

# /usr/lib/systemd/system/sshd.service
[Unit]
Description=OpenSSH server daemon
Documentation=man:sshd(8) man:sshd_config(5)
After=network.target sshd-keygen.service
Wants=sshd-keygen.service

[Service]
Type=notify
EnvironmentFile=/etc/sysconfig/sshd
ExecStart=/usr/sbin/sshd -D $OPTIONS
ExecReload=/bin/kill -HUP $MAINPID
KillMode=process
Restart=on-failure
RestartSec=42s

[Install]
WantedBy=multi-user.target
```

每个服务文件以 .service 结尾，一般会分为 3 部分，必须包含 [Service] 部分

## [Unit] 启动顺序与依赖关系

```shell
Description：当前服务的简单描述
Documentation：指定 man 文档位置

After：如果 network.target 或 sshd-keygen.service 需要启动，那么 sshd.service 应该在它们之后启动
Before：定义 sshd 应该在哪些服务之前启动
注意：After 和 Before 字段只涉及启动顺序，不涉及依赖关系。

Wants：表示 sshd.service 与 sshd-keygen.service 之间存在"弱依赖"关系，即如果"sshd-keygen.service"启动失败或停止运行，不影响 sshd.service 继续执行
Requires：表示"强依赖"关系，即如果该服务启动失败或异常退出，那么sshd.service 也必须退出
注意：Wants 字段与 Requires 字段只涉及依赖关系，与启动顺序无关，默认情况下是同时启动。
```

## [Service] 启动行为

```shell
EnvironmentFile：许多软件都有自己的环境参数文件，该字段指定文件路径
注意：/etc/profile 或者 /etc/profile.d/ 这些文件中配置的环境变量仅对通过 pam 登录的用户生效，而 systemd 是不读这些配置的。
systemd 是所有进程的父进程或祖先进程，它的环境变量会被所有的子进程所继承，如果需要给 systemd 配置默认参数可以在 /etc/systemd/system.conf  和 /etc/systemd/user.conf 中设置。
加载优先级 system.conf 最低，可能会被其他的覆盖。


Type：定义启动类型。可设置：simple，exec，forking，oneshot，dbus，notify，idle
simple(设置了 ExecStart= 但未设置 BusName= 时的默认值)：ExecStart 字段启动的进程为该服务的主进程
forking：ExecStart 字段的命令将以 fork() 方式启动，此时父进程将会退出，子进程将成为主进程


ExecStart：定义启动进程时执行的命令
上面的例子中，启动 sshd 执行的命令是 /usr/sbin/sshd -D $OPTIONS，其中的变量 $OPTIONS 就来自 EnvironmentFile 字段指定的环境参数文件。类似的，还有如下字段：
ExecReload：重启服务时执行的命令
ExecStop：停止服务时执行的命令
ExecStartPre：启动服务之前执行的命令
ExecStartPost：启动服务之后执行的命令
ExecStopPost：停止服务之后执行的命令


RemainAfterExit：设为yes，表示进程退出以后，服务仍然保持执行


KillMode：定义 Systemd 如何停止服务，可以设置的值如下：
control-group（默认值）：当前控制组里面的所有子进程，都会被杀掉
process：只杀主进程
mixed：主进程将收到 SIGTERM 信号，子进程收到 SIGKILL 信号
none：没有进程会被杀掉，只是执行服务的 stop 命令


Restart：定义了退出后，Systemd 的重启方式。可以设置的值如下：
no（默认值）：退出后不会重启
on-success：只有正常退出时（退出状态码为0），才会重启
on-failure：非正常退出时（退出状态码非0），包括被信号终止和超时，才会重启
on-abnormal：只有被信号终止和超时，才会重启
on-abort：只有在收到没有捕捉到的信号终止时，才会重启
on-watchdog：超时退出，才会重启
always：不管是什么退出原因，总是重启


RestartSec：表示 Systemd 重启服务之前，需要等待的秒数
```

**配置中多个相同配置会选择最后一个，下面结果是 execstart2**

[Service]

ExecStart=/bin/echo execstart1

ExecStart=/bin/echo execstart2

 

**所有的启动设置之前，都可以加上一个连词号（-），表示"抑制错误"，即发生错误的时候，不影响其他命令的执行**

EnvironmentFile=-/etc/sysconfig/sshd，表示即使 /etc/sysconfig/sshd 文件不存在，也不会抛出错误

## [Install]

```shell
WantedBy：表示该服务所在的 Target(服务组)
```

```shell
# 查看默认 Target
systemctl get-default
# 结果为 multi-user.target，表示默认的启动 Target 是multi-user.target。在这个组里的所有服务，都将开机启动。这就是为什么 systemctl enable 命令能设置开机启动的原因


# 查看 multi-user.target 包含的所有服务
systemctl list-dependencies multi-user.target

# 切换到另一个 target
# shutdown.target 就是关机状态
# 常用的 Target 有两个：一个是 multi-user.target，表示多用户命令行状态；另一个是 graphical.target，表示图形用户状态，它依赖于 multi-user.target
systemctl isolate shutdown.target
```

**关于 Target，运行级别**

# 自定义服务

```shell
vim /usr/lib/systemd/system/zdy.service

[Unit]
Description=描述
Environment=环境变量或参数(系统环境变量此时无法使用)
After=network.target

[Service]
Type=forking
EnvironmentFile=所需环境变量文件或参数文件
ExecStart=启动命令(需指定全路径)
ExecStop=停止命令(需指定全路径)
User=以什么用户执行命令

[Install]
WantedBy=multi-user.target
```

新建完成后设置自启动

```shell
# 添加或修改配置文件后，需要重新加载
systemctl daemon-reload

# 设置自启动，实质就是在 /etc/systemd/system/multi-user.target.wants/ 添加服务文件的链接
systemctl enable zdy
```

# 防火墙

## 查看防火墙状态

```javascript
systemctl status firewalld
```

## 启动防火墙

```javascript
systemctl start firewalld
```

## 停止某项服务，这里举例停止防火墙

```javascript
systemctl stop firewalld
```

## 查看防火墙已经开放的端口

```javascript
firewall-cmd --list-port
```

## 添加开放指定防火墙

```javascript
firewall-cmd --zone=public --add-port=这里是需要开启的端口号/tcp --permanent
```

## 重新加载防火墙

```javascript
firewall-cmd --reload
firewall-cmd --remove-port=3306/tcp  --permanent 移除
service docker restart  docker重启
```

# Centos7下彻底删除Mysql

## 一、检查是否安装了Mysql

Yum检查
yum list installed | grep mysql

## 安装则直接删除

yum remove mysql mysql-server mysql-libs compat-mysql

yum remove mysql-community-release

rpm检查
rpm -qa | grep -i mysql 

有则直接删除

rpm -e --nodeps mysql-community-libs-5.7.22-1.el7.x86_64

rpm -e –nodeps mysql57-community-release-el7-11.noarch

## 二、口令查找Mysql的安装目录和残存文件

1. whereis mysql

2. find / -name mysql

找到后，全部rm删除。

## 三、查看mysql配置文件

以my.cnf为例，一般在/etc/my.cnf，直接rm即可。

如果设置了开机启动，也需要关闭。

chkconfig --list | grep -i mysql

chkconfig --del mysqld

## 四、再次检查

重复上面的步骤，检查是否完关于mysql的内容。



### 1、查看系统中是否自带安装mysql

```shell
yum list installed | grep mysql
```

### 2、删除系统自带的mysql及其依赖（防止冲突）

```shell
yum -y remove mysql-libs.x86_64
```

### 3、安装wget命令

```shell
yum install wget -y 
```

### 4、给CentOS添加rpm源，并且选择较新的源

```shell
wget -i -c https://dev.mysql.com/get/mysql80-community-release-el7-3.noarch.rpm
```

### 5、安装下载好的rpm文件

```shell
 yum install mysql80-community-release-el7-3.noarch.rpm -y
```

### 6、使用yum安装mysql

```shell
yum install mysql-community-server -y
```

### 6.1、安装中遇到错误解决方式

错误：
mysql-community-libs-8.0.32-1.el7.x86_64.rpm 的公钥尚未安装
失败的软件包是：mysql-community-libs-8.0.32-1.el7.x86_64
GPG 密钥配置为：file:///etc/pki/rpm-gpg/RPM-GPG-KEY-mysql
解决办法：
执行如下命令后再次安装

```shell
rpm --import https://repo.mysql.com/RPM-GPG-KEY-mysql-2022

```

### 7、启动mysql服务

\#启动mysql服务，查看启动状态及是否开机启动

```shell
systemctl start mysqld.service
systemctl status mysqld.service
systemctl list-unit-files | grep enabled
```

### 8、获取mysql的临时密码

```shell
grep "password" /var/log/mysqld.log

```

### 9、使用临时密码登录

```
mysql -uroot -p
#输入密码
```



### 10、修改密码

#密码要符合mysql安全规则，否则修改不成功

```
ALTER USER 'root'@'localhost' IDENTIFIED BY '密码';
```



### 11、修改远程访问权限

```
1.create user 'aiops'@'%' identified by '123456';
2.grant all privileges on *.* to 'aiops'@'%' with grant option;
3.flush privileges;
```

### 12、设置字符集为utf-8

#在[mysqld]部分添加：
character-set-server=utf8
#在文件末尾新增[client]段，并在[client]段添加：
default-character-set=utf8


# 后期继续



































[^a-d]: 不是a到d开头的
