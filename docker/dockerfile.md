# 使用 Dockerfile 创建镜像

镜像的定制实际上就是定制每一层所添加的配置、文件。如果我们可以把每一层修改、安装、构建、操作的命令都写入一个脚本，用这个脚本来构建、定制镜像。Dockerfile 是一个文本文件，其内包含了一条条的指令(Instruction)，每一条指令构建一层，因此每一条指令的内容，就是描述该层应当如何构建。

## 一个简单的例子

下面以一个简单的例子，最小化显示镜像的构建与使用。

创建一个目录，并在其中创建名为Dockerfile的文本文件，其内容为

```bash
FROM nginx
RUN echo '<h1>Hello, Docker!</h1>' > /usr/share/nginx/html/index.html
```

在该目录中，继续执行 `docker build` 命令构建镜像：

```bash
docker build -t nginx:v1 .
```

构建完毕后，使用镜像创建容器：

```bash
docker run --name web2 -d -p 80:80 nginx:v1
```

现在访问<http://localhost>，应该能看到 Nginx 的自定义欢迎界面了。

### 使用 Dockerfile 定制镜像

一般来说，应该会将 Dockerfile 置于一个空目录下，或者项目根目录下。如果该目录下没有所需文件，那么应该把所需文件复制一份过来。如果目录下有些东西确实不希望构建时传给 Docker 引擎，那么可以用 .gitignore 一样的语法写一个 .dockerignore，该文件是用于剔除不需要作为上下文传递给 Docker 引擎的。

所谓定制镜像，就是以一个镜像为基础，也可以是空镜像（scratch），在其基础上添加新的内容。

Docker 支持使用脚本构建镜像，脚本内容写在 Dockerfile 中。关于 Dockerfile 的指令，可以到 GitHub 站点学习官方以及其他网友提供的构建脚本。

Dockerfile 的常用指令如下

|指令|用途|案例|
|----|----|----|
|FROM|指定基础镜像|FROM nginx 以官方nginx镜像为基础|
|RUN|执行命令| RUN apt-get update 执行更新操作|
|COPY|复制文件|COPY [--chown=<user>:<group>] ["<源路径1>",... "<目标路径>"]|
|CMD|容器启动后运行命令|CMD ["nginx", "-g", "daemon off;"] 容器启动后，前台运行nginx服务|
|ENV|设置环境变量|ENV NODE_VERSION 7.2.0 |
|VOLUME|定义匿名卷|VOLUME /data|
|EXPOSE|声明容器打算使用的端口||
|WORKDIR|指定工作目录|如果需要改变以后各层的工作目录的位置，那么应该使用 WORKDIR 指令|
