# Sublime Text 编辑器的使用

> 工欲善其事，必先利其器。
> 节选自——孔子《论语·卫灵公》

## 为什么选择 Sublime Text 编辑器

作为开发人员，选择一款理想的文本编辑器，有助于工作效率的提高。实际上，有很多出色的文本编辑器供我们选择，比如Vim、Emacs、WebStorm、Dreamweaver、Notepad++、Sublime Text等等。我们之所以选择Sublime Text编辑器作为开发工具，主要是基于如下优点：

* **学习成本低** Vim和Emacs虽然功能强大，但其具有较为陡峭的学习曲线，而Sublime Text作为一款现代编辑器，更注重用户体验，基本做到了“开箱即用”。
* **跨平台** Sublime Text均为跨平台编辑器（在Linux、OS X和Windows下均可使用）。为了减少重复学习，使用一个跨平台的编辑器是很有必要的。
* **界面优美** 与大多数编辑器只注重满足功能性需求不同，Sublime Text编辑器的界面非常简洁，尤其是选择免打扰模式后，开发人员可集中注意力于工作本身，不被系统中的其他软件信息干扰。还有，其特有的文件迷你地图可让编辑人员直观地了解到自己在文本中的位置。
* **免费** 与商业软件WebStorm、Dreamweaver相比，Sublime Text编辑器可免费使用。Sublime Text虽然不是开源免费软件，但可免费使用全部功能，只是偶尔会在保存文件时提示购买信息。
* **轻便快速** Sublime Text编辑器安装包非常小，只有区区几兆（而其它的商业开发工具往往在1G左右，非常笨重），甚至可以放在U盘中使用；还有，在Sublime Text中，可使用“转到任何”功能，快捷键为`Ctrl+ p`实现文件的快速打开和跳转，提高工作效率；另外，Sublime Text编辑器打开文件时速度很快，尤其是文件比较大时。
* **扩展性良好** Sublime Text编辑器吸收了其它编辑器的优点，用户可对其进行定制和扩展，因此，涌现出能各种需求的扩展程序包，正是这些扩展程序包，使得Sublime Text编辑器和其它编辑器相比有了更多的吸引力。除由他人开发的控制包外，开发人员还可以自定义代码段，能够按照自己的需求自动完成代码，可大大提高编写效率。
* **生态系统完善** 不同于其他编辑器需要用户自行寻找、自行安装扩展包的方式，Sublime Text编辑器的扩展包都统一在一个入口中，这使得用户能够非常方便地获取和更新扩展包，围绕着特定功能往往有多个扩展包可供选择，在[https://packagecontrol.io/](https://packagecontrol.io/)网站，用户可以通过对众多用户行为（使用、安装、卸载）的统计来对扩展包做出选择，借助于统一公开的插件入口和大多数人做出的选择，使得扩展包的开发存在着有序竞争，保障了Sublime Text编辑器的活力。

## 安装与配置

从[Sublime Text官方网站](http://www.sublimetext.com)选择合适的安装版本，安装后需要进行必要的配置才能更高效地使用Sublime Text。

### 设置字体

字体的选择，看起来无关紧要，但如果字体不合适，会给开发工作带来不必要的麻烦。字体的选择，第一个原则是近似字符的区分要清晰，比如`K`和`k`，\`和`'`。字体选择的另外一个因素就是中文支持。结合这两点，建议选择`Consolas`或者`Ubuntu Mono`字体。选择菜单“首选项 → 设置-用户”，打开用户配置文件，加入字体配置：

```json
"font_face": "Ubuntu Mono",
```

### 设置缩进

打开用户配置文件，设置缩进：

```json
"tab_size": 4,
"translate_tabs_to_spaces": true,
"expand_tabs_on_save": true,
```

前两行表示所有自动缩进和tab键都是使用4个空格进行，最后一样是自动转换tab为空格缩进，这样代码就可以实现跨平台保持格式不变。

### 设置换行格式

```json
"default_line_ending": "unix",
"ensure_newline_at_eof_on_save": true,
```

为确保文件在不同系统中都能正常打开，建议将行结束符设置为unix格式。

### 安装Package Control

Package Control是一个非常方便的扩展包管理扩展，在最新版中，安装入口已集成在软件中，点击安装即可。

### 安装中文语言包

安装好Package Control后，就可以方便的安装、卸载、浏览Sublime Text的扩展包，我们先安装Sublime Text的中文语言包，具体步骤如下：

* 选择 “Preference → Package Control → Install Package”，在对话框中键入`Chinese`，选择Chinese Localizition扩展包；
* Package Control会自动从网站下载并安装Chinese Localizition扩展包，安装完成后即可看到中文菜单。

## 常用组件

以下介绍一些常用、必要的扩展包：

* **IMESupport** 解决Sublime Text中使用中文输入法时的光标跟随问题。
* **Alignment** 按照“=”对齐多行，使代码显得更加整洁、可读性更强。
* **DocBlockr** 非常便利的函数功能注释生成扩展，支持Javascript, PHP, CoffeeScript, Actionscript, C , C++ 等等。
* **Emmet** 快速生成HTML、CSS代码的扩展包。该扩展包在书写HTML、CSS代码时可通过缩写提高效率，具体使用方法参见<http://docs.emmet.io/>。
* **FTPsync** 使用ftp方式同步本地代码与远程代码。
* **HTML-CSS-JS Prettify** 使用node.js（需要单独安装node.js）美化HTML, CSS, JavaScript 和 JSON 代码。
* **Auto​PEP8** Python 语言自动排版美化插件。
* **Meterial Theme** 一个漂亮有质感的界面。
* **Terminal** 直接在编辑器中打开终端，并切换到项目目录，默认快捷键为`super+shift+t`。
* **StandardSnippets** JavaScript 代码补全，符合`standardjs code style`。


## 常用快捷键

以下为常用功能对应的快捷键（Windows平台和Mac平台有细微差异）,快捷键的使用是提高工作效率的关键，能用快捷键实现的功能，就不要点击鼠标，随着对编辑器的熟悉，这些快捷键就会慢慢掌握：

* `Ctrl+Shift+D` 复制当前行
* `Ctrl+Shift+K` 删除行
* `Ctrl+K，Ctrl+K` 删除到行末
* `Ctrl+/`  添加或取消注释
* `Ctrl+J` 连接行
* `Ctrl+Enter`  插入空行到下一行
* `Ctrl+Shift+Enter` 插入空行到上一行
* `Alt+-` 返回上次编辑点
* `Alt+Shift+-` 跳转到编辑点
* `Ctrl+Shift+G` 为当前内容添加起始和结束标签
* `Ctrl+alt+up` 与上一行交换顺序
* `Ctrl+alt+l` 进入多行编辑模式

## 常见问题

### 如何自定义代码片段

对经常重复使用的代码片段，我们可以通过sublime text提供的自定义代码片段功能(snippet)来提高效率。

1. 激活定制命令。依次点击菜单：“工具 → 插件开发 → 新建代码片段…”，出现代码片段窗口；
2. 输入代码片段。将`<![CDATA[`和 `]]>` 中的内容替换为想要反复使用的代码片段，在其中可以通过`$1`和`$2`之类的变量，设置跳转点和变量内容；
3. 设置触发命令。取消`<tabTrigger></tabTrigger>`这一行的注释，将触发内容（即输入什么内容后按tab键）写入`<tabTrigger></tabTrigger>`之中；
4. 设置触发命令有效范围。取消`<scope></scope>`这一行的注释，在其中写入snippet的作用范围，即在什么类型的文档中才会触发。文档类型的值，可以在对应的文档中，按`Control+Alt+P`来获得。如md文档的值为`text.html.markdown`，多个文档类型之间可以通过逗号隔开。
5. 存储snippet。将文档保存到`Sublime Text 3/Packages/user`目录中（该目录可以通过菜单“首选项 → 浏览插件目录”打开）。后缀名必须为`.sublime-snippet`。

存储后，该snippet会立即生效。

### 如何使用快速跳转功能

当项目文件数量众多时，查找文件的特定部分就变得低效且繁琐，针对这一问题，Sublime Text 提供了快速跳转命令（Go Anything，快捷键为`Ctrl+P`）解决方案。该功能在打开文件夹的情况下，才能正常使用，否则，只能在已经打开的文件中进行跳转。如：

使用`Ctrl+P`打开快速查找对话框后，输入`wista/index.html`，就会打开`wista`文件夹中的`index.html`文件。

在快速查找对话框输入`@body`，可以快速定位到当前文件的`body`标签。

在快速查找对话框输入输入`:8`，则跳转到第8行。

### 如何为特定功能设置快捷键

Sublime Text中可为任何命令绑定快捷键，这也是它能吸引用户的特性之一。

a. 打开控制台，输入如下内容，以便查看命令名称（当然，如果你知道准确的命令名称的话，就可跳过这一步骤）：

```python
sublime.log_commands(True)
```

比如，我们要为切换状态栏显示状态设定快捷键，可通过刚才的设定，看到其命令为：`toggle_status_bar`。

b. 点击菜单“首选项 → 按键绑定--用户”，打开快捷键配置文件，将控制台反馈的命令按照自己的习惯设定快捷键即可：

```json
[
    { "keys": ["ctrl+k", "ctrl+b"], "command": "toggle_status_bar" },
]
```

通过刚才的设定，当我们按下快捷键`Ctrl+K`后再按`Ctrl+B`就可以显示或隐藏状态栏。

### 如何格式化vue文件

Vue的组件后缀名为.vue，内容是html、css与js代码，使用`HTML/CSS/JS Prettify` 这个插件就行， 安装后 `tools->HTML/CSS/JS Prettify->set prettify preference` 在`"allowed_file_extensions": ["htm", "html", "xhtml", "shtml", "xml", "svg","vue"]`加上vue即可。

### 如何在Mac终端中启动

```bash
ln -s "/Applications/Sublime Text.app/Contents/SharedSupport/bin/subl" /usr/local/bin
```

### Sublime text 无法安装插件的解决办法

Sublime text 编辑器有时会出现能显示插件，但是选择插件后没有任何反应的现象，解决方法如下：

打开设置中的自定义设置信息，将其中的`"0_package_control_loader"`删除即可。

```json
{
    "ignored_packages":
    [   "0_package_control_loader",
        "ASP",
        "Vintage"
    ]
}
```

## 学习资源

* [Sublime Text 非官方详细文档](https://docs.sublimetext.info/en/latest/index.html)
* [Sublime Text 官方论坛](https://forum.sublimetext.com)
* [Sublime Text 官方文档](http://www.sublimetext.com/support)
* [慕课网——前端开发工具技巧介绍—Sublime篇](http://www.imooc.com/view/40)
* [慕课网——快乐的sublime编辑器](http://www.imooc.com/view/333)
