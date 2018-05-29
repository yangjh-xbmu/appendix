# Linux 操作系统

我们这里所说的服务器是指运行在互联网上，提供特定服务（如www、ftp等等）的一台或一组计算机。随着信息技术的发展，网络服务器经历了自建、托管、虚拟主机到现在的云主机，相比之前，云主机具有一系列的优势，如自主安装操作系统、自主搭设软件环境，用户自由度很高。因此，对于网络应用开发者而言，非常有必要掌握一定的服务器运维知识。

### Linux 简介

Linux是一个多用户多任务的自由和开放源代码的类UNIX操作系统。该操作系统的内核由Linus Torvalds在1991年10月5日首次发布。在加上一些应用程序之后，成为Linux操作系统，其主要大量运行在网络服务器上。绝大多数服务器选择Linux系列发行版作为操作系统，这样做得优势有二：一是安全稳定，二是免费。

严格来说，Linux不算是一个操作系统，是Linux系统中的内核，即与组成计算机的各种硬件（如CPU、内存、硬盘、键盘、网卡等等）进行通讯的平台。Linux操作系统的全称是GNU/Linux，GNU是Richard Stallman组织的自由软件项目，基于GNU发展出众多自由、开源软件，Linux就是其中的典型代表，基于GNU和Linux，又发展出了众多Linux发行版，如Redhat、Ubuntu、CentOS等等，所谓发行版，可以理解为针对特定目的（如个人桌面应用）基于Linux内核，集成必要软件（如浏览器、办公软件、电子邮件等等）的软件包，其中CentOS就是专门针对网络服务器的Linux发行版。

下面我们就以CentOS作为主要学习的操作系统。

### CentOS的安装

服务器端，我们通常可以选择云主机服务商提供的镜像，非常方便地安装。而在本地电脑中，大多数情况下操作系统为windows或mac，因此建议[通过虚拟机技术搭设CentOS开发环境](virtualmachine.html)，如使用Vagrant进行虚拟机的管理。

### 登录到服务器

登录到远程服务器，windows用户可以通过putty，mac用户可以在终端中使用ssh命令。

```sh
ssh root@10.10.2.2 //ssh 用户名@主机ip地址
```

登录到本地虚拟机，如果使用vagrant作为虚拟机管理工具的话，则使用如下命令即可登录：

```sh
vagrant ssh
```

### 用户管理

在Linux中，有三种用户：

1. root用户，也称为超级用户，对系统拥有完全的控制权限。
2. 系统用户，系统用户是Linux运行某些程序所必须的用户，如mail用户、sshd用户等。
3. 普通用户，普通用户对系统文件的访问受限，不能执行某些命令。

用户组，就是具有相同特征的用户的集合。一个组可以包含多个用户，每个用户也可以属于不同的组。

#### 与用户和组有关的系统文件

1. `/etc/passwd` 保存用户名和密码等信息。这个文件对所有用户都是可读的。
1. `/etc/group` 保存用户组的所有信息。

其中`/etc/passwd`文件的结构如下：

```sh
root   :*   :0      :0    :System Administrator :/var/root    :/bin/sh
vagrant:x   :1000   :1000 :vagrant              :/home/vagrant:/bin/bash
用户名 :密码:用户id :组id :描述信息             :用户主目录   :用户shell
```

用户id有以下几种：

1. 0 代表系统管理员。
1. 1-500 是系统预留id。
1. 500 以上是普通用户。

#### 查看登录到系统的用户

可以使用`users`、`who`和`w`命令来查看登录到系统的用户：

```sh
[vagrant@localhost ~]$ users
vagrant
[vagrant@localhost ~]$ who
vagrant  pts/0        May 29 08:28 (10.0.2.2)
[vagrant@localhost ~]$ w
 08:29:24 up 20 min,  1 user,  load average: 0.00, 0.01, 0.05
USER     TTY      FROM             LOGIN@   IDLE   JCPU   PCPU WHAT
vagrant  pts/0    10.0.2.2         08:28    4.00s  0.02s  0.00s w
```

