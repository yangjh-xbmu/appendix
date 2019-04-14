# Git 使用中的常见问题

初学者可先不阅读这一节内容，在有需求的时候再深入学习。

## 如何在 push 时不输入密码

在命令行中，执行如下指令，可全局性地让 Git 工具记住个人用户名和密码信息：

```bash
git config --global credential.helper store
```

还可以使用SSH方式，配置公钥信息后，也可以不输入密码访问。

## 如何为项目创建不同于全局性设置的用户信息

在有些情况下，我们创建的项目仓库，需要设置不同于全局性设置的用户信息，尤其是我们在不同的代码托管站点创建了多个仓库时，很有可能不同网站的用户信息是不一致的。怎样才能为不同仓库设置不同的用户信息，而不使用同一全局性信息呢？

想使用全局配置或是某个项目需要单独配置 `user.name` 和 `user.email`：

```sh
git config user.name "xxx"
git config user.email "xxx@163.com"
```

查看 Git 配置信息，包括全局配置和项目当前配置，二者都有的情况下，**Git 优先使用项目当前配置**：

```sh
git config --list
```

## 如何清除 git 缓存

当我们修改了仓库密码时，由于 git 会缓存之前的密码，可能会出现授权错误，这是可以运行

```sh
git credential-cache exit
```

来清除缓存。

## 如何忽略项目中的特定文件

在项目中，总会有一些特定的文件不想采用 Git 工具进行版本的控制，如临时文件、编译时产生的过渡文件或包含帐号信息的文件，对于这类文件，Git 提供了一个非常高效灵活的方式进行屏蔽，即创建一个`.gitignore`文件。

开发者还可通过 [https://www.gitignore.io/](https://www.gitignore.io/) 工具生成合适的`.gitignore`文件。

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

1. 清除缓存。命令为：

    ```sh
    git rm -r --cached .
    ```

2. 添加文件到仓库：

    ```sh
    git add .
    ```

3. 之后就可添加说明、推送。

## 如何彻底删除仓库中的文件

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

注意，filter-branch 操作中，文件路径必须正确，负责会出现 unchanged 的错误信息。
