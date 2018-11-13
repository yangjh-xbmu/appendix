# Pandoc

[Pandoc](http://pandoc.org/)是一个文档转换工具，支持docx、markdown、html、pdf、txt等等文件格式的互相转化，作者[John MacFarlane](http://johnmacfarlane.net/)是美国加州大学伯克利分校的哲学教授。

## 用法实例

### markdown转docx

```bash
pandoc demo-math.md -o demo-math.docx
```

将名为`demo-math.md`的文件转化为`demo-math.docx`的word文档。

### 转docx并指定样式

```bash
pandoc -s m.md -S --reference-docx reference.docx -o m.docx
```

将名为`m.md`的文件转化为`m.docx`的word文档，同时使用reference.docx中的样式作为模板，这在一定程度上实现了word创作时的内容和表现分离。

### 转docx并自动生成参考文献

```bash
pandoc --filter pandoc-citeproc --bibliography=myref.bib --csl=chinese-gb7714-2005-numeric.csl demo-citation.md -o demo-citation.docx
```

将名为`demo-citation.md`的文件转化为`demo-citation.docx`的word文档，同时自动生成参考文献。参考文献格式由`csl`文件指定，参考文献内容在`myref.bib`中。

其中markdown文件中写入参考文献的方式为：

```markdown
[@王国成2017从]
```

### 转docx并自动对图表编号

```bash
pandoc --filter pandoc-fignos demo-figref.md -o demo-figref.docx
```

将名为`demo-figref.md`的文件转化为`demo-figref.docx`的word文档，同时自动生成图表编号。其中`pandoc-fignos`需要提前使用pip工具安装（`pip install pandoc-fignos`）

markdown文件要使用自动图表编号，首先在文件头部写入如下信息：

```markdown
---
fignos-cleveref: On
fignos-plus-name: 图
...
```

然后再在图表和引用处标记：

```markdown
大数据的3V特性如{@fig:bigdata3v}所示

![大数据的3V特性](assets/demo-a5a137d9.png){#fig:bigdata3v}
```

## 参考资料

1. [如何用Markdown写论文？](https://zhuanlan.zhihu.com/p/31690364)
1. [pandoc-fignos](https://github.com/tomduck/pandoc-fignos)
1. [pandoc-citeproc](https://hackage.haskell.org/package/pandoc-citeproc)
1. [Pandoc手册](http://pandoc.org/MANUAL.html)
