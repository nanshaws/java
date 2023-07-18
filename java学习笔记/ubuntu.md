# 在ubuntu下使用 apt-get install 或 apt install 下载安装软件

在ubuntu下使用 apt-get install 或 apt install 下载安装软件，

软件包：/var/cache/apt/archives
安装位置：/usr/share
快捷方式：/usr/share/applications
可执行文件：/usr/bin
lib文件：/usr/lib
配置文件：/etc
用下面的命令安装指定版本，

sudo apt-get install package=version
apt-get clean删除/var/cache/apt/archives/ 和 /var/cache/apt/archives/partial/目录下所有包(锁定的除外)。
apt-get autoclean仅删除不再能被下载的包。 