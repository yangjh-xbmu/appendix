# Docker 镜像的使用

镜像是创建容器的模板。

## 获取镜像

使用 pull 命令可从 Docker Hub 上获取官方提供的镜像，例如：

```bash
docker pull centos
```

将会输出：

```bash
Using default tag: latest
latest: Pulling from library/centos
8ba884070f61: Pull complete 
Digest: sha256:8d487d68857f5bc9595793279b33d082b03713341ddec91054382641d14db861
Status: Downloaded newer image for centos:latest
```

从输出信息可以看到，pull命令后如果不指定用户名，将会使用library作为用户名，软件的标签如未指定，将使用latest。

完整的获取镜像的命令如下：

```bash
docker pull [选项] [Docker Registry 地址[:端口号]/]仓库名[:标签]
```

## 使用镜像

获取镜像后，我们就能以这个镜像为基础创建容器。例如以上面的镜像centos为例，可以执行：

```bash
docker run -it centos
```

其中`-it`表示使用交互模式终端。进入终端后，就可以像实体机器一样继续操作了。

## 列出已有镜像

```bash
docker image ls
```

### 对镜像的常用命令总结

|                     命令                     |        含义        |
| -------------------------------------------- | ------------------ |
| docker image ls                              | 列出已经下载的镜像 |
| docker image rm [选项] <镜像1> [<镜像2> ...] | 删除本地镜像       |
