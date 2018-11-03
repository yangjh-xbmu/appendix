# 命令行

简单地说，命令行是一个将接收到的键盘键入命令提交给操作系统执行的程序。在早期，命令行是人们和计算机进行交互的唯一方式，但现在，人们已经习惯使用图形界面（GUI)，但在软件开发过程中，却又需要掌握必要的命令行知识。

## 命令行工具

### windows命令行工具

Windows系统自带命令行工具cmd和powershell，但其界面过于简陋，且功能有限。开源项目cmder解决了在windows系统中使用命令行工具的一些痛点，建议使用，其官方地址为：<http://cmder.net/>，下载完全版，即可在windows系统中免安装使用和Linux、Macos类似的命令行工具。

### MacOS命令行工具

在MacOS中自带终端（terminal）作为命令行工具，还可使用包管理工具Homebrew安装其他命令行工具，不同终端的用法基本保持一致。

## 常用命令

### man

man 命令提供详细的参考手册，如想知道ls命令的详细用法，即可在命令行中执行如下指令:

```bash
man ls
```

按q键退出man命令显示的手册信息。

当我们想要详细了解某个命令的用法时，可使用man命令。

### cd

cd命令改变当前目录位置，用法比较灵活，常用方法如下：

| 命令 | 效果 |
|------|------|
|`cd`   |返回默认目录|
|`cd ..` |返回上一级目录|
|`cd -` |返回之前的目录|
|`cd xxx`|进入xxx目录|
|`cd ph*`|进入第一个ph开头的目录|

### pwd

pwd 显示当前目录信息。

### mkdir

mkdir 用来创建目录，为mkdir命令增加`-p`选项，可以逐级创建所需要的目录。

### rmdir

rmdir 用来删除目录，删除目录时，目录里面不能包含任何文件或目录。

### cp

cp 复制文件或文件夹。常用参数如下：

| 命令 | 效果 |
|------|------|
|`cp -Rf  source target`|复制源目录及文件到目标目录及文件|

### ls

ls 列出目录及文件信息，常见用法如下：

| 命令 | 效果 |
|------|------|
|`ls -l`|显示当前目录及文件的详细信息|
|`ls -lt`|显示当前目录及文件的详细信息，并按照时间倒序显示|
|`ls -ltr`|显示当前目录及文件的详细信息，并按照时间顺序显示|
|`ls -lS`|显示当前目录及文件的详细信息，并按照文件大小排序显示|

通过 ls -l 列出的文件，每一行的开头字符表示文件类型：

|前缀|描述|
|----|----|
|\-|普通文件|
|b|块设备文件|
|c|字符设备文件|
|d|目录文件|
|&#124;|软连接，相当于windows中的快捷方式|
|p|具名管道|
|s|用于进程间通讯的套接字|

### mv

mv 移动目录与文件，这个命令还可以用来重命名文件。

### rm

rm 删除文件或目录，常见用法如下：

| 命令 | 效果 |
|------|------|
|`rm -R xxx`|删除xxx目录及其子目录中的内容|
|`rm -f xxx`|删除xxx目录或文件，并且没有提示信息|

### clear

clear 清除当前终端显示内容，亦可用快捷键`ctrl+k`代替。

### cat

cat 显示文件内容

### wc

wc 用来统计文件的行数、单词数和字符数。

### touch

touch 创建文件

### vi

vi 查看编辑文件内容，属于运行于命令行中的编辑器。

## 命令行操作

### 重复命令

按上下键可调用之前执行过的命令，从而节省键入时间。

### 强行退出

使用快捷键`ctrl+c`可以强行退出正在执行的命令。

## 扩展阅读资料

1. <http://linuxcommand.org/index.php>