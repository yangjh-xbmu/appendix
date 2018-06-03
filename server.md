# 服务器搭建

我们这里所说的服务器是指运行在互联网上，提供特定服务（如www、ftp等等）的一台或一组计算机。随着信息技术的发展，网络服务器经历了自建、托管、虚拟主机到现在的云主机，相比之前，云主机具有一系列的优势，如自主安装操作系统、自主搭设软件环境，用户自由度很高。因此，对于网络应用开发者而言，非常有必要掌握一定的服务器运维知识。

服务器的搭建有两种思路，一种是自己根据需要选择安装合适、必要的软件包；另外一种是使用服务器面板，如宝塔面板、amh面板。第二种方式更加适合初学者，也是效率较高的一种选择。

## 创建CentOS虚拟机

使用虚拟机技术，创建centos/7虚拟机，启动虚拟机后，先使用yum进行更新，确保软件包保持最新状态。

虚拟机配置如下：

```ruby
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

```sh
sudo yum update
```
## 设置时区信息

```sh
sudo cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime
```

## 安装必要的服务

### 添加IUS源

IUS只为RHEL和CentOS这两个发行版提供较新版本的rpm包。如果在os或epel找不到某个软件的新版rpm，软件官方又只提供源代码包的时候，可以来ius源中找，几乎都能找到。

```sh
sudo yum install https://centos7.iuscommunity.org/ius-release.rpm -y
```

### 安装nginx

```sh
sudo yum install nginx -y
```

启动Nginx：

```sh
sudo systemctl start nginx
```

然后让它开机自启动：

```sh
sudo systemctl enable nginx
```

### 安装MariaDB

CentOS原版中自带MariaDB，但版本较低，因此，我们先移除自带的版本较低的MariaDB，然后安装高版本的MariaDB，再启动MariaDB服务，并将其加入自启动，执行安装设置：

```sh
sudo yum remove mariadb-libs -y
sudo yum install mariadb101u-server -y
sudo systemctl start mariadb
sudo systemctl enable mariadb
sudo mysql_secure_installation
```

### 安装PHP

安装PHP-fpm及常用扩展：

```sh
sudo yum install php71u-fpm php71u-cli php71u-xml php71u-gd php71u-mysqlnd php71u-pdo php71u-mcrypt php71u-mbstring php71u-json -y
```

启动PHP服务，并将其加入自启动：

```sh
sudo systemctl start php-fpm
sudo systemctl enable php-fpm
```

### 配置Nginx信息

```sh
sudo vi /etc/nginx/conf.d/php.basic.conf
```

在这个配置文件中，写入如下信息：

```conf
server {
  listen        80;
  server_name   192.168.33.10;
  root          /vagrant_data/www;
  index         index.php index.html;

 location / {
    try_files $uri $uri/ /index.php?$query_string;
  }

  location ~ \.php$ {
    fastcgi_pass 127.0.0.1:9000;
    fastcgi_index index.php;
    include fastcgi.conf;
  }
}
```

### 安装phpMyAdmin

在phpMyAdmin官方网站下载压缩包，解压到合适目录，依照提示，进行必要的设置。

### 安装nodejs

```sh
vagrant ssh
sudo wget https://nodejs.org/dist/v8.11.2/node-v8.11.2-linux-x64.tar.xz
sudo xz -d node-v8.11.2-linux-x64.tar.xz
sudo tar xvf node-v8.11.2-linux-x64.tar
sudo rm node-v8.11.2-linux-x64.tar
sudo mv node-v8.11.2-linux-x64 node
sudo vim /etc/profile
```

在`/etc/profile`中加入如下信息：

```sh
#set for nodejs
export NODE_HOME=/usr/local/node
export PATH=$NODE_HOME/bin:$PATH
```

重新登录shell，完成nodejs安装。

### 安装yarn

```sh
curl --silent --location https://dl.yarnpkg.com/rpm/yarn.repo | sudo tee /etc/yum.repos.d/yarn.repo
sudo yum install yarn
```

## 使用宝塔面板快速搭建网站

宝塔面板是国内领先的服务器面板服务商，免费提供功能强大的服务器维护程序。在其官方网站运行在线安装脚本即可安装：

```sh
yum install -y wget && wget -O install.sh http://download.bt.cn/install/install.sh && sh install.sh
```
