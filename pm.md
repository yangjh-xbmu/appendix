# 系统包管理工具

## 为什么要用系统包管理工具

通常情况下，我们使用系统默认的方式，如Windows系统中，使用特定的安装程序，Mac中，可使用安装程序或直接拖动到应用程序文件夹即可。除此之外，我们还可以使用系统包管理工具进行软件的安装、升级、卸载。

使用系统包管理工具管理软件有什么好处呢？

1. 通过系统包管理工具安装我们所需软件的时候，包管理工具会为用户自动去下载软件所依赖的其它的东西。
2. 使用包管理工具，可以很方便的去管理软件，比如去升级还有删除它们。
3. 简化软件设置的步骤，方便用户使用。
4. 所有安装的软件都来源于软件的官方网站，增加安全性。

## Windows包管理工具Chocolatey

### 安装

打开<https://Chocolatey.org>官方网站，复制安装脚本，使用管理员身份启动PowerShell或者cmd，按照官网步骤执行脚本，即可完成安装。

### 基本用法

|用法|作用|
|----|----|
|choco install xxx|安装xxx软件|
|choco uninstall xxx|卸载xxx软件|
|choco upgrade xxx|更新xxx软件|
|choco search xxx|搜索xxx软件|

## Mac包管理工具Homebrew

Homebrew是一款自由及开放源代码的软件包管理系统，用以简化Mac OS X系统上的软件安装过程，
使用 Homebrew 安装 Apple 没有预装但你需要的东西。最初由马克斯·霍威尔（Max Howell）写成，因其可扩展性得到了一致好评。

在Mac中安装软件时，优先考虑使用Homebrew进行安装和管理。

### 安装

在其官方网站`https://brew.sh/index_zh-cn`复制安装脚本，然后在终端中执行脚本即可。Homebrew 不会将文件安装到它本身目录之外，所以您可将 Homebrew 安装到任意位置。

安装之后运行：

```sh
brew update
brew doctor
```

排除检查出的错误及警告信息，确保brew正确安装。

之后，添加Homebrew的路径到终端`~/.bash_profile`：

```sh
vi ~/.bash.profile
```

```sh
export PATH="/usr/local/bin:$PATH"
```

### 基本用法

|用法|作用|
|----|----|
|brew install xxx|安装xxx软件|
|brew uninstall xxx|卸载xxx软件|
|brew upgrade xxx|更新xxx软件|
|brew search xxx|搜索xxx软件|

### 安装cask扩展

使用brew方式安装的大都是命令行界面的工具，如果需要使用Homebrew管理图形界面软件，则需要安装cask扩展：

```sh
brew tap caskroom/cask
```

这样，用户就可以使用命令行方式安装图形界面软件，例如：

```sh
brew cask install google-chrome
```

### 常用软件

```sh
brew install node
brew install curl
brew install tree
brew install openssl
brew install python
```

### 更换源

Homebrew的仓库托管在GitHub，在国内访问速度有时很慢，因此，有必要更新国内镜像源，推荐使用中国科技大学的镜像：

```bash
echo 'export HOMEBREW_BOTTLE_DOMAIN=https://mirrors.ustc.edu.cn/homebrew-bottles' >> ~/.bash_profile
source ~/.bash_profile

cd "$(brew --repo)/Library/Taps/homebrew/homebrew-core"
git remote set-url origin https://mirrors.ustc.edu.cn/homebrew-core.git

cd "$(brew --repo)"
git remote set-url origin https://mirrors.ustc.edu.cn/brew.git

cd "$(brew --repo)"/Library/Taps/homebrew/homebrew-cask
git remote set-url origin https://mirrors.ustc.edu.cn/homebrew-cask.git
```
