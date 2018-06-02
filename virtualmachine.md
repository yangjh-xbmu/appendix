# 虚拟机

## 为什么要用虚拟机

1. 运行网站、app的真实主机，操作系统大多为linux，而我们开发环境却大多为windows和mac，这样会出现程序在本地运行和在远程主机上运行存在差异的问题，因此有必要在本地模拟远端主机的真实环境，以便减少开发过程中由于运行环境不一致而产生的运行错误问题。
2. 虚拟机可用来安全测试，系统部署，网络测试等，本来需要很多台电脑完成的事情，现在直接在一台或多台物理主机连接的虚拟机网络中就可以完成。
3. 可以在本地电脑中，创建不同开发环境，而互相不影响，如我们可以创建PHP、nodejs、python不同版本的运行环境。

## 虚拟机使用最佳实践

传统使用虚拟机的方式是安装虚拟机软件，然后再在虚拟机中安装操作系统和必要软件，这种方式比较繁琐。使用vagrant虚拟机管理工具，可大大提高使用虚拟机的效率。

### 安装virtualbox

mac用户可利用Homebrew进行安装：

```bash
brew cask install virtualbox
```

### 安装vagrant

Mac用户利用Homebrew进行安装：

```bash
brew cask install vagrant
```

### 查看已安装box

vagrant可以查看本地可用的box（即虚拟镜像），使用如下命令：

```sh
vagrant box list
```

如果没有box，则会显示：

```sh
There are no installed boxes! Use `vagrant box add` to add some.
```

### 安装box

vagrant默认安装box的方式为：

```sh
vagrant box add xx/xxx
```

其中xx/xxx 就是box的名字，如果要使用vagrant提供的box，可从[vagrantcloud站点](https://app.vagrantup.com/boxes/search)进行搜索和下载。由于vagrant默认安装方式时的包存放在国外，直接下载速度可能很慢，因此我们可以先使用迅雷等下载工具，将其下载到本地后，在添加到vagrant系统中，例如：

```sh
vagrant box add centos/7 centos7.box
```

上述命令将当前目录中的centos7.box加载到vagrant管理工具中，并将其命名为centos/7。

### 为项目创建虚拟机

#### 初始化

有了box之后，我们可以将其应用到项目开发中，在项目文件夹中运行如下命令，即可创建虚拟机：

```sh
vagrant init centos/7
```

上述操作会在当前目录中创建vagrantfile文件，这是vagrant工具的配置文件，使用文本编辑器打开这个文件后，将其中的私有网络注释去掉，这样主机和虚拟机之间就可以使用私有网络进行交互：

```sh
  config.vm.network "private_network", ip: "192.168.33.10"
```

#### 设置共享目录

默认情况下，vagrant会共享我们的项目目录，在项目的虚拟机里面，会有一个跟我们的项目的目录是同步的。但在某些情况下，这个默认共享目录无法使用。我们需要手工设置同步目录：

先安装 vbguest 插件，用它可以为虚拟机安装 vbguest：

```sh
vagrant plugin install vbguest
```

然后创建项目目录，初始化虚拟机。

```sh
mkdir centos-7
cd centos-7
vagrant init centos/7
```

编辑配置文件，常用设置如下：

```sh
# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|

  config.vm.box = "centos/7"

  config.vm.network "private_network", ip: "192.168.33.10"

  config.vm.synced_folder "../data", "/www/wwwroot", create:true
  config.vm.synced_folder ".", "/vagrant", disabled: true

  config.vm.provider "virtualbox" do |vb|
    vb.memory = "2048"
  end
end
```

之后启动虚拟机：

```sh
vagrant up
```

先忽略启动错误信息，登录到虚拟机后更新、重启：

```sh
vagrant ssh
sudo yum -y install kernel kernel-devel
sudo yum update
vagrant reload
```

至此，虚拟机与主机之间的共享目录可正常工作了。

#### 启动虚拟机

```sh
vagrant up
```

#### 查看虚拟机状态

```sh
vagrant status
```

#### 连接到虚拟机

```sh
vagrant ssh
```

连接到虚拟机后，用户可以安装必要的软件，进行服务器端的配置。如果想退出连接，执行exit命令即可。

#### 虚拟机操作

|命令|效果|
|----|----|
|vagrant suspend|保存虚拟机状态到硬盘|
|vagrant halt|关闭虚拟机|
|vagrant reload|重启虚拟机|
|vagrant resume|激活挂起的虚拟机|
|vagrant destroy|销毁当前项目创建的虚拟机|

## 如何创建自己的虚拟机镜像包

### 清理一些文件

使用ssh登录到虚拟机，然后清理如下文件，这个文件不清除，这个 box 的项目在配置好网络的时候启动以后会遇到问题。

```sh
sudo rm -rf /etc/udev/rules.d/70-persistent-net.rules
```

### 打包box

```sh
vagrant package
```

该命令会在当前目录生成一个叫`package.box`的文件。

## 扩展阅读资料

1. <https://www.vagrantup.com/intro/getting-started/index.html>
