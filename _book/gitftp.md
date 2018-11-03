# 用Git方式进行FTP

利用FTP工具可以将本地文件上传到服务器，但传统的FTP工具在使用过程中，都需要留意本地文件和远程文件之间的差异，经常会出现本地文件已经更新，但是忘记上传服务器，或上传到服务器的错误目录。总之，需要人工对上传过程进行干预，故而增加出错可能，降低工作效率。

使用[git-ftp](https://git-ftp.github.io/)工具，可以避免上述问题。

## 安装

在Mac系统中进行安装，需要执行如下命令：

```bash
brew install git
brew install curl --with-libssh2
brew install brotli
brew install git-ftp
```

其他系统的安装，参考[官方网站的信息](https://github.com/git-ftp/git-ftp/blob/master/INSTALL.md)

## 配置

```bash
git config git-ftp.url ftp.example.net
git config git-ftp.user ftp-user
git config git-ftp.password secr3t
```

## 初始化

```bash
# Upload all files
git ftp init

# Or if the files are already there
git ftp catchup
```

## 更新推送

```bash
git ftp push
```
