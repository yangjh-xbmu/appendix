# 服务器

我们这里所说的服务器是指运行在互联网上，提供特定服务（如www、ftp等等）的一台或一组计算机。随着信息技术的发展，网络服务器经历了自建、托管、虚拟主机到现在的云主机，相比之前，云主机具有一系列的优势，如自主安装操作系统、自主搭设软件环境，用户自由度很高。因此，对于网络应用开发者而言，非常有必要掌握一定的服务器运维知识。

## 服务器操作系统

## Linux 简介

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

### 常用命令

参见[命令行](commandline.html)章节内容。

### 文件管理

Linux中的所有数据都保存在文件中，所有的文件有被分配到不同的目录中，目录是一种类似于树结构的文件系统。在Linux中，有三种基本的文件类型：

1. 普通文件
1. 目录
1. 设备文件，Linux将外部设备视为一个文件，输入输出到外部设备的方式和输入输出到一个文件的方式是相同的。



## 常用服务的搭设

### 网页服务

### ftp

### git

### 数据库

### php

### node

### python

## 服务器安全