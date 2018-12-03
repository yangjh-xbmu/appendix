# Visual Studio Code 编辑器的使用

## VS Code的优势

### 方便的插件安装及管理

与Sublime Text（以下简称ST）编辑器相比，Visual Studio Code（以下简称VS Code）的主要优势在于插件安装的便利性，虽然在速度、内存占用等方面略输ST编辑器，但由于其是微软公司主导开发的开源软件，在生态建设方面、开发速度、更新速度等方面要好于由个人主导开发的ST编辑器，尤其是在插件商店安装的体验要好于ST编辑器。

在ST中，插件的安装需要用户自行搜索添加，而VS Code除了可自行搜索添加外，还可根据打开的文件类型增推荐相关插件，并且插件的安装也非常简单，点击安装即可。

### 内置功能众多

与ST只提供基础编辑功能相比，VSCode内置了很多功能，比如emmet、格式化代码、git等等，使得其更容易被初学者接受。

## VS Code安装

安装VSCode非常简单，从官方网站下载合适的安装包即可，VSCode目前支持Windows、linux和Mac系统。

## 使用简介

### 如何更改编辑器主题

打开命令面板，搜索`theme`，选择颜色主题，再选择合适的编辑器主题即可。

### 如何自定义代码片段

在VSCode中自定义代码片段和ST非常类似，选择`首选项->打开用户代码段`，然后选择对应的语言即可创建自定义代码片段，在VSCode中代码片段使用JSON格式定义。

### 如何自定义快捷键

VSCode快捷键的定义，类似于ST，使用JSON格式，打开`首选项->打开键盘快捷方式`，支持直接设定快捷键，也支持通过`Keybindings.json`自定义快捷键，以下是自定义示例：

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

用户配置文件可存储在云端，这样可在不同机器实现统一配置，具体可通过插件`Settings Sync`实现。该插件的使用需要Github账号。

### 如何在Mac中使用命令行启动VS Code

1. 启动 VS Code.
2. 使用快捷键(⇧⌘P)打开命令面板，输入'shell command'，安装'code' 命令到 PATH。
3. 重启终端，以便新的全局变量生效，现在你可以在任意路径下键入`code`来启动VS Code编辑器了。

## 常用快捷键

VSCode快捷键和ST类似，并且大多数功能的都可以设置快捷键，常用快捷键如下：

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

1. **markdownlint**，Markdown语法检查及风格提示插件。
1. **Snippetica for Markdown**，Markdown snippet，减少书写Markdown文件时键入量。
1. **Live Server**，新建一个可以实时刷新的本地服务器，大大减少开发者的重复性动作，文件修改后，就可在页面中看到更新后的效果。
1. **ESLint**，功能强大的js语法提示工具，减少js代码调试成本。
1. **phpcs**, 按照PSR规则进行语法提示，需要安装pear及CodeSniffer，并进行php.ini配置。
1. **php cs fixer**, 按照PSR规则或自定义规则自动进行PHP文档规范化，比phpfmt更符合psr规范，但无法自动对齐。
1. **better align**，自动对齐，需要设置快捷键。