另外，使用`whoami`可以查看当前用户名称：

```sh
[vagrant@localhost ~]$ whoami
vagrant
```

#### 管理用户和组

|命令|描述|
|----|----|
|useradd|添加用户|
|passwd|更改用户密码|
|uermode|修改用户信息|
|userdel|删除用户|
|groupadd|添加用户组|
|groupmod|修改用户组信息|
|groupdel|删除用户组|

### 常用命令

参见[命令行](commandline.html)章节内容。

### 文件管理

#### 文件类型

Linux中的所有数据都保存在文件中，所有的文件有被分配到不同的目录中，目录是一种类似于树结构的文件系统。在Linux中，有三种基本的文件类型：

1. 普通文件
1. 目录，目录也是一个文件，它的唯一功能就是保存文件及其相关信息。
1. 设备文件，Linux将外部设备视为一个文件，输入输出到外部设备的方式和输入输出到一个文件的方式是相同的。

#### 隐藏文件

在Linux中，隐藏文件的第一个字符为英文点`.`，隐藏文件通常用来保存配置信息。

#### 目录

Linux目录有清晰的层级结构，`\`表示根目录，所有的文件和目录都位于根目录之下。

用户登录到Linux后，所在的位置是主目录，用`~`表示。

### 文件权限和访问模式

#### 文件权限

文件权限是Linux系统的第一道安全防线，基本的权限有读取`r`、写入`w`和执行`x`。Linux系统为不同文件赋予不同权限，每个文件都可设定三类权限：

1. 所有者权限
1. 用户组权限
1. 其他用户权限

#### 查看权限

使用`ls -l`命令可以查看文件权限信息：

```sh
~/document/works/www/appendix />ls -l
total 184
-rw-r--r--   1 ncsxbmu  staff    146  5 28 12:13 FOOTER.md
-rw-r--r--   1 ncsxbmu  staff   9149  5 28 12:13 Howtolearn.md
-rw-r--r--   1 ncsxbmu  staff    424  5 28 12:13 README.md
```

其中`-rw-r--r--`中的`-`表示当前文件为普通文件，后面的字符每三个为一组，分别表示所有者权限、用户组权限和其他用户权限。例如：

1. `rw-` 表示所有者`ncsxbmu`拥有读取`r`和写入`w`权限，但是没有执行`x`权限；
1. `r--` 表示所有者`ncsxbmu`所在的用户组`staff`拥有读取权限，但是没有写入和执行权限；
1. `rw-` 表示其他用户拥有读取权限，但没有写入和执行权限；

#### 改变权限

chmod命令来改变文件的访问权限，可以使用`+`、`-`、`=`设定特定权限：

```sh
~/document/works/www/appendix />ls -l book.json
-rw-r--r--  1 ncsxbmu  staff  2182  5 28 12:13 book.json
~/document/works/www/appendix />chmod g=rwx book.json
~/document/works/www/appendix />ls -l book.json
-rw-rwxr--  1 ncsxbmu  staff  2182  5 28 12:13 book.json
```

|符号|说明|
|----|----|
|+|为文件增加权限|
|\-|删除文件权限|
|=|设定特定权限|
|u|代表文件拥有者|
|g|代表用户组|
|o|代表其他用户|

除了符号，还可以使用八进制数字来设定具体权限，如下表：

|数字|说明|权限|
|----|----|----|
|0|没有任何权限|`---`|
|1|执行权限|`--x`|
|2|写入权限|`-w-`|
|3|写入执行|`-wx`|
|4|读取权限|`r--`|
|5|读取执行|`r-x`|
|6|读取写入|`rw-`|
|7|所有权限|`rwx`|

例如：

```sh
chmod 755 filename
```

上述命令将设置文件拥有者拥有全部权限，所在用户组及其他用户拥有读取和执行的权限。

#### 更改所有者和用户组

在Linux中，所有用户都有用户名和群组，所有文件都有拥有者和群组。可以通过`chown`和`chgrp`来改变文件拥有者和所属群组。超级用户root可以不受限制地更改文件所有者和用户组，但是普通用户只能更改所有者是自己的文件。

```sh
chown user filelist
chgrp user filelist
```

### Linux环境变量

在Linux中，环境变量是一个很重要的概念，环境变量可以由系统、用户、shell以及其他程序来设定。变量就是一个被复制的字符串。登录系统后，shell会有一个初始化的过程，shell会读取`/etc/profile`和`/~/.profile`两个文件中的设置信息。

在主目录下的`.profile`文件，用户可以修改并增加一些个性化的初始化信息。

### 管道和过滤器

管道是Linux进程之间一种重要的通讯机制，除了管道，还有共享内存、消息队列、信号、套接字等进程通讯机制。使用管道，我们可以将一个命令的输出作为另一个命令的输入，使用`|`可以建立管道。另外，能够接受数据，过滤后再输出的工具，称为过滤器，常用过滤器命令有grep和sort、more。

例如：

```sh
~ />php -i | grep gzip
gzip compression => enabled
```

上述命令将php输出的大量信息进行筛选，只显示和gzip相关的信息。这种操作能大大提高信息查询的准确程度和速度。

再比如：

```sh
~ />ls -l | grep 2017 | sort +5n
drwx------+   8 ncsxbmu  staff      256  3  3  2017 Pictures
drwxr-xr-x    4 ncsxbmu  staff      128  5 22  2017 GitBook
drwx------+   6 ncsxbmu  staff      192 10 21  2017 Music
```

上述命令将列出当前目录中2017年的文件，并按照日期进行排序。

### 进程管理

当我们运行程序时，Linux会为程序创建一个特殊的环境，该环境包含程序运行需要的所有资源，以保证程序能够独立运行，不受其他程序的干扰。这个特殊的环境就称为进程。系统通过一个五位数字跟踪程序的运行状态，这个数字称为 pid 或进程ID，每个进程都拥有唯一的 pid。

每个 Linux 进程会包含两个进程ID：当前进程ID(pid)和父进程ID(ppid)。可以暂时认为所有的进程都有父进程。

进程有两种：前台进程和后台进程。

#### 查看进程

使用`ps`命令可查看前台和后台进程：

```sh
[vagrant@localhost ~]$ ps -f
UID        PID  PPID  C STIME TTY          TIME CMD
vagrant   2988  2987  0 08:28 pts/0    00:00:00 -bash
vagrant   3047  2988  0 08:47 pts/0    00:00:00 ps -f
```

每列的含义如下：

|名称|含义|
|----|----|
|UID|进程所属用户的ID|
|PID|进程ID|
|PPID|父进程ID|
|C|CPU使用率|
|STIME|进程开始时间|
|TTY|与进程有关的终端类型|
|TIME|进程所使用的CPU时间|
|CMD|创建进程所使用的命令|

#### 终止进程

前台进程可以通过`kill`或者`ctrl+c`终止，后台进程可以通过`kill`终止。

#### 查看系统进程

top 命令是一个很有用的工具，它可以动态显示正在运行的进程，还可以按照指定条件对进程进行排序，与Windows的任务管理器类似。top 命令可以显示进程的很多信息，包括物理内存、虚拟内存、CPU使用率、平均负载以及繁忙的进程等。

```sh
top - 08:51:50 up 42 min,  1 user,  load average: 0.00, 0.01, 0.05
Tasks:  87 total,   1 running,  86 sleeping,   0 stopped,   0 zombie
%Cpu(s):  0.0 us,  0.3 sy,  0.0 ni, 99.7 id,  0.0 wa,  0.0 hi,  0.0 si,  0.0 st
KiB Mem :   500076 total,   280092 free,   113416 used,   106568 buff/cache
KiB Swap:  1572860 total,  1572860 free,        0 used.   357876 avail Mem
```
