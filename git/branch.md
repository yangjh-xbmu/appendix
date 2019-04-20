# Git 分支管理

## Git 分支

与其它版本控制系统不同，Git 鼓励使用分支与合并。理解 Git 分支特性，从改变你的开发方式和工作流程。

Git 的分支非常非常轻量！Git 分支的实质上是包含所指对象校验和（长度为 40 的 SHA-1 值字符串）的文件，仅此而已，这样的设计，使得 Git 创建再多分的支也不会造成储存或内存上的开销，所以许多 Git 爱好者传颂：早建分支！多用分支！

在将分支和提交记录结合起来后，我们会看到两者如何协作。现在只要记住使用分支其实就相当于在说：“我想基于这个提交以及它所有的父提交进行新的工作。”

### 为什么要用分支

使用分支的场景很多，比如：想为正在上线运行的程序增加新的功能、修复正在运行程序的缺陷、在现有程序的基础上实验一些功能等等，在这种情况下，开发者可以不改动线上正在运行的代码，而是在现有代码的基础上，建立分支，在分支中进行开发，然后将最终的代码合并到正式发布的分支。

总而言之，当你想增加功能，而你不能、或者不想直接在父分支进行开发的时候，就应该使用分支。

### 创建分支

使用 git branch 就能创建分支：

```bash
git branch testing      // 在当前分支的基础上，创建 testing 分支，但并没有切换到 testing 分支
git checkout -b iss53   // 在当前分支的基础上，创建 iss53 分支，并切换到 iss53 分支
```

### 查看分支

当我们使用 Git 工具，创造本地仓库时，Git 会默认创建一个名为“master”的本地分支。使用`git branch`命令可以查看当前所处的分支：

```bash
git branch

  master
  testing
* iss53
```

其中的`*`号表示用户当前正在使用的分支。

### 合并分支

假设你已经修正了 iss53 问题，并且打算将你的工作合并入 master 分支。为此，你需要合并 iss53 分支到 master 分支，使用 merge 命令可以进行分支的合并，合并的时候，一定要注意要在合并到的分支（如：master）上进行工作。

```bash
$ git checkout master                   // 先切换到 master 分支

Switched to branch 'master'

$ git merge iss53                       // 合并 iss53 分支到当前（master）分支

Merge made by the 'recursive' strategy.
index.html |    1 +
1 file changed, 1 insertion(+)
```

执行 merge 操作的时候，如遇到需要人工决定内容的变动时，Git 工具会提示你进行人工操作，对内容进行修改后，合并才能成功。

### 如何删除分支

当某个分支的使命完成后，可以使用 branch 命令进行删除：

```bash
$ git branch -d hotfix
Deleted branch hotfix (3a0874c).
```

在`-d`参数后加上需要删除的分支即可，如果需要删除的分支中有没有合并到父分支的内容，Git 工具会进行提示。如果该分支的内容已经合并，则会执行分支删除操作。

### 分支管理最佳实践

因为新建分支很容易，所以在团队协作时，应该约定如何建立分支，如何为分支命名等规范，[Vincent Driessen](https://nvie.com/posts/a-successful-git-branching-model/) 在 2010 年提出了一个广受好评的分支管理模型：

![git flow](./../images/git-model@2x.png)

其核心是创建开发分支，将日常开发生成的代码和正式发布运行的代码分离起来，即日常工作都在`develop`分支完成，测试无误后，将其合并到`master`分支。详细情况请阅读 [一个成功的 Git 分支模型](https://nvie.com/posts/a-successful-git-branching-model/)。
