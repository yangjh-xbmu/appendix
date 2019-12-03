# 使用 Pages 服务建立静态网站

大多数 Git 服务商，如 GitHub 、Gitee、Coding.net等，不仅能托管代码，还可以通过 Pages 工具免费建立静态站点，非常适合前端开发人员学习、展示作品。

其中Github、Gitee等网站，可以指定分支中的某个目录为静态网站，比下面介绍的方法更为简单。

## 使用 GitHub Pages 建立个人站点

1. 在 Github 站点注册帐号，邮箱验证激活。
1. 创建仓库。在 GitHub 注册登陆后，创建以自己用户名开头的“username.github.io”的公开仓库，其中 username 必须和 GitHub 注册时的用户名一致，否则无法使用 Github page 服务。
1. 克隆仓库。进入到想要存储项目的文件夹，执行如下命令克隆仓库：

    ```sh
    git clone https://github.com/username/username.github.io.git
    ```

    输入用户名、密码，完成克隆操作后，应该在文件夹生成“username.github.io”的子文件夹，之后个人站点的文件和操作都在该文件夹中完成。

1. 创建首页。进入本地“username.github.io”文件夹，使用编辑器创建 index.html，这个文件将是个人站点的首页。
1. 提交代码到 GitHub。完成页面编辑后，就可以发布代码到 GitHub：

    ```sh
    git add --all
    git commit -m "Initial commit"
    git push -u origin master
    ```

    如果是首次运行 git 工具，还要进行全局性用户名和邮箱的声明：

    ```sh
    git config --global user.email "username@mail.com"
    git config --global user.name "username"
    ```

    上述操作完成后，本地仓库中的代码将推送到 GitHub 远程仓库。

1. 浏览站点。启动浏览器，访问如下地址，即可浏览站点：

    ```sh
    http://username.github.io
    ```
