# Visual Studio Code 编辑器的使用

## VS Code 的优势

### 方便的插件安装及管理

与 Sublime Text（以下简称 ST）编辑器相比，Visual Studio Code（以下简称 VS Code）的主要优势在于插件安装的便利性，虽然在速度、内存占用等方面略输 ST 编辑器，但由于其是微软公司主导开发的开源软件，在生态建设方面、开发速度、更新速度等方面要好于由个人主导开发的 ST 编辑器，尤其是在插件商店安装的体验要好于 ST 编辑器。

在 ST 中，插件的安装需要用户自行搜索添加，而 VS Code 除了可自行搜索添加外，还可根据打开的文件类型增推荐相关插件，并且插件的安装也非常简单，点击安装即可。

### 内置功能众多

与 ST 只提供基础编辑功能相比，VSCode 内置了很多功能，比如 emmet、格式化代码、git 等等，使得其更容易被初学者接受。

### 优秀的文档

VS Code 编辑器的官方文档，覆盖了编辑器使用的各个方面，且有视频讲解，极大地降低了用户的学习成本。

## VS Code 安装

安装 VSCode 非常简单，从官方网站下载合适的安装包即可，VSCode 目前支持 Windows、linux 和 Mac 系统。

## 使用简介

### 字体设置

VS Code 可以为文档指定多个字体，机制和 CSS 中的 font family 是一致的，故可以针对中英文指定不同的字体，英文采用等距字体

### 如何更改编辑器主题

打开命令面板，搜索`theme`，选择颜色主题，再选择合适的编辑器主题即可。

### 如何自定义代码片段

在 VSCode 中自定义代码片段和 ST 非常类似，选择`首选项->打开用户代码段`，然后选择对应的语言即可创建自定义代码片段，在 VSCode 中代码片段使用 JSON 格式定义。

### 如何自定义快捷键

VSCode 快捷键的定义，类似于 ST，使用 JSON 格式，打开`首选项->打开键盘快捷方式`，支持直接设定快捷键，也支持通过`Keybindings.json`自定义快捷键，以下是自定义示例：

```json
[
    {
        "key": "cmd+shift+l",
        "command": "editor.action.insertCursorAtEndOfEachLineSelected",
        "when": "editorTextFocus"
    },
]
```

### 如何进行多点编辑

进入多点编辑模式有多种方式，
通过键盘或鼠标选择多行文字后，选择`在行尾添加光标`进入多点编辑模式。

### 用户配置文件及插件的云端保存及同步

用户配置文件可存储在云端，这样可在不同机器实现统一配置，具体可通过插件`Settings Sync`实现。该插件的使用需要 Github 账号。

### 如何在 Mac 中使用命令行启动 VS Code

1. 启动 VS Code.
2. 使用快捷键 (⇧⌘P) 打开命令面板，输入'shell command'，安装'code' 命令到 PATH。
3. 重启终端，以便新的全局变量生效，现在你可以在任意路径下键入`code`来启动 VS Code 编辑器了。

### Python 解释器的设置

使用 VS Code 作为 Python 开发编辑器，最好进行如下操作：

1. 安装 Python 扩展。
1. 安装语法提示插件。
1. 选择解释器。当 VSCode 遇到 Python 虚拟环境的时候时常会无法找到正确的 Python 解释器和虚拟环境，导致调试无法进行。解决的方案是：在工作目录中设置 Python 的解释器，这样可以避免项目之间发生版本冲突。正确设置`python.pythonPath`即可。

## 常用快捷键

VSCode 快捷键和 ST 类似，并且大多数功能的都可以设置快捷键，常用快捷键如下：

|    功能    |        快捷键         |
| ---------- | --------------------- |
| 命令面板   | `shift+command+p`     |
| 终端面板   | `command+~`           |
| 插件面板   | `shift+command+x`     |
| 侧边栏     | `command+b`           |
| 底部信息栏 | `command+j`           |
| 折叠       | `command+alt+[`       |
| 展开       | `command+alt+]`       |
| 全部折叠   | `command+k,command+0` |
| 全部展开   | `command+k,command+j` |

## 配置文件

以下是我的用户配置文件示例：

```json
{
  // 以像素为单位控制字号。
  "editor.fontSize": 16,
  "workbench.colorTheme": "Solarized Light",
  // 保存时设置文件的格式。格式化程序必须可用，不能自动保存文件，并且不能关闭编辑器。
  "editor.formatOnSave": true,
  "workbench.startupEditor": "newUntitledFile",
  // 启用后，保存文件时在文件末尾插入一个最终新行。
  "files.insertFinalNewline": true,
  // 启用后，保存文件时将删除在最终新行后的所有新行。
  "files.trimFinalNewlines": true,
  // 控制是否显示 minimap
  "editor.minimap.enabled": false,
}
```

## 实用插件

1. **markdownlint**，Markdown 语法检查及风格提示插件。
1. **Snippetica for Markdown**，Markdown snippet，减少书写 Markdown 文件时键入量。
1. **Live Server**，新建一个可以实时刷新的本地服务器，大大减少开发者的重复性动作，文件修改后，就可在页面中看到更新后的效果。
1. **ESLint**，功能强大的 js 语法提示工具，减少 js 代码调试成本。
1. **phpcs**, 按照 PSR 规则进行语法提示，需要安装 pear 及 CodeSniffer，并进行 php.ini 配置。
1. **php cs fixer**, 按照 PSR 规则或自定义规则自动进行 PHP 文档规范化，比 phpfmt 更符合 psr 规范，但无法自动对齐。
1. **better align**，自动对齐，需要设置快捷键。

## 参考资料

1. [VS Code 官方文档](https://code.visualstudio.com/docs/)
