# 使用 Git 进行项目版本控制的基本流程

## 用 Git 获取代码

获取已有项目的内容，分为两种情况，即首次获取和更新数据。

### 使用 git clone 命令首次获取远程代码

用户可以自己创建远程仓库（如在GitHub、Gitee等等网站），或者直接找到他人已有的公开远程仓库，复制远程仓库地址后，在命令行中执行以下命令（Windows 用户在想要保存项目代码的文件夹上按右键，选择 Git Bash，进入 Git 命令行），即可获得托管在远程网站中的项目文件（包括代码和版本仓库），如：

```sh
git clone xxx（项目地址）
```

其中第二个参数 xxx 是类似于[https://git.oschina.net/yangjh/LearningPHP.git](https://git.oschina.net/yangjh/LearningPHP.git)的远程仓库地址， 就是公布在托管网站中的项目地址。上述命令执行完后，用户将得到项目文件。

### 使用 git pull 获取远程仓库的更新代码

在完成了对项目仓库的首次克隆后，之后就没有必要每次都完整下载了，可以使用git pull获取项目的全部最新修改，在命令行中执行如下操作：

```sh
git pull
```

需要注意的是，如果用户之前进行了修改，会提示进行代码合并操作。

### 获取远程仓库的特定分支

```sh
git clone -b <branch name> [remote repository address]
```

主要就是在 clone 的时候，后面添加 branch 的信息。如克隆远程仓库`https://git.coding.net/adamyang/blog.git`中的 coding-pages 分支：

```sh
git clone -b coding-pages https://git.coding.net/adamyang/blog.git
```

## 用 Git 管理自己的项目代码

### 设置 Git

使用 Git 工作之前，我们需要做个一次性的配置，这样 Git 就能跟踪到谁做了修改：

```sh
git config --global user.name "your_username"
git config --global user.email "your_email@domain.com"
```

还需要设定推送（push）的默认值：

```sh
git config --global push.default simple
```

### 首次建立 Git 仓库

使用 Git 管理自己的项目代码，也分为两种情况，首次建立仓库和提交更新内容。

初始化本地项目。在相应项目的文件夹上按右键，选择 Git Init here。或者进入 Git Bash 命令行中执行

```sh
git init
```

在项目文件夹上按右键，选择 Git add all files now，将文件夹中的所有文件添加到本地仓库中。或者进入 Git Bash 命令行中执行

```sh
git add .
```

在项目文件夹上按右键，选择 Git commit tool，在随后弹出的对话框中输入更新说明，提交。或者进入 Git Bash 命令行中执行

```sh
git commit -m "..... 更新说明"
```

如果想对本地仓库建立远程的镜像，即将本地仓库托管到 github 之类的站点，应先到此类站点注册帐号，建立远程仓库，然后执行如下命令建立本地仓库和远程仓库的对应关系：

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
2. 添加更新文件到本地仓库，选择`Git add all files now`即可。或者进入 Git Bash 命令行中执行

    ```sh
    git add .
    ```

3. 选择`Git commit tool`为这些更新添加说明注释。或者进入 Git Bash 命令行中执行：

    ```sh
    git commit -m "..... 更新说明"
    ```

4. 执行 Git push 将本地仓库同步到远程仓库。

至此，我们已经能用 Git 工具来管理和追踪项目的变化了。

为了不在每次推送时都输入用户名和密码，我们可以使用SSH公钥或者将密码信息写入配置文件。
