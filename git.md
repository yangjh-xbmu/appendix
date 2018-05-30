# Git简明教程

> Always use source code control.---Andrew Hunt 程序员修炼之道

本教程的首要目的，是使读者能用Git这个最流行的分布式版本控制系统管理自己的项目。本教程的另外一个目的，是让选修课程的同学能通过Git工具轻松获取课程的相关文件（代码、教案等）。

本教程并不能使你成为Git工具的专家，很多高级命令并不涉及，如果想进一步学习，请阅读[《Pro Git》](http://git-scm.com/book/zh){{ "Scott-2009" | cite }}。

## Git简介

### 什么是版本控制

什么是版本控制？我为什么要关心它呢？版本控制是一种记录一个或若干文件内容变化，以便将来查阅特定版本修订情况的系统。在本书所展示的例子中，我们仅对保存着软件源代码的文本文件作版本控制管理，但实际上，你可以对任何类型的文件进行版本控制。

如果你是位图形或网页设计师，可能会需要保存某一幅图片或页面布局文件的所有修订版本（这或许是你非常渴望拥有的功能）。采用版本控制系统（VCS）是个明智的选择。有了它你就可以将某个文件回溯到之前的状态，甚至将整个项目都回退到过去某个时间点的状态。你可以比较文件的变化细节，查出最后是谁修改了哪个地方，从而找出导致怪异问题出现的原因，又是谁在何时报告了某个功能缺陷等等。

使用版本控制系统通常还意味着，就算你乱来一气把整个项目中的文件改的改删的删，你也照样可以轻松恢复到原先的样子。但额外增加的工作量却微乎其微。

### 三种类型的版本控制系统

#### 本地版本控制系统

为了解决上面提到的问题，人们很久以前就开发了许多种本地版本控制系统，大多都是采用某种简单的数据库来记录文件的历次更新差异。

其中最流行的一种叫做 rcs，现今许多计算机系统上都还看得到它的踪影。甚至在流行的 Mac OS X 系统上安装了开发者工具包之后，也可以使用 rcs 命令。它的工作原理基本上就是保存并管理文件补丁（patch）。文件补丁是一种特定格式的文本文件，记录着对应文件修订前后的内容变化。所以，根据每次修订后的补丁，rcs 可以通过不断打补丁，计算出各个版本的文件内容。

#### 集中化的版本控制系统

接下来人们又遇到一个问题，如何让在不同系统上的开发者协同工作？于是，集中化的版本控制系统（ Centralized Version Control Systems，简称 CVCS ）应运而生。这类系统，诸如 CVS，Subversion 以及 Perforce 等，都有一个单一的集中管理的服务器，保存所有文件的修订版本，而协同工作的人们都通过客户端连到这台服务器，取出最新的文件或者提交更新。多年以来，这已成为版本控制系统的标准做法。

事分两面，有好有坏。这么做最显而易见的缺点是中央服务器的单点故障。如果宕机一小时，那么在这一小时内，谁都无法提交更新，也就无法协同工作。要是中央服务器的磁盘发生故障，碰巧没做备份，或者备份不够及时，就会有丢失数据的风险。最坏的情况是彻底丢失整个项目的所有历史更改记录，而被客户端偶然提取出来的保存在本地的某些快照数据就成了恢复数据的希望。但这样的话依然是个问题，你不能保证所有的数据都已经有人事先完整提取出来过。本地版本控制系统也存在类似问题，只要整个项目的历史记录被保存在单一位置，就有丢失所有历史更新记录的风险。

#### 分布式版本控制系统

于是分布式版本控制系统（ Distributed Version Control System，简称 DVCS ）面世了。在这类系统中，像 Git，Mercurial，Bazaar 以及 Darcs 等，客户端并不只提取最新版本的文件快照，而是把代码仓库完整地镜像下来。这么一来，任何一处协同工作用的服务器发生故障，事后都可以用任何一个镜像出来的本地仓库恢复。因为每一次的提取操作，实际上都是一次对代码仓库的完整备份。

### Git简史

同生活中的许多伟大事件一样，Git 诞生于一个极富纷争大举创新的年代。Linux 内核开源项目有着为数众广的参与者。绝大多数的 Linux 内核维护工作都花在了提交补丁和保存归档的繁琐事务上（1991－2002年间）。到 2002 年，整个项目组开始启用分布式版本控制系统 BitKeeper 来管理和维护代码。

到了 2005 年，开发 BitKeeper 的商业公司同 Linux 内核开源社区的合作关系结束，他们收回了免费使用 BitKeeper 的权力。这就迫使 Linux 开源社区（特别是 Linux 的缔造者 Linus Torvalds ）不得不吸取教训，只有开发一套属于自己的版本控制系统才不至于重蹈覆辙。他们对新的系统制订了若干目标：

40. 速度
41. 简单的设计
42. 对非线性开发模式的强力支持（允许上千个并行开发的分支）
43. 完全分布式
44. 有能力高效管理类似 Linux 内核一样的超大规模项目（速度和数据量）

于是Linus花了两周时间自己用C写了一个分布式版本控制系统，这就是Git。一个月之内，Linux系统的源码已经由Git管理了！什么是大牛？大家可以体会一下。{{ "liaoxuefeng-2014" | cite }}

自诞生于 2005 年以来，Git 日臻成熟完善，在高度易用的同时，仍然保留着初期设定的目标。它的速度飞快，极其适合管理大项目，它还有着令人难以置信的非线性分支管理系统，可以应付各种复杂的项目开发需求。

Git 版本管理还有一点特别需要说明，就是它的分布式设计非常巧妙和高效，每一个安装了Git的计算机，既是服务端，又是客户端；既能在联网情况下使用，又能在断网的情况使用。

Git迅速成为最流行的分布式版本控制系统，尤其是2008年，GitHub网站上线了，它为开源项目免费提供Git存储，无数开源项目开始迁移至GitHub，包括Linux[^51]，jQuery，PHP，Ruby等等。

历史就是这么偶然，如果不是当年BitMover公司威胁Linux社区，可能现在我们就没有免费而超级好用的Git了。

## 安装Git

Mac OS 最近的版本中，已经内置了git工具，无需安装。

Windows 上安装 Git 非常简单，可以到 [GitHub 的 msysGit 项目](http://msysgit.github.io/)下载 安装文件。完成安装之后，就可以使用命令行的 Git 工具（已经自带了 ssh 客户端）了，另外还有一个图形界面的 Git 项目管理工具。此外，windows用户还可以安装cmder，cmder内置了git，建议使用cmder，更加接近于终端的体验。

## 用Git获取代码

获取已有项目的内容，分为两种情况，即首次获取和更新数据。

### 首次获取代码

第一次获取已有项目数据的并不复杂，首先在想要保存项目代码的文件夹上按右键，选择Git Bash，进入Git命令行。然后在命令行中执行以下命令，即可获得托管在远程网站中的项目文件（包括代码和版本仓库），如：

```sh
git clone https://git.oschina.net/yangjh/LearningPHP.git
```

其中第二个参数[https://git.oschina.net/yangjh/LearningPHP.git](https://git.oschina.net/yangjh/LearningPHP.git)就是公布在托管网站中的项目地址。上述命令执行完后，用户将得到项目文件。

### 获取远程仓库的更新代码

在完成了对项目仓库的首次克隆后，想要获取项目的最新代码，只需在Git Bash命令行中执行如下操作：

```sh
git pull
```

### 获取远程仓库的特定分支

```sh
git clone -b <branch name> [remote repository address]
```

主要就是在clone的时候，后面添加branch的信息。如克隆远程仓库`https://git.coding.net/adamyang/blog.git`中的coding-pages分支：

```sh
git clone -b coding-pages https://git.coding.net/adamyang/blog.git
```

## 用Git管理自己的项目代码

### 设置Git

使用 Git 工作之前，我们需要做个一次性的配置，这样Git就能跟踪到谁做了修改：

```sh
git config --global user.name "your_username"
git config --global user.email "your_email@domain.com"
```

还需要设定推送（push）的默认值：

```sh
git config --global push.default simple
```

### 首次建立Git仓库

使用Git管理自己的项目代码，也分为两种情况，首次建立仓库和提交更新内容。

初始化本地项目。在相应项目的文件夹上按右键，选择Git Init here。或者进入Git Bash命令行中执行

```sh
git init
```

在项目文件夹上按右键，选择Git add all files now，将文件夹中的所有文件添加到本地仓库中。或者进入Git Bash命令行中执行

```sh
git add .
```

在项目文件夹上按右键，选择Git commit tool，在随后弹出的对话框中输入更新说明，提交。或者进入Git Bash命令行中执行

```sh
git commit -m ".....更新说明"
```

如果想对本地仓库建立远程的镜像，即将本地仓库托管到github之类的站点，应先到此类站点注册帐号，建立远程仓库，然后执行如下命令建立本地仓库和远程仓库的对应关系：

```sh
git add remote origin https://仓库地址
```

推送本地仓库数据到远程仓库，执行如下命令：

```sh
git push -u origin master
```

然后输入用户名和密码即可完成推送。

### 提交更新内容

完成上述操作后，以后的工作流程就更简洁了：

1. 编写或者修改代码，保存文件。
2. 添加更新文件到本地仓库，选择Git add all files now即可。或者进入Git Bash命令行中执行
```sh
git add .
```
3. 选择Git commit tool为这些更新添加说明注释。或者进入Git Bash命令行中执行
```sh
git commit -m ".....更新说明"
```
163. 执行Git push将本地仓库同步到远程仓库。

至此，我们已经能用Git工具来管理和追踪项目的变化了。

## 使用GitHub Pages建立个人站点

GitHub 不仅能托管代码，还可以通过GitHub Pages工具免费建立静态站点，非常适合前端开发人员学习、展示作品。具体步骤如下：

171. 在Github站点注册帐号，邮箱验证激活。
172. 创建仓库。在GitHub注册登陆后，创建以自己用户名开头的“username.github.io”的公开仓库，其中username必须和GitHub注册时的用户名一致，否则无法使用Github page服务。
173. 克隆仓库。进入到想要存储项目的文件夹，执行如下命令克隆仓库：

```sh
git clone https://github.com/username/username.github.io.git
```

输入用户名、密码，完成克隆操作后，应该在文件夹生成“username.github.io”的子文件夹，之后个人站点的文件和操作都在该文件夹中完成。

180. 创建首页。进入本地“username.github.io”文件夹，使用编辑器创建index.html，这个文件将是个人站点的首页。
181. 提交代码到GitHub。完成页面编辑后，就可以发布代码到GitHub：

```sh
git add --all
git commit -m "Initial commit"
git push -u origin master
```

如果是首次运行git工具，还要进行全局性用户名和邮箱的声明：

```sh
git config --global user.email "username@mail.com"
git config --global user.name "username"
```

上述操作完成后，本地仓库中的代码将推送到GitHub远程仓库。

197. 浏览站点。启动浏览器，访问如下地址，即可浏览站点：

```sh
http://username.github.io
```

## Git进阶

初学者可先不阅读这一节内容，在有需求的时候再深入学习。

### 如何为项目创建不同于全局性设置的用户信息

在有些情况下，我们创建的项目仓库，需要设置不同于全局性设置的用户信息，尤其是我们在不同的代码托管站点创建了多个仓库时，很有可能不同网站的用户信息是不一致的。怎样才能为不同仓库设置不同的用户信息，而不使用同一全局性信息呢？

想使用全局配置或是某个项目需要单独配置 `user.name` 和 `user.email`：

```sh
git config user.name "xxx"
git config user.email "xxx@163.com"
```

查看Git配置信息，包括全局配置和项目当前配置，二者都有的情况下，Git优先使用项目当前配置：

```sh
git config --list
```

### 如何清除git缓存

当我们修改了仓库密码时，由于git会缓存之前的密码，可能会出现授权错误，这是可以运行

```sh
git credential-cache exit
```

来清除缓存。

### 忽略项目中的特定文件

在项目中，总会有一些特定的文件不想采用Git工具进行版本的控制，如临时文件、编译时产生的过渡文件或包含帐号信息的文件，对于这类文件，Git提供了一个非常高效灵活的方式进行屏蔽，即创建一个`.gitignore`文件。

在这个文件中，项目拥有者只需将不想进入版本仓库的文件列举出来即可，支持通配符。例如：

```sh
*.sublime-project
*.sublime-workspace
*.bak
*.dump
.gz(busy)
test/*
```

需要提醒的是，当`.gitignore`文件更改后，并不能立即起效，需要进行如下操作：

224. 清除缓存。命令为：
```sh
 git rm -r --cached .
```
228. 添加文件到仓库。
```sh
git add .
```
之后就可添加说明、推送。

### 彻底删除仓库中的文件

有时候我们能从版本库中永久删除文件（如可执行文件、存有密码的文件等等），不留痕迹，不仅要让它在版本历史里看不出来，还要把它占用的空间也释放出来。执行如下操作：

```sh
git filter-branch --tree-filter 'rm -rf 要删除文件的完整路径' --tag-name-filter cat -- --all

git push origin --tags --force
git push origin --all --force

rm -rf .git/refs/original/
git reflog expire --expire=now --all
git gc --prune=now
git gc --aggressive --prune=now
du -hs
```

注意，filter-branch操作中，文件路径必须正确，负责会出现unchanged的错误信息。

<!-- ### 如何一次推送到两个远程仓库

### 如何在远程服务器上建立git服务 -->
[^51]: <https://github.com/torvalds/linux，由大神Linux Torvalds管理。>
