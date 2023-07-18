# Docker的下载和安装，看官网，谁不看我笑他两年半

![image-20230303160553455](C:\Users\cao'yang'lin\AppData\Roaming\Typora\typora-user-images\image-20230303160553455.png)

# 如果你是别的系统

在使用[docker](https://so.csdn.net/so/search?q=docker&spm=1001.2101.3001.7020)容器的时候，想要安装vim。在使用apt-get install vim 命令安装的时候提示：

```shell
Reading package lists... Done
Building dependency tree       
Reading state information... Done
E: Unable to locate package vim
```

需要先执行 apt-get update命令，这个命令的作用是：同步 /etc/apt/sources.list 和 /etc/apt/sources.list.d 中列出的源的索引，这样才能获取到最新的软件包。再执行 apt-get install vim 就可以安装vim了。

# Docker的基本命令

```shell
docker version  #显示版本信息
docker info     #显示docker的系统信息,包括镜像和容器的数量
docker 命令 --help  #万能命令

```

帮助文档地址:[Reference documentation (docker.com)](https://docs.docker.com/reference/)

# docker的开启，如果没有设置开机自启的话

```shell
Start Docker.

$ sudo systemctl start docker
```



# 镜像命令

docker images 查看所有本地的主机的镜像

```shell
[root@localhost ~]# docker images 
REPOSITORY    TAG       IMAGE ID       CREATED         SIZE
hello-world   latest    feb5d9fea6a5   17 months ago   13.3kB
hello-world   latest    feb5d9fea6a5   17 months ago   13.3kB

#解释:
REPOSITORY 镜像的仓库源
TAG        镜像的标签
IMAGE ID   镜像的id
CREATED    镜像的创建时间
SIZE       镜像的大小


#可选项:
   Options:
  -a, --all             #列出所有的镜像
  -q, --quiet           #只显示镜像的ID


```

docker search 搜索镜像

```shell
[root@localhost ~]# docker search mysql
NAME                            DESCRIPTION                                      STARS     OFFICIAL   AUTOMATED
mysql                           MySQL is a widely used, open-source relation…   13878     [OK]       
mariadb                         MariaDB Server is a high performing open sou…   5291      [OK]       

#可选项
--filter =stars =3000   搜索出来的镜像就是stars大于三千的

[root@localhost ~]# docker search mysql --filter=stars=10000
NAME      DESCRIPTION                                      STARS     OFFICIAL   AUTOMATED
mysql     MySQL is a widely used, open-source relation…   13878     [OK]       

```

docker pull  下载镜像

```shell
#下载镜像    docker pull mysql  [:tag](版本)
[root@localhost ~]# docker pull mysql
Using default tag: latest
latest: Pulling from library/mysql
b4ddc423e046: Pull complete 
b338d8e4ffd1: Pull complete 
b2b1b06949ab: Pull complete 
daf393284da9: Pull complete 
1cb8337ae65d: Pull complete 
f6c2cc79221c: Pull complete 
4cec461351e0: Pull complete 
ab6bf0cba08e: Pull complete 
8df43cafbd11: Pull complete 
c6d0aac53df5: Pull complete 
b24148c7c251: Pull complete 
Digest: sha256:d8dc78532e9eb3759344bf89e6e7236a34132ab79150607eb08cc746989aa047
Status: Downloaded newer image for mysql:latest
docker.io/library/mysql:latest   #真实地址

#两个命令是等价的
docker pull mysql 
docker pull docker.io/library/mysql:latest

#指定版本下载
[root@localhost ~]# docker pull mysql:5.7.41
5.7.41: Pulling from library/mysql
e048d0a38742: Pull complete 
c7847c8a41cb: Pull complete 
351a550f260d: Pull complete 
8ce196d9d34f: Pull complete 
17febb6f2030: Pull complete 
d4e426841fb4: Pull complete 
fda41038b9f8: Pull complete 
f47aac56b41b: Pull complete 
a4a90c369737: Pull complete 
97091252395b: Pull complete 
84fac29d61e9: Pull complete 
Digest: sha256:8cf035b14977b26f4a47d98e85949a7dd35e641f88fc24aa4b466b36beecf9d6
Status: Downloaded newer image for mysql:5.7.41
docker.io/library/mysql:5.7.41

```

docker rml 删除镜像

```shell
[root@localhost ~]# docker rmi -f be16cf2d832a
Untagged: mysql:5.7.41
Untagged: mysql@sha256:8cf035b14977b26f4a47d98e85949a7dd35e641f88fc24aa4b466b36beecf9d6
Deleted: sha256:be16cf2d832a9a54ce42144e25f5ae7cc66bccf0e003837e7b5eb1a455dc742b
Deleted: sha256:2dd6e094d35f48086adcdff89f36c9be8166fbbda0775b72efd9b12788a400a0
Deleted: sha256:01de218cde8a6eef7c19083f1a9dfdcc10e656651137c5083c8e8b293561e674
Deleted: sha256:84e3163c39fc29722fbea1461bc279bafc9d2da5937b1f4e5db6e08c6f08e3b4
Deleted: sha256:2b39b403c72a380afa25629a8b0af21e5bd33b071985740242e63856e6453359
Deleted: sha256:bf76a072ee83eef013d21ef4aed92cea89f1d15edd62ce0d4204268f513a2658
Deleted: sha256:8112761750f4100814858c647189c97db4129852fec2060580625254fa9b3440
Deleted: sha256:a527ebda1c7ee77668ecfec84a62ba7cc46769946fb565ff7895f2a0aecfd082
Deleted: sha256:ba8f679e76a9faba19756857e6f5d6809d8ba0a90507c6a815f3823244636e64
Deleted: sha256:51b0a4dc7d8cdf87950abd409fe3155df9118e4b33a1bbe91d6367d62557db87
Deleted: sha256:f3277814332978b36b309d241f692a182e37564d96a94fdde0382cb471953483
Deleted: sha256:c233345f327a72c79e2e19c75fcf9089a0c1488dfb66dd00d49fa2a5d1f76057


#docker rmi -f $(docker images -aq)    #删除全部的容器

```





# 容器命令

说明: 我们有了镜像才可以创建容器,linux,下载一个CentOS镜像来测试学习

```shell
docker pull centos
```

## 新建容器并启动

```shell
docker run [可选参数] image

# 参数说明
--name="Name"   容器名字   tomcat001   tomcat002 ,用来区分容器
-d              后台方式运行
-it             使用交互方式运行，进入容器查看内容
-p              指定容器的端口   -p 8080:8080
     -p ip:主机端口:容器端口
     -p 主机端口:容器端口      (常用的)
     -p 容器端口
     容器端口
-P              随机指定端口




#测试,启动并进入容器
[root@localhost ~]# docker run -it centos /bin/bash
[root@f77cf5efff07 /]# ls  #查看容器内的centos,基础版本，很多命令都是不完善的
bin  dev  etc  home  lib  lib64  lost+found  media  mnt  opt  proc  root  run  sbin  srv  sys  tmp  usr  var 

#进入容器
[root@localhost home]# docker run -it baecb060a464 /bin/bash

#从容器中退出主机
[root@f77cf5efff07 /]# exit
exit
[root@localhost ~]# ls
anaconda-ks.cfg  cmake01  GameBookServer            mysql80-community-release-el7-7.noarch.rpm  redis-6.0.16 (3).tar.gz  test.c  模板  图片  下载  桌面
bianyi           cmake02  jdk-18_linux-x64_bin.rpm  redis-6.0.16                                test                 公共    视频  文档  音乐

```

## 列出所有的运行的容器

```shell
#docker ps 命令
     #列出当前正在运行的容器
-a   #列出当前正在运行的容器+带出历史运行过的容器
-n=? #显示最近创建的容器
-q   #只显示容器的编号


[root@localhost ~]# docker ps
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
[root@localhost ~]# docker ps -a
CONTAINER ID   IMAGE          COMMAND       CREATED         STATUS                     PORTS     NAMES
f77cf5efff07   centos         "/bin/bash"   7 minutes ago   Exited (0) 2 minutes ago             gifted_lehmann
06a28682bc04   feb5d9fea6a5   "/hello"      2 hours ago     Exited (0) 2 hours ago               reverent_khorana
aac81cb05c0d   feb5d9fea6a5   "/hello"      2 weeks ago     Exited (0) 2 weeks ago               infallible_bassi

```

## 退出容器

```shell
exit    #直接容器停止并退出
Ctrl +P +Q #容器不停止退出
[root@localhost ~]# docker run -it centos /bin/bash
[root@0d56e07d34d8 /]# [root@localhost ~]# docker ps
CONTAINER ID   IMAGE     COMMAND       CREATED          STATUS          PORTS     NAMES
0d56e07d34d8   centos    "/bin/bash"   20 seconds ago   Up 19 seconds             intelligent_jang
[root@localhost ~]# 

```



## 删除容器

```shell
docker rm 容器id                #删除指定的容器,不能删除正在运行的容器,如果要强制删除 rm -f
docker rm -f $(docker ps -aq)  #删除所有的容器
docker rm $(docker ps -aq)     #删除所有的容器
```

## 启动和停止容器的操作

```shell
docker start 容器id             #启动容器
docker restart 容器id           #重启容器
docker stop 容器id              #停止当前正在运行的容器
docker kill 容器id              #强制停止当前容器
```

# 常用的其他命令

后台启动容器

```shell
# 命令 docker run -d 镜像名 !
[root@localhost ~]# docker run -d centos
# 问题docker ps 发现centos停止了

#常见的坑 ,docker 容器启动后台运行，就必须要有一个前台进程，docker发现没有应用，就会自动停止
#nginx，容器启动后，发现自己没有提供服务，就会立刻停止，没有程序了
docker run -p 3303:3306 --name mysql-master \
-v /mydata/mysql-master/log:/var/log/mysql \
-v /mydata/mysql-master/data:/var/lib/mysql \
-v /mydata/mysql-master/conf:/etc/mysql \
-e MYSQL_ROOT_PASSWORD=root  \
-d mysql:5.7

```

## 查看日志命令

```shell
docker logs -f --tail  
#自己写一个shell脚本
[root@localhost ~]# docker run -d centos /bin/sh -c "while true;do echo caoyanglin ;sleep 1;done"

#展示出服务器id
[root@localhost ~]# docker ps -a
CONTAINER ID   IMAGE     COMMAND                   CREATED          STATUS         PORTS     NAMES
08504c38c87e   centos    "/bin/sh -c 'while t…"   10 seconds ago   Up 9 seconds             thirsty_almeida
#显示日志
 -tf            #显示的日志
 --tail number  #要显示的日志条数
[root@localhost ~]# docker logs -tf --tail 10 08504c38c87e

```

## 查看容器中进程信息 ps

```shell
[root@localhost ~]# docker top 08504c38c87e
UID                 PID                 PPID                C                   STIME               TTY     
root                20400               20380               0                   18:40               ?       
root                22335               20400               0                   18:55               ?       
```

## 查看镜像的元数据

```shell
#命令
[root@localhost ~]# docker inspect 08504c38c87e


#测试
[
    {
        "Id": "08504c38c87ee8ac68aa7d2cd66793cd21abf4cdb097765e111dedd3e8f0e7d2",
        "Created": "2023-03-03T10:40:17.000488802Z",
        "Path": "/bin/sh",
        "Args": [
            "-c",
            "while true;do echo caoyanglin ;sleep 1;done"
        ],
        "State": {
            "Status": "running",
            "Running": true,
            "Paused": false,
            "Restarting": false,
            "OOMKilled": false,
            "Dead": false,
            "Pid": 20400,
            "ExitCode": 0,
            "Error": "",
            "StartedAt": "2023-03-03T10:40:17.275031068Z",
            "FinishedAt": "0001-01-01T00:00:00Z"
        },
        "Image": "sha256:5d0da3dc976460b72c77d94c8a1ad043720b0416bfc16c52c45d4847e53fadb6",
        "ResolvConfPath": "/var/lib/docker/containers/08504c38c87ee8ac68aa7d2cd66793cd21abf4cdb097765e111dedd3e8f0e7d2/resolv.conf",
        "HostnamePath": "/var/lib/docker/containers/08504c38c87ee8ac68aa7d2cd66793cd21abf4cdb097765e111dedd3e8f0e7d2/hostname",
        "HostsPath": "/var/lib/docker/containers/08504c38c87ee8ac68aa7d2cd66793cd21abf4cdb097765e111dedd3e8f0e7d2/hosts",
        "LogPath": "/var/lib/docker/containers/08504c38c87ee8ac68aa7d2cd66793cd21abf4cdb097765e111dedd3e8f0e7d2/08504c38c87ee8ac68aa7d2cd66793cd21abf4cdb097765e111dedd3e8f0e7d2-json.log",
        "Name": "/thirsty_almeida",
        "RestartCount": 0,
        "Driver": "overlay2",
        "Platform": "linux",
        "MountLabel": "",
        "ProcessLabel": "",
        "AppArmorProfile": "",
        "ExecIDs": null,
        "HostConfig": {
            "Binds": null,
            "ContainerIDFile": "",
            "LogConfig": {
                "Type": "json-file",
                "Config": {}
            },
            "NetworkMode": "default",
            "PortBindings": {},
            "RestartPolicy": {
                "Name": "no",
                "MaximumRetryCount": 0
            },
            "AutoRemove": false,
            "VolumeDriver": "",
            "VolumesFrom": null,
            "ConsoleSize": [
                41,
                189
            ],
            "CapAdd": null,
            "CapDrop": null,
            "CgroupnsMode": "host",
            "Dns": [],
            "DnsOptions": [],
            "DnsSearch": [],
            "ExtraHosts": null,
            "GroupAdd": null,
            "IpcMode": "private",
            "Cgroup": "",
            "Links": null,
            "OomScoreAdj": 0,
            "PidMode": "",
            "Privileged": false,
            "PublishAllPorts": false,
            "ReadonlyRootfs": false,
            "SecurityOpt": null,
            "UTSMode": "",
            "UsernsMode": "",
            "ShmSize": 67108864,
            "Runtime": "runc",
            "Isolation": "",
            "CpuShares": 0,
            "Memory": 0,
            "NanoCpus": 0,
            "CgroupParent": "",
            "BlkioWeight": 0,
            "BlkioWeightDevice": [],
            "BlkioDeviceReadBps": [],
            "BlkioDeviceWriteBps": [],
            "BlkioDeviceReadIOps": [],
            "BlkioDeviceWriteIOps": [],
            "CpuPeriod": 0,
            "CpuQuota": 0,
            "CpuRealtimePeriod": 0,
            "CpuRealtimeRuntime": 0,
            "CpusetCpus": "",
            "CpusetMems": "",
            "Devices": [],
            "DeviceCgroupRules": null,
            "DeviceRequests": null,
            "MemoryReservation": 0,
            "MemorySwap": 0,
            "MemorySwappiness": null,
            "OomKillDisable": false,
            "PidsLimit": null,
            "Ulimits": null,
            "CpuCount": 0,
            "CpuPercent": 0,
            "IOMaximumIOps": 0,
            "IOMaximumBandwidth": 0,
            "MaskedPaths": [
                "/proc/asound",
                "/proc/acpi",
                "/proc/kcore",
                "/proc/keys",
                "/proc/latency_stats",
                "/proc/timer_list",
                "/proc/timer_stats",
                "/proc/sched_debug",
                "/proc/scsi",
                "/sys/firmware"
            ],
            "ReadonlyPaths": [
                "/proc/bus",
                "/proc/fs",
                "/proc/irq",
                "/proc/sys",
                "/proc/sysrq-trigger"
            ]
        },
        "GraphDriver": {
            "Data": {
                "LowerDir": "/var/lib/docker/overlay2/5ddce84565d6c04924a542be883fe457f0f5631d8e7377f6c713cde1d78b6a69-init/diff:/var/lib/docker/overlay2/6c7d5de3e945d5b9ec9282d89a3ba316a30352474b400050232ff19fa9ab78fb/diff",
                "MergedDir": "/var/lib/docker/overlay2/5ddce84565d6c04924a542be883fe457f0f5631d8e7377f6c713cde1d78b6a69/merged",
                "UpperDir": "/var/lib/docker/overlay2/5ddce84565d6c04924a542be883fe457f0f5631d8e7377f6c713cde1d78b6a69/diff",
                "WorkDir": "/var/lib/docker/overlay2/5ddce84565d6c04924a542be883fe457f0f5631d8e7377f6c713cde1d78b6a69/work"
            },
            "Name": "overlay2"
        },
        "Mounts": [],
        "Config": {
            "Hostname": "08504c38c87e",
            "Domainname": "",
            "User": "",
            "AttachStdin": false,
            "AttachStdout": false,
            "AttachStderr": false,
            "Tty": false,
            "OpenStdin": false,
            "StdinOnce": false,
            "Env": [
                "PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin"
            ],
            "Cmd": [
                "/bin/sh",
                "-c",
                "while true;do echo caoyanglin ;sleep 1;done"
            ],
            "Image": "centos",
            "Volumes": null,
            "WorkingDir": "",
            "Entrypoint": null,
            "OnBuild": null,
            "Labels": {
                "org.label-schema.build-date": "20210915",
                "org.label-schema.license": "GPLv2",
                "org.label-schema.name": "CentOS Base Image",
                "org.label-schema.schema-version": "1.0",
                "org.label-schema.vendor": "CentOS"
            }
        },
        "NetworkSettings": {
            "Bridge": "",
            "SandboxID": "3bab56edbb62ed8d524fff0c9a4677b7917760643c9685f3599056e93e9f2d21",
            "HairpinMode": false,
            "LinkLocalIPv6Address": "",
            "LinkLocalIPv6PrefixLen": 0,
            "Ports": {},
            "SandboxKey": "/var/run/docker/netns/3bab56edbb62",
            "SecondaryIPAddresses": null,
            "SecondaryIPv6Addresses": null,
            "EndpointID": "ee729c09aa5cf4cb35dc53e22faea80b1ea763f91a137c3e96daa29e7a58c140",
            "Gateway": "172.17.0.1",
            "GlobalIPv6Address": "",
            "GlobalIPv6PrefixLen": 0,
            "IPAddress": "172.17.0.2",
            "IPPrefixLen": 16,
            "IPv6Gateway": "",
            "MacAddress": "02:42:ac:11:00:02",
            "Networks": {
                "bridge": {
                    "IPAMConfig": null,
                    "Links": null,
                    "Aliases": null,
                    "NetworkID": "3eb2b5e1358f67189e127f1437850080ea0e73b0e6e0160c91fcf878bb7241f3",
                    "EndpointID": "ee729c09aa5cf4cb35dc53e22faea80b1ea763f91a137c3e96daa29e7a58c140",
                    "Gateway": "172.17.0.1",
                    "IPAddress": "172.17.0.2",
                    "IPPrefixLen": 16,
                    "IPv6Gateway": "",
                    "GlobalIPv6Address": "",
                    "GlobalIPv6PrefixLen": 0,
                    "MacAddress": "02:42:ac:11:00:02",
                    "DriverOpts": null
                }
            }
        }
    }
]

```

## 进入当前正在运行的容器

```shell
# 我们通常容器都是使用后台方式运行的，需要进入容器，修改一些配置

#命令
docker exec -it 容器的id  bashShell

#测试
[root@localhost ~]# docker exec -it 08504c38c87e /bin/bash
[root@08504c38c87e /]# ls
bin  dev  etc  home  lib  lib64  lost+found  media  mnt  opt  proc  root  run  sbin  srv  sys  tmp  usr  var
[root@08504c38c87e /]# cd lib
[root@08504c38c87e lib]# ll
bash: ll: command not found
[root@08504c38c87e lib]# cd /
[root@08504c38c87e /]# ll
bash: ll: command not found
[root@08504c38c87e /]# ls
bin  dev  etc  home  lib  lib64  lost+found  media  mnt  opt  proc  root  run  sbin  srv  sys  tmp  usr  var
[root@08504c38c87e /]# ps -ef
UID         PID   PPID  C STIME TTY          TIME CMD
root          1      0  0 10:40 ?        00:00:00 /bin/sh -c while true;do echo caoyanglin ;sleep 1;done
root       1667      0  0 11:08 pts/0    00:00:00 /bin/bash
root       1795      1  0 11:09 ?        00:00:00 /usr/bin/coreutils --coreutils-prog-shebang=sleep /usr/bin/sleep 1
root       1796   1667  0 11:09 pts/0    00:00:00 ps -ef
[root@08504c38c87e /]# cd home
[root@08504c38c87e home]# ll
bash: ll: command not found
[root@08504c38c87e home]# ls
[root@08504c38c87e home]# touch t1.txt
[root@08504c38c87e home]# ls
t1.txt
[root@08504c38c87e home]# vim t1.txt
bash: vim: command not found

#方式二
docker attach 容器ID
正在执行当前的代码


#docker exec      #进入容器后开启一个新的终端
#docker attach    #进入容器正在执行的终端，不会启动新的进程
```

## 从容器内拷贝文件到主机上

```shell
docker cp 容器id :容器内路径 目的的主机

#进入容器内，新建一个文件
[root@localhost bianyi]# docker attach 76b3e15bb464
[root@76b3e15bb464 /]# cd /home
[root@76b3e15bb464 home]# ls
[root@76b3e15bb464 home]# touch test.java
[root@76b3e15bb464 home]# exit
exit


#将容器里面的文件拷贝出来
[root@localhost bianyi]# docker ps -a
CONTAINER ID   IMAGE     COMMAND       CREATED          STATUS                      PORTS     NAMES
76b3e15bb464   centos    "/bin/bash"   17 minutes ago   Exited (0) 18 seconds ago             cranky_beaver
[root@localhost bianyi]# docker cp 76b3e15bb464:/home/test.java /home
Preparing to copy...
Successfully copied 1.536kB to /home

#查看
[root@localhost /]# cd home
[root@localhost home]# ll
总用量 4
drwx------. 16 it   it   4096 2月   3 11:02 it
-rw-r--r--.  1 root root    0 3月   3 19:54 test.java

#拷贝是一个手动过程，未来我们使用 -v 卷的技术，可以实现
```

学习方式：将我的所有命令全部敲一遍

# 常用命令小结

![img](https://img-blog.csdnimg.cn/20201006011640397.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzI0NjIxNQ==,size_16,color_FFFFFF,t_70#pic_center)

命令	英文描述	中文意思
attach	Attach to a running container	当前shell下attach连接指定运行镜像
build	Build an image from a Dockerfile	通过Dockerfile定制镜像
commit	Create a new image from a container changes	提交当前容器为新的境像
cp	copy files/folders from the containers filesystem to the host path	从容器中拷贝指定文件或者目录到宿主机中
create	Create a new container	创建一个新的容器，同run.但不启动容器
diff	Inspect changes on a container’s filesystem	查看docker容器变化
events	Get real time events from the server	从docker服务中获取容器实时事件
export	Stream the contents of a container as a tar archive	导出容器的内容流作为一个 tar归档文件[对应import]
history	Show the history of an image	展示一个境像形成历史
images	List images	列出系统当前所有镜像
import	Create a new filesystem image from the contents of a tarball	从tar包中的内容创建一个新的文件系统映像[对应export]
info	Display system-wide information	显示系统相关信息
inspect	Return low-level information on a container	查看容器详细信息
kill	Kill a running container	kill指定docker容器
load	Load an image from a tar archive	从—个 tar包中加载一个镜像[对应save]
login	Register or Login to the docker registry server	注册或者登陆一个docker源服务器
logout	Log out from a Docker registry server	从当前Docker registry退出
logs	Fetch the logs of a container	输出当前容器日志信息
port	Lookup the public-facing port which is NAT-ed to PRIVATE_PORT	查看映射端口对应的容器内部源端
pause	Pause all processes within a container	暂停容器
ps	List containers	列出容器列表
pull	Pull an image or a repository from the docker registry server	从docker镜像服务器中拉取指定镜像或者库镜像
push	push an image or a repository to the docker registry server	推送指定镜像或者库镜像至docker源服务器
restart	Restart a running container	重启运行的容器
rm	Remove one or more containers	移除—个或者多个容器
rmi	Remove one or more images	移除一个或多个境像[无容器使用该镜像才可删除，否则需删除相关容器才可能继续或者 -f 强制删除
run	Run a command in a new container	创建—个新的容器并运行一个命令
save	Save an image to a tar arehive	保存一个镜像为—个tar包「对应load]
search	Search for an image on the Docker Hub	在docker hub中搜索镜像
start	start a stopped containers	启动容器
stop	stop a stopped containers	停止容器
tag	Tag an image into a repository	给源中镜像打标签
top	Lookup the running processes of a container	查看容器中运行的进程信息
unpause	Unpause a paused container	取消暂停容器
version	show the docker version information	查看docker版本号
wait	Block until a container stops，then print its exit code	截取容器停止时的退出状态值

# 作业一

```
docker安装Nginx
```

```shell
#1.搜索镜像  (网站搜索)
#2.拉取镜像（下载）
#3.运行测试
[root@localhost ~]# docker images
REPOSITORY    TAG       IMAGE ID       CREATED         SIZE
nginx         latest    904b8cb13b93   2 days ago      142MB
mysql         latest    4f06b49211c0   8 days ago      530MB
hello-world   latest    feb5d9fea6a5   17 months ago   13.3kB
centos        latest    5d0da3dc9764   17 months ago   231MB

#-d 后台运行
#--name 给容器命名
#-p 宿主机端口:容器内部端口
[root@localhost ~]# docker run -d --name nginx01 -p 3344:80 nginx
750af31ad6ab99b558d8f0acbdaeea0bcf08e80d7f3b34f08302ce5808fe62cd
[root@localhost ~]# docker ps
CONTAINER ID   IMAGE     COMMAND                   CREATED         STATUS         PORTS                                   NAMES
750af31ad6ab   nginx     "/docker-entrypoint.…"   7 seconds ago   Up 7 seconds   0.0.0.0:3344->80/tcp, :::3344->80/tcp   nginx01
[root@localhost ~]# curl localhost:3344


#进入容器
[root@localhost ~]# docker exec -it 750af31ad6ab /bin/bash
root@750af31ad6ab:/# whereis nginx
nginx: /usr/sbin/nginx /usr/lib/nginx /etc/nginx /usr/share/nginx
root@750af31ad6ab:/# cd /etc/nginx
root@750af31ad6ab:/etc/nginx# ls
conf.d	fastcgi_params	mime.types  modules  nginx.conf  scgi_params  uwsgi_params

```

端口暴露的概念

![img](https://img-blog.csdnimg.cn/20201006021818734.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzI0NjIxNQ==,size_16,color_FFFFFF,t_70#pic_center)

# 作业二

```
docker 安装一个tomcat
```

```shell
#官方的使用
$ docker run -it --rm tomcat:9.0

#我们之前的启动都是后台，停止了容器之后，容器还是可以查到docker run -it --rm tomcat:9.0 一般用来测试，用完就删,只是删容器而已

#下载在启动

$ docker pull tomcat:9.0

#启动运行
docker run -d -p 3355:8080 --name tomcat01 tomcat

#测试访问没有问题

#进入容器
[root@localhost ~]# docker exec -it tomcat01 /bin/bash
root@a23ea7f5c7f0:/usr/local/tomcat# ls
bin  BUILDING.txt  conf  CONTRIBUTING.md  lib  LICENSE  logs  native-jni-lib  NOTICE  README.md  RELEASE-NOTES  RUNNING.txt  temp  webapps  webapps.dist  work

#发现问题: 1.linux命令少了.2.webapps里面没有东西,阿里云镜像的原因，默认是最小的镜像，所有不必要的都剔除掉了
#保证最小可运行的环境


```

思考一个问题，我们以后每次要部署项目，如果每次都要进入容器是不是十分麻烦？我们可以在容器外提供一个映射路径，webapps，

我们在外部放置项目，就自动同步到内部就好了，docker容器一删除，里面的内容岂不是都没了



# 作业三

```
部署es+kibana
```

```shell
#es 暴露的端口很多!
#es 十分的耗内存
#es 的数据一般要放置到安全目录，挂载
# --net somenetwork ? 网络配置

#启动 elasticsearch
docker run -d --name elasticsearch  -p 9200:9200 -p 9300:9300 -e "discovery.type=single-node" elasticsearch:7.6.2

#启动了 linux服务器就卡住了

#es是十分耗内存的，1.xG 

#停止整个docker
#docker stats 查看占用多大内存


#测试一下es是否成功了
[root@localhost ~]# curl localhost:9200
{
  "name" : "44f1cf00fd70",
  "cluster_name" : "docker-cluster",
  "cluster_uuid" : "xHRemTzUR363-Li_xiEMFg",
  "version" : {
    "number" : "7.6.2",
    "build_flavor" : "default",
    "build_type" : "docker",
    "build_hash" : "ef48eb35cf30adf4db14086e8aabd07ef6fb113f",
    "build_date" : "2020-03-26T06:34:37.794943Z",
    "build_snapshot" : false,
    "lucene_version" : "8.4.0",
    "minimum_wire_compatibility_version" : "6.8.0",
    "minimum_index_compatibility_version" : "6.0.0-beta1"
  },
  "tagline" : "You Know, for Search"
}

```

![image-20230304161044909](C:\Users\cao'yang'lin\AppData\Roaming\Typora\typora-user-images\image-20230304161044909.png)

```shell
#赶紧关闭，增加内存的限制
docker run ----------------------------
```

# 可视化

portalner

# **docker镜像讲解**

## 镜像是什么？

镜像是一种轻量级的、可执行的独立软件包，用来打包软件运行环境和基于运行环境开发的软件，它包含运行某个软件所需要的所有内容，包括代码、运行时、库、环境变量和配置文件等等。

## 如何得到镜像？

- 从远程仓库下载镜像
- 从朋友那里拷贝镜像
- 自己制作一个镜像dockerFile

## Docker镜像加载原理

### （1）UnionFS（联合文件系统）

UnionFS（联合文件系统）：Union文件系统是一种分层、轻量级并且高性能的文件系统，它支持对文件系统的修改作为一次提交来一层层的叠加，同时可以讲不同目录挂载到同一个虚拟文件系统下（unite several directories into a single virtual filesystem）。Union文件系统是Docker镜像的基础。镜像可以通过分层来进行集成，基于基础镜像（没有父镜像），可以制作各种具体的应用镜像。

### （2）Docker镜像加载原理

docker的镜像实际上由一层一层的文件系统组成，这种层级的文件系统叫做UnionFS.

bootfs(boot file system)主要包含bootloader和kernel，bootloader主要是引导加载kernel，Linux刚启动时会加载bootfs文件系统，在Docker镜像的最底层是bootfs。这一层与我们典型的Linux/Unix系统是一样的，包含boot加载器和内核。当boot加载完成之后整个内核就都在内存中了，此时内存的使用权已由bootfs转交给内核，此时系统也会卸载bootfs。

rootfs (root file system)，在bootfs之上。包含的就是典型Linux系统中的/dev，/proc， /bin，letc等标准目录和文件。rootfs就是各种不同的操作系统发行版，比如Ubuntu，Centos等等。|
![img](https://img-blog.csdnimg.cn/20201007152652541.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzI0NjIxNQ==,size_16,color_FFFFFF,t_70#pic_center)

提问：平时我们安装虚拟机的Centos都是好几个G的，为什么Docker里面的Centos镜像只有200M左右呢？

回答：对于一个精简的OS， rootfs 可以很小，只需要包含最基本的命令，工具和程序库就可以了，因为底层直接用Host的kernel，自己只需要提供rootfs就可以了。由此可见对于不同的linux发行版, bootfs基本是一致的, rootfs会有差别，因此不同的发行版可以公用bootfs.

虚拟机是分钟级别的，而容器是秒级别的，区别就是因为以上解释。

## 镜像原理之分层理解

### （1）分层的镜像

当我们去下载一个镜像的时候，注意观察下载的日志输出，可以看到的是镜像是一层一层的下载的，如下所示：

![在这里插入图片描述](https://img-blog.csdnimg.cn/20201007152856152.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzI0NjIxNQ==,size_16,color_FFFFFF,t_70#pic_center)

思考：为什么Docker镜像要采用这种分层的结构呢？

最大的好处就是资源共享，例如多个镜像都是从相同的Base镜像构建而来的，那么宿主机只需要在磁盘上保留一份base镜像，同时内存中也只需要加载一份base镜像，这样就可以为所有的容器服务卡，而且每一层都可以被共享。就像上图中的第一项，就是base镜像，说明已经存在该镜像了，所以就不需要下载了。
而查看镜像分层的方式我们可以通过 docker image inspect 命令去查看

理解：
所有的Docker镜像都起始于一个基础镜像层，当进行修改或增加新的内容时，就会在当前镜像层之上，创建新的镜像层。

举一个简单的例子，假如基于Ubuntu Linux 16.04创建一个新的镜像，这就是新镜像的第一层；如果在该镜像中添加Python包，就会在基础镜像层之上创建第二个镜像层；如果继续添加一个安全补丁，就会创建第三个镜像层。
该镜像当前已经包含3个镜像层，如下图所示(这只是一个用于演示的很简单的例子）。

![在这里插入图片描述](https://img-blog.csdnimg.cn/2020100715305770.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzI0NjIxNQ==,size_16,color_FFFFFF,t_70#pic_center)

在添加额外的镜像层的同时，镜像始终保持是当前所有镜像的组合，理解这一点非常重要。下图中举了一个简单的例子，每个镜像层包含3个文件，而镜像包含了来自两个镜像层的6个文件。

![在这里插入图片描述](https://img-blog.csdnimg.cn/20201007153115746.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzI0NjIxNQ==,size_16,color_FFFFFF,t_70#pic_center)

下图中展示了一个稍微复杂的三层镜像，在外部看来整个镜像只有6个文件，这是因为最上层中的文件7是文件5的一个更新版本。

![在这里插入图片描述](https://img-blog.csdnimg.cn/20201007153231942.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzI0NjIxNQ==,size_16,color_FFFFFF,t_70#pic_center)


这种情况下，上层镜像层中的文件覆盖了底层镜像层中的文件。这样就使得文件的更新版本作为一个新镜像层添加到镜像当中。

Docker通过存储引擎（新版本采用快照机制)的方式来实现镜像层堆栈，并保证多镜像层对外展示为统一的文件系统。

Linux上可用的存储引擎有AUFS、Overlay2、Device Mapper、Btrfs以及ZFS。顾名思义，每种存储引擎都基于Linux中对应的文件系统或者块设备技术，并且每种存储引擎都有其独有的性能特点。

Docker在Windows上仅支持windowsfilter一种存储引擎，该引擎基于NTFS文件系统之上实现了分层和CoW[1]。

下图展示了与系统显示相同的三层镜像。所有镜像层堆叠并合并，对外提供统一的视图。

![在这里插入图片描述](https://img-blog.csdnimg.cn/20201007153313905.png#pic_center)

特点
Docker镜像都是只读的，当容器启动时，一个新的可写层被加载到镜像的顶部，这一次就是我们通常说的容器层，容器之下的都叫镜像层。

![在这里插入图片描述](https://img-blog.csdnimg.cn/20201007153416751.png#pic_center)

## Commit镜像（如何提交一个自己的镜像）

```shell
命令：docker commit #提交一个新的副本
命令和git原理类似
格式为：docker commit -m="提交的描述信息" -a="作者" 容器id 目标镜像名:[TAG版本号]
```

练习：封装一个Tomcat镜像

```shell
# 1、启动一个默认的tomcat；



# 2、发现这个默认的tomcat是没有webapps应用，镜像的原因，官方的镜像默认webapps下面是没有文件的；



# 3、我自己拷贝进去了基本的文件；

注意：前面三步不熟悉的话可以看上面的tomcat练习。

# 4、将我们操作过的容器通过commit提交为一个镜像!我们以后就使用我们修改过的镜像即可，这就是我们自己的一个修改的镜像

命令：docker commit -a="oldou" -m="add webapps app" 容器的ID tomcat02:版本号
$    docker commit -a="caoyanglin" -m="add WebApps app" a6e61bde8670 tomcat02:1.0
```

```shell
# 1、启动一个默认的tomcat；
# 2、发现这个默认的tomcat是没有webapps应用，镜像的原因，官方的镜像默认webapps下面是没有文件的；
# 3、我自己拷贝进去了基本的文件；

注意：前面三步不熟悉的话可以看上面的tomcat练习。

# 4、将我们操作过的容器通过commit提交为一个镜像!我们以后就使用我们修改过的镜像即可，这就是我们自己的一个修改的镜像
命令：docker commit -a="oldou" -m="add webapps app" 容器的ID tomcat02:版本号

```

![image-20230304183454796](C:\Users\cao'yang'lin\AppData\Roaming\Typora\typora-user-images\image-20230304183454796.png)

如果想要保存当前容器的状态，那么就可以通过`commit`来进行提交，获取一个镜像，这就好比VM的快照。

# 注意

**学到这里的时候，才算入门Docker，接下来想要对Docker了解更深，就继续往后学吧。**



# Docker容器数据卷的使用

## 什么是容器数据卷？

Docker的理念回顾：将应用和环境打包成一个镜像，如果数据都在容器中，那么当我们容器被删除的时候，数据就会丢失。【需求：数据可以持久化】。假如MYSQL数据库，如果容器被删除了，那么数据库内的数据就会丢失，因此我们希望：MySQL数据库中的数据可以存储在本地。

容器之间可以有一个数据共享的技术，Docker容器中产生的数据可以同步到本地。这就是卷技术，目录的挂载：就是将容器内的目录挂载到Linux上面。

![在这里插入图片描述](https://img-blog.csdnimg.cn/20201007154257591.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzI0NjIxNQ==,size_16,color_FFFFFF,t_70#pic_center)

**总结：容器的持久化和同步操作，容器间也是数据共享的。**

如何使用数据卷？
方式一：直接使用命令来挂载 -v

```shell
命令格式：docker run -it -v 主机目录 : 容器内目录
```

测试

第一步：我们使用以下命令连接容器，并且将Linux的/home/ceshi目录和容器内的/home目录连接起来，如果没有ceshi目录就会自动创建一个。

**命令：**`docker run -it -v /home/ceshi:/home centos /bin/bash`

![img](https://img-blog.csdnimg.cn/20201007154638245.png#pic_center)

做完以上的操作，这个时候我们在容器内对/home目录下的操作会被同步到Linux的/home/ceshi目录下

第二步：当容器启动起来的时候，我们在Linux的操作命令窗口处通过 docker inspect 容器id去查看卷的挂载信息
命令：docker inspect centos容器的id
![在这里插入图片描述](https://img-blog.csdnimg.cn/20201007154828369.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzI0NjIxNQ==,size_16,color_FFFFFF,t_70#pic_center)

- 以上两个目录的数据会进行同步，例如我在主机内的ceshi目录下做一些操作【增、删、改等等】会同步到docker容器内的home目录下。

**注意**：如果没有上图中的这个挂载项，就说明挂载失败了，重新再挂载一下。下面我们进行数据同步测试。

## 测试文件同步

**1、测试容器中的数据会不会同步到主机中**

![在这里插入图片描述](https://img-blog.csdnimg.cn/20201007154928189.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzI0NjIxNQ==,size_16,color_FFFFFF,t_70#pic_center)



![image-20230304192514439](C:\Users\cao'yang'lin\AppData\Roaming\Typora\typora-user-images\image-20230304192514439.png)

**结果证明**，我们在容器中做了一个添加test.java文件的操作，数据会被同步到主机的对应目录下，这就是双向绑定。

好处：我们以后修改只需要在本地修改即可，容器内会自动同步!

# 实战：MySQL同步数据

我们来实现一下将MySQL容器中的数据同步到我们的Linux中，同时实现用Windows电脑上的Navicat连接上Linux上的MySQL容器。

官网：https://hub.docker.com/_/mysql

思考：Mysql的数据持久化的问题

```shell

#官方的
$ docker run --name some-mysql -e MYSQL_ROOT_PASSWORD=my-secret-pw -d mysql:tag

#启动我们的
-d 后台运行
-p 端口映射
-v 数据卷挂载
-e 环境配置
--name 容器名字

[root@localhost home]# docker run -d -p 3310:3306 -v /home/mysql/conf:/etc/mysql/conf.d -v /home/mysql/data:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=123456 --name mysql01 mysql
a29ed558ac18302d44d2dd4a5042e22b155e4dfbcb5e8a5239a9914f22c9de6c

```

6.4、具名和匿名挂载
## 匿名挂载
```
-v 容器内路径！
docker run -d -p --name nginx01 -v /etc/nginx nginx

# 查看所有的volume的情况
```



```shell


[root@iZ8vbgc3u6dvwrjyp45lyrZ lib]# docker volume ls
DRIVER VOLUME NAME
local 3df3ebf883092323908b31e21c761b56c937ee04ed51d418eedcc10df8d5f20a
# 这里发现，这种就是匿名挂载，我们在 -v 只写了容器内的路径，没有写容器外的路径！
匿名就是没有名字

# 具名挂载

➜ ~ docker run -d -P --name nginx02 -v juming-nginx:/etc/nginx nginx
➜ ~ docker volume ls
DRIVER VOLUME NAME
local juming-nginx

# 通过 -v 卷名：容器内路径
# 查看一下这个卷
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/20210722142200514.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3N1MjIzMTU5NTc0Mg==,size_16,color_FFFFFF,t_70)

所有的docker容器内的卷，没有指定目录的情况下都是在 `/var/lib/docker/volumes/xxx/_data`

以/开头的就是从根目录开始搜索

我们通过具名挂载可以方便的找到我们的 一个卷，大多数情况使用的是 具名挂载

```shell
# 如何确定是具名挂载还是匿名挂载，还是指定路径挂载！
-v 容器内路径 # 匿名挂载
-v 卷名:容器内路径 # 具名挂载
-v /宿主机路径:容器路径 # 指定路径挂载！
```

拓展：

```shell
# 通过 -v 容器内路径： ro rw 改变读写权限
ro readonly # 只读
rw readwrite # 可读可写
 
# 一旦设置了容器权限，容器对我们挂载出来的内容就有限定了！
docker run -d -P --name nginx05 -v juming:/etc/nginx:ro nginx
docker run -d -P --name nginx05 -v juming:/etc/nginx:rw nginx
 
# ro 只要看到ro就说明这个路径只能通过宿主机来操作，容器内部是无法操作！
```

## 6.5、初识Dockerfile

Dockerfile 就是用来构建docker镜像的构建文件！

通过这个脚本可以生成镜像，镜像是一层一层的，脚本就是一个一个的命令

```shell
# 创建一个dockerfile文件，名字可以随机 建议 Dockerfile
# 文件中的内容 指令（大写）参数
FROM centos
 
VOLUME ["/volume01", "/volume02"]  匿名挂载
 
CMD echo "----end----------"
CMD /bin/bash
 
# 这里的每个命令，就是镜像的一层！

```

![image-20230305213905272](C:\Users\cao'yang'lin\AppData\Roaming\Typora\typora-user-images\image-20230305213905272.png)

启动自己写的镜像

![image-20230305214456435](C:\Users\cao'yang'lin\AppData\Roaming\Typora\typora-user-images\image-20230305214456435.png)

这个卷和外部一定有一个同步的目录！

![img](https://img-blog.csdnimg.cn/20210722155132469.png)

查看一下卷挂载的路径

```shell
docker inspect 容器id
```

![image-20230305215547303](C:\Users\cao'yang'lin\AppData\Roaming\Typora\typora-user-images\image-20230305215547303.png)

测试一下刚才的文件是否同步出去了！

这种方式使用的十分多，因为我们通常会构建自己的镜像！

假设构建镜像时候没有挂载卷，要手动镜像挂载 -v 卷名：容器内路径！

## 6.6、数据卷容器

多个MySQL同步数据！

命名的容器挂载数据卷！

![img](https://img-blog.csdnimg.cn/img_convert/509123ae482041b594dff90c81dd799c.png)

启动3个容器，通过我们刚才自己写的镜像启动

![image-20230305222949668](C:\Users\cao'yang'lin\AppData\Roaming\Typora\typora-user-images\image-20230305222949668.png)     

```shell
--volumes-from list Mount volumes from the specified container(s)
# 测试，
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/img_convert/ade6838d7b0150f2678468edc41bf86c.png)

![image-20230305223710650](C:\Users\cao'yang'lin\AppData\Roaming\Typora\typora-user-images\image-20230305223710650.png)

![image-20230305223725192](C:\Users\cao'yang'lin\AppData\Roaming\Typora\typora-user-images\image-20230305223725192.png)

```shell
# 测试，可以删除docker01，查看一下docker02 和 docker03 是否还可以访问这个文件
# 测试依旧可以访问
```

![img](https://img-blog.csdnimg.cn/4d1a976f0ff841e5a046a37d999303a9.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3N1MjIzMTU5NTc0Mg==,size_16,color_FFFFFF,t_70)

多个mysql实现数据共享

```shell
➜ ~ docker run -d -p 3306:3306 -v /home/mysql/conf:/etc/mysql/conf.d -v /home/mysql/data:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=123456 --name mysql01 mysql:5.7
 
➜ ~ docker run -d -p 3307:3306 -e MYSQL_ROOT_PASSWORD=123456 --name mysql02 --volumes-from mysql01 mysql:5.7
# 这个时候，可以实现两个容器数据同步！
```

结论：

容器之间的配置信息的传递，数据卷容器的生命周期一直持续到没有容器使用为止。

但是一旦你持久化到了本地，这个时候，本地的数据是不会删除的！

# 七、DockerFile

### 7.1、DockerFile介绍

dockerfile 是用来构建docker镜像的文件！命令参数脚本！

构建步骤：

1、 编写一个dockerfile文件

2、 docker build 构建称为一个镜像

3、 docker run运行镜像

4、 docker push发布镜像（DockerHub 、阿里云仓库)
![在这里插入图片描述](https://img-blog.csdnimg.cn/3e9dde477bcd4f10a93d106af5501e81.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3N1MjIzMTU5NTc0Mg==,size_16,color_FFFFFF,t_70)

![在这里插入图片描述](https://img-blog.csdnimg.cn/765a0bd85ff947fcb008bfc88ecf9cab.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3N1MjIzMTU5NTc0Mg==,size_16,color_FFFFFF,t_70)

但是很多官方镜像都是基础包，很多功能没有，我们通常会自己搭建自己的镜像！

官方既然可以制作镜像，那我们也可以！



### 7.2、DockerFile构建过程

基础知识：

1、每个保留关键字(指令）都是必须是大写字母

2、执行从上到下顺序

3、#表示注释

4、每一个指令都会创建提交一个新的镜像曾，并提交！

![在这里插入图片描述](https://img-blog.csdnimg.cn/c40a1beeb33140e687c92a3ef54a0680.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3N1MjIzMTU5NTc0Mg==,size_16,color_FFFFFF,t_70)

Dockerfile是面向开发的，我们以后要发布项目，做镜像，就需要编写dockerfile文件，这个文件十分简单！

Docker镜像逐渐成企业交付的标准，必须要掌握！

DockerFile：构建文件，定义了一切的步骤，源代码

DockerImages：通过DockerFile构建生成的镜像，最终发布和运行产品。

Docker容器：容器就是镜像运行起来提供服务

### 7.3、DockerFile常用指令

```shell
FROM # 基础镜像，一切从这里开始构建
MAINTAINER # 镜像是谁写的， 姓名+邮箱
RUN # 镜像构建的时候需要运行的命令
ADD # 步骤，tomcat镜像，这个tomcat压缩包！添加内容 添加同目录
WORKDIR # 镜像的工作目录
VOLUME # 挂载的目录
EXPOSE # 保留端口配置
CMD # 指定这个容器启动的时候要运行的命令，只有最后一个会生效，可被替代。
ENTRYPOINT # 指定这个容器启动的时候要运行的命令，可以追加命令
ONBUILD # 当构建一个被继承 DockerFile 这个时候就会运行ONBUILD的指令，触发指令。
COPY # 类似ADD，将我们文件拷贝到镜像中
ENV # 构建的时候设置环境变量！
```

### 7.4、实战测试

Docker Hub中 99% 镜像都是从这个基础镜像过来的`FROM scratch` , 然后配置需要的软件和配置来进行的构建

![img](https://img-blog.csdnimg.cn/1e323c4feaf9415cbc0a79e7e2418c90.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3N1MjIzMTU5NTc0Mg==,size_16,color_FFFFFF,t_70)

创建一个自己的centos

```shell

# 1.编写Dockerfile文件

-rw-r--r--. 1 root root 211 3月   6 08:08 mydockerfile-centos
[root@localhost dockerfile]# cat mydockerfile-centos
from centos
MAINTAINER caoyanglin<3347004610@qq.com>

ENV MYPATH /usr/local
WORKDIR $MYPATH

RUN yun -y install vim
RUN yun -y install net-tools

EXPOSE 80

CMD echo $MYPATH
CMD echo "---end---"
CMD /bin/bash

# 2、通过这个文件构建镜像
# 命令 docker build -f 文件路径 -t 镜像名:[tag] .
docker build -f mydockerfile-centos -t mycentos:0.1 .
 
Successfully built f22b7b27d5d2
Successfully tagged mycentos:0.1
 
# 3、测试运行
docker images                                               
docker run -it mycentos:0.1
```

对比：之前的原生的centos

![img](https://img-blog.csdnimg.cn/77f72fde47d945708933e95b6bb2fb7a.png)

我们增加之后的镜像

![img](https://img-blog.csdnimg.cn/886c3935a4e74b8198ba8750866fe32c.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3N1MjIzMTU5NTc0Mg==,size_16,color_FFFFFF,t_70)

我们平时拿到一个镜像，可以研究一下它是怎么做的？

### docker history查看更改的镜像软件

![img](https://img-blog.csdnimg.cn/0911c9df057342489a5ed0318a68d494.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3N1MjIzMTU5NTc0Mg==,size_16,color_FFFFFF,t_70)

CMD 和 ENTRYPOINT区别

```shell
CMD # 指定这个容器启动的时候要运行的命令，只有最后一个会生效，可被替代。
ENTRYPOINT # 指定这个容器启动的时候要运行的命令，可以追加命令
```

#### 测试cmd

```shell
# 编写dockerfile文件
$ vim dockerfile-test-cmd
 
FROM centos
CMD ["ls","-a"]
 
# 构建镜像
$ docker build -f dockerfile-test-cmd -t cmd-test:0.1 .
 
# 运行镜像
$ docker run cmd-test:0.1
.
..
.dockerenv
bin
dev
 
# 想追加一个命令 -l 成为ls -al
$ docker run cmd-test:0.1 -l
docker: Error response from daemon: OCI runtime create failed:container_linux.go:349: starting container process caused "exec: \"-l\":executable file not found in $PATH": unknown.
ERRO[0000] error waiting for container: context canceled
 
# cmd的情况下 -l 替换了CMD["ls","-l"]。 -l 不是命令所有报错
```

#### 测试ENTRYPOINT

```shell
# 编写dockerfile文件
$ vim dockerfile-test-entrypoint
 
FROM centos
ENTRYPOINT ["ls","-a"]
 
$ docker run entrypoint-test:0.1
.
..
.dockerenv
bin
dev
etc
home
lib
lib64
lost+found ...
 
# 我们的命令，是直接拼接在我们得ENTRYPOINT命令后面的
$ docker run entrypoint-test:0.1 -l
total 56
drwxr-xr-x 1 root root 4096 May 16 06:32 .
drwxr-xr-x 1 root root 4096 May 16 06:32 ..
-rwxr-xr-x 1 root root 0 May 16 06:32 .dockerenv
lrwxrwxrwx 1 root root 7 May 11 2019 bin -> usr/bin
drwxr-xr-x 5 root root 340 May 16 06:32 dev
drwxr-xr-x 1 root root 4096 May 16 06:32 etc
drwxr-xr-x 2 root root 4096 May 11 2019 home
lrwxrwxrwx 1 root root 7 May 11 2019 lib -> usr/lib
lrwxrwxrwx 1 root root 9 May 11 2019 lib64 -> usr/lib64 ....
```

Dockerfile中很多命令都十分的相似，我们需要了解它们的区别，我们最好的学习就是对比他们然后测试效果！

### 7.5、实战：Tomcat镜像

1、准备镜像文件

准备tomcat 和 jdk到当前目录，编写好README 。

2、编写dokerfile

```shell
FROM centos #
MAINTAINER cheng<1204598429@qq.com>
COPY README /usr/local/README #复制文件
ADD jdk-8u231-linux-x64.tar.gz /usr/local/ #复制解压
ADD apache-tomcat-9.0.35.tar.gz /usr/local/ #复制解压
RUN yum -y install vim
ENV MYPATH /usr/local #设置环境变量
WORKDIR $MYPATH #设置工作目录
ENV JAVA_HOME /usr/local/jdk1.8.0_231 #设置环境变量
ENV CATALINA_HOME /usr/local/apache-tomcat-9.0.35 #设置环境变量
ENV PATH $PATH:$JAVA_HOME/bin:$CATALINA_HOME/lib #设置环境变量 分隔符是：
EXPOSE 8080 #设置暴露的端口
CMD /usr/local/apache-tomcat-9.0.35/bin/startup.sh && tail -F /usr/local/apache-tomcat-9.0.35/logs/catalina.out # 设置默认命令
```

```shell
FROM centos:7
MAINTAINET caoyanglin<3347003610@qq.com>
COPY readme.txt /usr/local/readme.txt
ADD jdk-18_linux-x64_bin.rpm /usr/local
ADD apache-tomcat-9.0.73.tar.gz /usr/local

RUN yum -y install vim

ENV MYPATH /usr/local
WORK $MYPATH

ENV JAVA_HOME /usr/local/jdk1.8.0_202
ENV CLASSPATH $JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar
ENV CATALINA_HOME /usr/local/apache-tomcat-9.0.73
ENV CATALINA_BASH /usr/local/apache-tomcat-9.0.73
ENV PATH $PATH:$JAVA_HOME/bin:$CATALINA_HOME/lib:$CATALINA_HOME/bin

EXPOSE 8080

CMD /usr/local/apache-tomcat-9.0.73/bin/startup.sh && tail -F /url/local/apache-tomcat-9.0.73/bin/logs/catalina.out

```

3、构建镜像

```shell
# 因为dockerfile命名使用默认命名 因此不用使用-f 指定文件
 
$ docker build -t mytomcat:0.1 .
$ docker build -t diytomcat .
```

4、run镜像

```shell
$ docker run -d -p 8080:8080 --name tomcat01 -v /home/kuangshen/build/tomcat/test:/usr/local/apache-tomcat-9.0.35/webapps/test -v /home/kuangshen/build/tomcat/tomcatlogs/:/usr/local/apache-tomcat-9.0.35/logs
mytomcat:0.1
```

5、访问测试

6、发布项目(由于做了卷挂载，我们直接在本地编写项目就可以发布了！)

发现：项目部署成功，可以直接访问！

我们以后开发的步骤：需要掌握Dockerfile的编写！我们之后的一切都是使用docker镜像来发布运行！

### 7.6、发布自己的镜像

1、地址 https://hub.docker.com/

2、确定这个账号可以登录

3、登录

```shell
$ docker login --help
Usage: docker login [OPTIONS] [SERVER]
Log in to a Docker registry.
If no server is specified, the default is defined by the daemon.
Options:
-p, --password string Password
--password-stdin Take the password from stdin
-u, --username string Username
```

4、提交 push镜像.

```shell
# push自己的镜像到服务器上！
$ docker push diytomcat
```

![img](https://img-blog.csdnimg.cn/33e5c9d809c049e59bf62d2e455535cd.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3N1MjIzMTU5NTc0Mg==,size_16,color_FFFFFF,t_70)

## 八、Docker 网络

![image-20230417115717488](C:\Users\cao'yang'lin\AppData\Roaming\Typora\typora-user-images\image-20230417115717488.png)

### 8.1、理解Docker 0

#### 清空所有网络

三个网络

![img](https://img-blog.csdnimg.cn/94d1f7f7ffd74e13a8f055ce6dc9c6e4.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3N1MjIzMTU5NTc0Mg==,size_16,color_FFFFFF,t_70)

问题： docker 是如果处理容器网络访问的？

```shell
# 测试 运行一个tomcat
$ docker run -d --name tomcat01 tomcat
 
$ ip addr
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
inet 127.0.0.1/8 scope host lo
valid_lft forever preferred_lft forever
2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast state UP group default qlen 1000
link/ether 00:16:3e:13:78:90 brd ff:ff:ff:ff:ff:ff
inet 172.23.104.112/20 brd 172.23.111.255 scope global dynamic eth0
valid_lft 314146894sec preferred_lft 314146894sec
3: docker0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP group default
link/ether 02:42:c9:5a:27:6c brd ff:ff:ff:ff:ff:ff
inet 172.17.0.1/16 brd 172.17.255.255 scope global docker0
valid_lft forever preferred_lft forever
441: veth049f362@if440: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue master docker0 state UP group default
link/ether ea:55:6c:48:c4:7e brd ff:ff:ff:ff:ff:ff link-netnsid 0
 
$ docker exec -it 容器id
$ ip addr
# 查看容器内部网络地址 发现容器启动的时候会得到一个 eth0@if551 ip地址，docker分配的！
550: eth0@if551: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue
state UP group default
link/ether 02:42:ac:11:00:02 brd ff:ff:ff:ff:ff:ff link-netnsid 0
inet 172.17.0.2/16 brd 172.17.255.255 scope global eth0
valid_lft forever preferred_lft forever
# 思考？ linux能不能ping通容器内部！ 可以 容器内部可以ping通外界吗？ 可以！
$ ping 172.17.0.2
PING 172.17.0.2 (172.17.0.2) 56(84) bytes of data.
64 bytes from 172.17.0.2: icmp_seq=1 ttl=64 time=0.069 ms
64 bytes from 172.17.0.2: icmp_seq=2 ttl=64 time=0.074 ms
 
# linux 可以ping 通docker容器内部
```

#### **原理**

1、我们每启动一个docker容器，Docker就会给docker容器分配一个ip，我们只要安装了docker，就会有一个docker0桥接模式，使用的技术是 veth-pair 技术！

再次测试ip addr

![img](https://img-blog.csdnimg.cn/7c612b1f3ff949e587e96a48a6ab584f.png)

#### 2 、在启动一个容器测试，发现又多了一对网络

![img](https://img-blog.csdnimg.cn/f170b48be44743ae9877c723fc7248a2.png)

我们发现这个容器带来网卡，都是一对对的

veth-pair 就是一对的虚拟设备接口，他们都是成对出现的，一端连着协议，一端彼此相连，正因为有这个特性 veth-pair 充当一个桥梁，连接各种虚拟网络设备的OpenStac,Docker容器之间的连接，OVS的连接，都是使用evth-pair技术

#### 3、我们来测试下tomcat01和tomcat02是否可以ping通

```shell
$ docker-tomcat docker exec -it tomcat01 ip addr #获取 tomcat01 的ip
172.17.0.2
550: eth0@if551: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue
state UP group default
link/ether 02:42:ac:11:00:02 brd ff:ff:ff:ff:ff:ff link-netnsid 0
inet 172.17.0.2/16 brd 172.17.255.255 scope global eth0
valid_lft forever preferred_lft forever
$ docker-tomcat docker exec -it tomcat02 ping 172.17.0.2 #让tomcat02 ping tomcat01
PING 172.17.0.2 (172.17.0.2) 56(84) bytes of data.
64 bytes from 172.17.0.2: icmp_seq=1 ttl=64 time=0.098 ms
64 bytes from 172.17.0.2: icmp_seq=2 ttl=64 time=0.071 ms
 
# 结论：容器和容器之间是可以互相ping通的
```

![img](https://img-blog.csdnimg.cn/cce22e1584b349f69aa07c6a01ad9d1e.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3N1MjIzMTU5NTc0Mg==,size_16,color_FFFFFF,t_70)

结论：tomcat01和tomcat02公用一个路由器，docker0。

所有的容器不指定网络的情况下，都是docker0路由的，docker会给我们的容器分配一个默认的可用ip。

小结： Docker使用的是Linux的桥接，宿主机是一个Docker容器的网桥 docker0
![img](https://img-blog.csdnimg.cn/690de016b877403296c0ec5edd23e370.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3N1MjIzMTU5NTc0Mg==,size_16,color_FFFFFF,t_70)

Docker 中的所有的网络接口都是虚拟的。虚拟的转发效率高！

只要容器删除，对应网桥一对就没了！

![img](https://img-blog.csdnimg.cn/16e851ba1eb142059cb0461d5ecc2f30.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3N1MjIzMTU5NTc0Mg==,size_16,color_FFFFFF,t_70)

思考一个场景：我们编写了一个微服务，database url=ip: ，项目不重启，数据库ip换了，我们希望可以处理这个问题，可以通过名字来进行访问容器？

### 8.2、–link

```shell
$ docker exec -it tomcat02 ping tomca01 # ping不通ping: tomca01: Name or service not known# 运行一个tomcat03 --link tomcat02$ docker run -d -P --name tomcat03 --link tomcat02 tomcat5f9331566980a9e92bc54681caaac14e9fc993f14ad13d98534026c08c0a9aef# 用tomcat03 ping tomcat02 可以ping通$ docker exec -it tomcat03 ping tomcat02PING tomcat02 (172.17.0.3) 56(84) bytes of data.64 bytes from tomcat02 (172.17.0.3): icmp_seq=1 ttl=64 time=0.115 ms64 bytes from tomcat02 (172.17.0.3): icmp_seq=2 ttl=64 time=0.080 ms# 用tomcat02 ping tomcat03 ping不通
```

**探究：** docker network inspect 网络id 网段相同
docker inspect tomcat03

![在这里插入图片描述](https://img-blog.csdnimg.cn/16e851ba1eb142059cb0461d5ecc2f30.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3N1MjIzMTU5NTc0Mg==,size_16,color_FFFFFF,t_70)

其实这个tomcat03 就是本地配置了tomcat02的配置？

![img](https://img-blog.csdnimg.cn/ac76669d0bae4229914b73e2ffdf98a9.png)

–link 本质就是在hosts配置中添加映射

现在使用Docker已经不建议使用–link了！

自定义网络，不使用docker0！

docker0问题：不支持容器名连接访问！

### 8.3、自定义网络

```shell
$ docker network --help
connect -- Connect a container to a network
create -- Creates a new network with a name specified by the
disconnect -- Disconnects a container from a network
inspect -- Displays detailed information on a network
ls -- Lists all the networks created by the user
prune -- Remove all unused networks
rm -- Deletes one or more networks
```

#### 查看所有的docker网络

![img](https://img-blog.csdnimg.cn/04d730e68bd844809461e19c9482c9ad.png)

#### **网络模式**

bridge ：桥接 docker（默认，自己创建也是使用bridge模式）

none ：不配置网络，一般不用

host ：和所主机共享网络

container ：容器网络连通（用得少！局限很大）

**测试**

```shell
# 我们直接启动的命令 --net bridge,而这个就是我们得docker0
# bridge就是docker0
$ docker run -d -P --name tomcat01 tomcat
等价于 => docker run -d -P --name tomcat01 --net bridge tomcat
 
# docker0，特点：默认，域名不能访问。 --link可以打通连接，但是很麻烦！
 
# 我们可以 自定义一个网络
# --driver bridge
# --subnet 192.168.0.0/16 子网
# --gateway 192.168.0.1 网关
$ docker network create --driver bridge --subnet 192.168.0.0/16 --gateway 192.168.0.1 mynet
```

![img](https://img-blog.csdnimg.cn/5101c9a64b8844948d2a1f74144db313.png)

```shell
$ docker network inspect mynet
```

![img](https://img-blog.csdnimg.cn/f7695ce6d1e041e5ad49c5ae36ff3ef9.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3N1MjIzMTU5NTc0Mg==,size_16,color_FFFFFF,t_70)

启动两个tomcat,再次查看网络情况

```shell
[root@iZ8vbgc3u6dvwrjyp45lyrZ ~]# docker run -d -P --name tomcat-net-01 --net mynet tomcat
8f3b8236b5d9d149612d1dbe6b533c21601cfd7392cb5bf226a8427b5fc1b3e3
[root@iZ8vbgc3u6dvwrjyp45lyrZ ~]# docker run -d -P --name tomcat-net-02 --net mynet tomcat
3279bc773cacaa51368f4417e42159732f046c0d300ce881fb0a598663e79779
 
 
[root@iZ8vbgc3u6dvwrjyp45lyrZ ~]# docker network inspect mynet
[
{
"Name": "mynet",
"Id": "be05f1f6f6909cee0d1e868acb718c47c3e2efb9f5f33ccc38b6955ae6fb3578",
"Created": "2021-07-26T11:11:10.09948571+08:00",
"Scope": "local",
"Driver": "bridge",
"EnableIPv6": false,
"IPAM": {
"Driver": "default",
"Options": {},
"Config": [
{
"Subnet": "192.168.0.0/16",
"Gateway": "192.168.0.1"
}
]
},
"Internal": false,
"Attachable": false,
"Ingress": false,
"ConfigFrom": {
"Network": ""
},
"ConfigOnly": false,
"Containers": {
"3279bc773cacaa51368f4417e42159732f046c0d300ce881fb0a598663e79779": {
"Name": "tomcat-net-02",
"EndpointID": "0d31467ee4bc86d1b55d1889a07b468b57aeb82a9b23bbb2e2df5632d158ac0f",
"MacAddress": "02:42:c0:a8:00:03",
"IPv4Address": "192.168.0.3/16",
"IPv6Address": ""
},
"8f3b8236b5d9d149612d1dbe6b533c21601cfd7392cb5bf226a8427b5fc1b3e3": {
"Name": "tomcat-net-01",
"EndpointID": "7ae56746e954749dfd52c5f2965cc667d307b198f792175cca80040aed59eb52",
"MacAddress": "02:42:c0:a8:00:02",
"IPv4Address": "192.168.0.2/16",
"IPv6Address": ""
}
},
"Options": {},
"Labels": {}
}
]
 
 
# 再次测试 ping 连接
[root@iZ8vbgc3u6dvwrjyp45lyrZ ~]# docker exec -it tomcat-net-01 ping 192.168.0.3
PING 192.168.0.3 (192.168.0.3) 56(84) bytes of data.
64 bytes from 192.168.0.3: icmp_seq=1 ttl=64 time=0.135 ms
64 bytes from 192.168.0.3: icmp_seq=2 ttl=64 time=0.099 ms
 
# 现在不使用--link也可以ping名字了
[root@iZ8vbgc3u6dvwrjyp45lyrZ ~]# docker exec -it tomcat-net-01 ping tomcat-net-02
PING tomcat-net-02 (192.168.0.3) 56(84) bytes of data.
64 bytes from tomcat-net-02.mynet (192.168.0.3): icmp_seq=1 ttl=64 time=0.095 ms
64 bytes from tomcat-net-02.mynet (192.168.0.3): icmp_seq=2 ttl=64 time=0.108 ms
64 bytes from tomcat-net-02.mynet (192.168.0.3): icmp_seq=3 ttl=64 time=0.093 ms
```

在自定义的网络下，服务可以互相ping通，不用使用–link

我们自定义的网络docker当我们维护好了对应的关系，推荐我们平时这样使用网络！

好处：

- redis -不同的集群使用不同的网络，保证集群是安全和健康的
- mysql-不同的集群使用不同的网络，保证集群是安全和健康的

![img](https://img-blog.csdnimg.cn/6184a7c2d3b3460983a5463dafb0f05f.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3N1MjIzMTU5NTc0Mg==,size_16,color_FFFFFF,t_70)

### 8.4、网络连通

![img](https://img-blog.csdnimg.cn/1d0f80c7903f469c8213b96ed5b5ef8e.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3N1MjIzMTU5NTc0Mg==,size_16,color_FFFFFF,t_70)

![img](https://img-blog.csdnimg.cn/44d046a5c4b74e6ebb4e890ba3067a7b.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3N1MjIzMTU5NTc0Mg==,size_16,color_FFFFFF,t_70)

```shell
# 测试两个不同的网络连通 再启动两个tomcat 使用默认网络，即docker0
$ docker run -d -P --name tomcat01 tomcat
$ docker run -d -P --name tomcat02 tomcat
# 此时ping不通
```

要将tomcat01 连通 tomcat—net-01 ，连通就是将 tomcat01加到 mynet网络

#### 一个容器两个ip（tomcat01）

![img](https://img-blog.csdnimg.cn/74df32fa98d74030bc7543cc36289c69.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3N1MjIzMTU5NTc0Mg==,size_16,color_FFFFFF,t_70)

```shell
# 01 连通ok
[root@iZ8vbgc3u6dvwrjyp45lyrZ ~]# docker exec -it tomcat01 ping tomcat-net-01
PING tomcat-net-01 (192.168.0.2) 56(84) bytes of data.
64 bytes from tomcat-net-01.mynet (192.168.0.2): icmp_seq=1 ttl=64 time=0.130 ms
64 bytes from tomcat-net-01.mynet (192.168.0.2): icmp_seq=2 ttl=64 time=0.097 ms
64 bytes from tomcat-net-01.mynet (192.168.0.2): icmp_seq=3 ttl=64 time=0.106 ms
64 bytes from tomcat-net-01.mynet (192.168.0.2): icmp_seq=4 ttl=64 time=0.109 ms
 
# 02 是依旧打不通的
[root@iZ8vbgc3u6dvwrjyp45lyrZ ~]# docker exec -it tomcat02 ping tomcat-net-01
ping: tomcat-net-01: Name or service not known
```

结论：假设要跨网络操作别人，就需要使用 docker network connect 连通！

### 8.5、实战：部署Redis集群

![img](https://img-blog.csdnimg.cn/5d90a471e0a34f2bafd51a05be204bf9.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3N1MjIzMTU5NTc0Mg==,size_16,color_FFFFFF,t_70)

```shell
# 创建网卡
docker network create redis --subnet 172.38.0.0/16
# 通过脚本创建六个redis配置
for port in $(seq 1 6);\
do \
mkdir -p /mydata/redis/node-${port}/conf
touch /mydata/redis/node-${port}/conf/redis.conf
cat << EOF >> /mydata/redis/node-${port}/conf/redis.conf
port 6379
bind 0.0.0.0
cluster-enabled yes
cluster-config-file nodes.conf
cluster-node-timeout 5000
cluster-announce-ip 172.38.0.1${port}
cluster-announce-port 6379
cluster-announce-bus-port 16379
appendonly yes
EOF
done
 
# 通过脚本运行六个redis
for port in $(seq 1 6);\
docker run -p 637${port}:6379 -p 1667${port}:16379 --name redis-${port} \
-v /mydata/redis/node-${port}/data:/data \
-v /mydata/redis/node-${port}/conf/redis.conf:/etc/redis/redis.conf \
-d --net redis --ip 172.38.0.1${port} redis:5.0.9-alpine3.11 redis-server /etc/redis/redis.conf
 
docker run -p 6371:6379 -p 16671:16379 --name redis-1 \
-v /mydata/redis/node-1/data:/data \
-v /mydata/redis/node-1/conf/redis.conf:/etc/redis/redis.conf \
-d --net redis --ip 172.38.0.11 redis:5.0.9-alpine3.11 redis-server /etc/redis/redis.conf
 
 docker run -p 6376:6379 -p 16676:16379 --name redis-6 \
-v /mydata/redis/node-6/data:/data \
-v /mydata/redis/node-6/conf/redis.conf:/etc/redis/redis.conf \
-d --net redis --ip 172.38.0.16 redis:5.0.9-alpine3.11 redis-server /etc/redis/redis.conf
 
docker exec -it redis-1 /bin/sh #redis默认没有bash
 
# 创建集群
redis-cli --cluster create 172.38.0.11:6379 172.38.0.12:6379 172.38.0.13:6379 172.38.0.14:6379 172.38.0.15:6379 172.38.0.16:6379 --cluster-replicas 1
```



# Use Docker Compose

```yml
services:
  app:
    image: node:18-alpine
    command: sh -c "yarn install && yarn run dev"
    ports:
      - 3000:3000
    working_dir: /app
    volumes:
      - ./:/app
    environment:
      MYSQL_HOST: mysql
      MYSQL_USER: root
      MYSQL_PASSWORD: secret
      MYSQL_DB: todos

  mysql:
    image: mysql:8.0
    volumes:
      - todo-mysql-data:/var/lib/mysql
    environment:
      MYSQL_ROOT_PASSWORD: secret
      MYSQL_DATABASE: todos

volumes:
  todo-mysql-data:
```



# 要通过 nicolaka/netshoot 容器来修改 nginx 的配置文件，可以按照以下步骤操作：

1. 运行 nicolaka/netshoot 容器并加入到与 nginx 相同的网络中：

   ```
   docker run -it --network=<nginx_network_name> nicolaka/netshoot
   ```

2. 使用 `nsenter` 命令进入 nginx 容器的命名空间：

   ```
   nsenter -t <nginx_container_pid> -n sh
   ```

   这里需要知道 ngin容器的PID，可以使用`docker inspect`获取

3. 在 nginx 配置文件所在目录下（一般是 `/etc/nginx/`）进行配置的修改。

4. 退出 `nsenter` 命令并离开容器。

5. 如果您使用了 Docker Compose，可以尝试在 `docker-compose.yaml` 文件中将 `nicolaka/netshoot` 容器定义为一个单独的服务，并将其连接到与 nginx 容器相同的网络中。例如:

   ```
   
   services:
     nginx:
       image: nginx
       networks:
         - mynetwork
       # other configuration
     netshoot:
       image: nicolaka/netshoot
       networks:
         - mynetwork
   networks:
     mynetwork:
   ```

   然后运行：

   ```
   docker-compose run netshoot nsenter -t <nginx_container_pid> -n sh
   ```

   就可以进入 nginx 容器的`sh`终端，开始对 nginx 配置进行修改了。

注意：实际使用时，需要将 `<nginx_network_name>` 和 `<nginx_container_pid>` 替换为您自己的值。此外，在修改nginx配置之前，建议您备份原始配置文件以避免不必要的损失。

如果您使用 `nsenter -t <nginx_container_pid> -n sh` 命令进入容器，但是发现里面没有容器里面的东西，可能是因为您没有进入容器的命名空间。在 `nsenter` 命令中，`-n` 选项只会进入容器的网络命名空间，而不会进入容器的其他命名空间（如挂载命名空间、进程命名空间等）。

要进入容器的所有命名空间，可以使用以下命令：

```
nsenter -t <nginx_container_pid> -m -u -i -n -p sh
```

该命令中，`-m` 选项表示进入容器的挂载命名空间，`-u` 选项表示进入容器的用户命名空间，`-i` 选项表示进入容器的 ipc 命名空间，`-n` 选项表示进入容器的网络命名空间，`-p` 选项表示进入容器的进程命名空间。

这样，您就可以完全进入容器的命名空间，查看容器中的所有内容。

# 注意

在 docker 19.03 版本之后，docker 的默认安全配置已更改，其中包括禁用了在容器中查看主机的 pid 命名空间。因此，在新版 docker 中，如果您尝试在容器中查看 `/proc/pid/ns/` 目录，可能会发现该目录为空。

如果您需要在容器中查看主机的 pid 命名空间，可以在创建容器时使用 `--pid=host` 选项，例如：

```
docker run --pid=host -it ubuntu /bin/bash
```

这将创建一个 ubuntu 容器，并在容器中启用主机的 pid 命名空间，使您可以查看主机的进程列表等信息。

请注意，启用主机的 pid 命名空间可能会增加安全风险，因此请仅在必要时使用。

在新版的 docker 中，命名空间是通过软连接的方式进行实现的。具体来说，docker 会在容器的 `/proc/<pid>/ns/` 目录下创建一系列软连接，这些软连接指向主机上对应的命名空间文件。例如，`/proc/1/ns/mnt` 软连接会指向主机上的 `/proc/1/ns/mnt` 文件。

通过这种方式，docker 可以在容器中使用主机上的命名空间，从而实现容器与主机之间的隔离。同时，docker 还可以通过创建新的命名空间来实现容器内部的隔离，例如网络命名空间、挂载命名空间等。

需要注意的是，如果您在容器内部查看 `/proc/<pid>/ns/` 目录，会发现其中的软连接指向的是主机上的文件。因此，如果您需要在容器内部查看容器自身的命名空间，可以使用 `readlink` 命令获取软连接指向的实际文件，例如：

```
readlink /proc/1/ns/mnt
```

该命令会返回容器内部的命名空间文件路径，而非主机上的文件路径。
