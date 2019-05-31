# MySQL

## MySQL 简介

MySQL 是最流行的开源 SQL 数据库管理系统之一，原本由瑞典的 MySQL AB 公司开发，后被美国甲骨文公司（Oracle）收购，现在为甲骨文公司旗下产品。

### 特性

1. MySQL 是一个数据库管理系统。数据库是一组结构化数据的集合，比如一个购物清单、或者图片库。为了添加、获取、处理存储在计算机中的数据库，我们需要一个类似于 MySQL 的数据库管理系统。计算机非常擅长处理大量的数据，数据库管理系统在处理数据中扮演着关键的核心角色。
2. MySQL 是关系型数据库。所谓关系型数据库，就是将数据存放在不同的数据表中，而不是把所有的数据都存储到一起。关系型数据库的结构，考虑到性能因素，分别组织在不同的文件中。采用诸如数据库、数据表、视图、行和列等方式提供灵活的存储和管理数据的方法。“MySQL”中的 SQL，指的是“Structured Query Language”。SQL 是最常用的管理数据库的通用语言。我们可以单独使用 SQL、也可以在 PHP 等编程语言中嵌套着使用 SQL。
3. MySQL 是开源软件。开源意味着任何人都可以使用并且编辑。任何人都可以通过互联网免费下载并使用 MySQL 软件，如果你愿意，你还可以改变 MySQL 的代码，使之更加符合自己的需求。
4. MySQL 数据库具有快速、可靠、可大规模扩展以及容易使用的优点。MySQL 数据库服务器可以运行在台式机或者笔记本，也可以运行在独立的服务器上，并且还可以通过网络将很多台机器组织成大规模的数据库集群。MySQL 数据库从一开始，就是为了快速处理大量数据而开发的，经过多年的开发，MySQL 已经成为功能强大、性能优越、安全可靠的非常适合互联网环境的主流数据库。
5. 支持多种操作系统，如 FreeBSD、HP-UX、Linux、Mac OS、Novell NetWare、NetBSD、OpenBSD、OS/2 Wrap、Solaris、Windows 等等。

“MySQL”的官方读法为“My Ess Que Ell”，但又同时不介意其他习惯性读法的存在。MySQL 中的 My 是 MySQL 的主要开发成员 [Ulf Michael Widenius](http://monty-says.blogspot.hk/) 的女儿名字。

### MySQL 的发展

MySQL 被收购后，甲骨文公司大幅调涨 MySQL 商业版的售价，且甲骨文公司不再支持另一个自由软件项目 OpenSolaris 的发展，因此导致自由软件社区们对于 Oracle 是否还会持续支持 MySQL 社区版（MySQL 之中唯一的免费版本）有所隐忧，因此原先一些使用 MySQL 的开源软件逐渐转向其它的数据库。出于对 MySQL 可能成为闭源软件的担忧，MySQL 的创始人 Ulf Michael Widenius 以 MySQL 为基础，成立分支计划 MariaDB。

MariaDB 的的 API 和协议兼容 MySQL。维基百科已于 2013 年正式宣布将从 MySQL 迁移到 MariaDB 数据库。

## 在 macOS 中安装 MySQL

建议使用 Homebrew 安装，步骤如下：

```bash
# 安装 mysql
brew install mysql
# 启动 mysql 服务
brew services start mysql
# 设置 mysql 管理员信息及安全设置
mysql_secure_installation
# 使用管理员账号登录
mysql -uroot -p
```

使用如下命令，可以查看 MySQL 的配置文件所在路径：

```bash
mysql --help |grep my.cnf
```

找到配置文件所在位置，设置必要的配置信息，如默认字符集等等。

重启服务：

```bash
brew services restart mysql
```

## 创建数据库

在开始处理数据库之前，必须确定需求。网站的需求规定了应该如何设计数据库。

### 命名数据库的元素

精确来说，数据库、表和列名称的长度限制为 64 个字节。虽然在有的系统中，数据库和表的名称不区分大小写，但我们建议总是区分大小写，并将名称全部小写。{{ "Ullman-2014" | cite }}

1. 在使用数据库前，我们需要创建数据库，而创建数据库，首要的问题就是确定数据库的名称。主要确保数据库名称对于 MySQL 服务器是唯一的即可。
1. 确定表名称。数据库中表的名称必须唯一。
1. 确定表中列的名称。命名时尽可能避免与 MySQL 的关键字冲突。

### 确定列类型和大小

一旦确定了数据库所需的所有表和列，就应该确定每个列的数据类型。MySQL 要求明确指定每个列的信息类型。

1. 字符串
1. 数字
1. 日期和时间

列数据类型的选择不仅仅指示数据库存储什么信息，还会影响到数据库的总体性能。开发人员应该根据网站实际需求，合理确定数据类型。MySQL 常用数据类型见表。

|           类型           |                  大小                   |                                   描述                                    |
| ------------------------ | --------------------------------------- | ------------------------------------------------------------------------- |
| char[length]             | length 字节                             | 定长字段，长度为 0-255 个字符                                             |
| varchar[length]          | string 长度+1 字节或 string 长度+2 字节 | 变长字段，长度为 0-65535 个字符                                           |
| tinytext                 | string 长度+1 字节                      | 字符串，最大长度为 255 个字符                                             |
| mediumtext               | string 长度+2 字节                      | 字符串，最大长度为 16777215 个字符                                        |
| longtext                 | string 长度+4 字节                      | 字符串，最大长度为 4294967295 个字符                                      |
| tinyint[length]          | 1 字节                                  | 范围：-128-127，或者 0-255                                                |
| smallint[length]         | 2 字节                                  | 范围：-32768-32767，或者 0-65535                                          |
| mediumint[length]        | 3 字节                                  | 范围：-8388608-8388607，或者 0-16777215                                   |
| int[length]              | 4 字节                                  | 范围：-2147483648-2147483647，或者 0-4294967295                           |
| bigint[length]           | 8 字节                                  | 范围：-923372036854775808-923372036854775807，或者 0-18446774073709551615 |
| float[length,decimals]   | 4 字节                                  | 具有浮动小数点的较小的数                                                  |
| decimal[length,decimals] | 8 字节                                  | 具有浮动小数点的较大的数                                                  |
| date                     | 3 字节                                  | 采用 YYYY-MM-DD 的格式                                                    |
| datetime                 | 8 字节                                  | 采用 YYYY-MM-DD HH:MM:SS 格式                                             |
| timestamp                | 4 字节                                  | 采用 YYYYMMDDHHMMSS 格式，从 1970-2038 年                                 |
| time                     | 3 字节                                  | 采用 HH:MM:SS 格式                                                        |
| enum                     | 1 或者 2 字节                           | enumeration（枚举）的简写，每一列都可以具有多个可能的值                   |
| set                      | 1、2、3、4 或者 8 字节                  | 与 enum 一样，只不过每一列都可以具有多个可能的值                          |

类型中可选的 length 属性，用来限制大小，这种对于列中存储数据量的限制，其目的在于保障性能。

与文本类型的长度属性不同，数字类型中的长度属性不会影响列中可以存储的值的范围。对于整数，长度为显示宽度；对于小数，长度为可以存储的总位数。

timestamp 字段类型的值，会在发生 insert 或者 update 时，自动设置为当前日期和时间。

MySQL 还具有文本类型的多种变体。这些类型是：binary、varbinary、tinyblob、mediumblob 和 longblob。这些类型用于存储文件或加密数据。

char 与 varchar 这两种类型都存储字符串，并且可以设置固定的最大长度。他们之间的区别是，存储为 char 的任何内容将存储为列长度的字符串，如果不够长度，将用空格填充够（从数据库取出时又将删除多余空格）。而 varchar 列中存储的字符串只需要与字符串本身一样长的空间。

从性能角度讲，数据库处理定长的 char 类型时速度更快。

enum 和 set 类型，允许为字段定义一系列可接受的值，enum 可以从数千个可能的值中取一个值，而 set 允许从最多 64 个可能的值中取多个值。

在确定列应该为文本、数字，还是日期类型后，再为每一列选择最合适的子类型。

选择好数据子类型后，应该基于个能最大的输入，把字段的大小限制为尽可能小的值。

### 选择其他的列属性

除了决定列的类型和大小外，还应该考虑列的一些其他属性，如是否为空、默认值、索引、键和自动增加等属性。

首先，不管什么类型，每一列都可以定义为 NOT NULL。理想情况下，在正确设计的数据库中，每张表每一行的每一列都应该有一个值，NOT NULL 将强制一个字段具有值。

在创建表时，还可以为列制定一个默认值。如：

``` sql
gender ENUM('M', 'F') default 'F'
```

gender 列，在添加记录时，如果没有为其指定值，则会使用默认值'F'。

注意，text 列不能设置默认值。

数据类型标记为 unsigned 时，数字限制为整数或 0，还可以把数字类型标记为 ZERO-FILL，这意味着将用 0 填充任何多余的空间。

数据库中的索引（index）是请求数据库留意特定列或者列组合的值得一种方式，通过索引，在检索记录时会提高性能，但是在数据变动后，需要重新建立索引。

数据库中的键（key）是用于设计数据库的规范化过程的组成部分，有两种类型的键：主键（primary key）和外键（foreign key）。每张表都应该有一个主键，一个表中的主键通常被链接为另一张表中的外键。

表中的主键应该遵守以下规则：

1. 它必须总是具有一个值。
1. 它的值确定后不再变化。
1. 它的值不能重复。

在 MySQL 中，可以通过设置`AUTO_INCREMENT`描述为数字列自动增加数值。

## SQL 简介

SQL 是一组特殊的单词，专门用于同数据库交互。所有的主流数据库都会使用 SQL，MySQL 也不例外。SQL 非常容易学习和使用，但要精通 SQL 语句，则需要深入的学习和实践。

### 创建数据库和表

使用 SQL 创建数据库的语法如下：

``` sql
CREATE DATABASE databasename
CREATE SCHEMA `new_schema` DEFAULT CHARACTER SET utf8mb4 ;
```

SQL 不区分大小写。不过建议大写 SQL 关键字，就像前面的示例语法那样。这样做有助于把 SQL 名词与数据库、表和列名区分开。

CREATE 名词也用于建立表。语法如下：

``` sql
CREATE TABLE tablename (column1name description,column2name description...)
```

在 MySQL 客户端内，必须用分号终止每一条 SQL 命令，尽管严格说来这些分号不是 SQL 自身的一部分。

SHOW 命令可用于呈现数据库中的表，或者表中的列名称和类型。语法如下：

``` sql
SHOW TABLES;
SHOW COLUMNS FROM tablename;
```

SHOW 命令的等价命令为 DESCRIBE。

### 插入记录

在创建数据库和表之后，使用 INSERT 命令插入记录，语法如下：

``` sql
INSERT INTO tablename (column1, column2…) VALUES (value1, value2 …)
INSERT INTO tablename (column4, column8) VALUES (valueX, valueY)
```

使用这种结构，可以添加多行记录。

在 SQL 命令中，数值不能用引号括住，字符串、日期时间必须用引号括住，单词 NULL 不能用引号括住。如果在值中需要使用引号，可以使用反斜线进行转义。

偶尔会在 SQL 命令中看到使用反引号（\`）。这个字符与波浪符（～）是同一个键，它与单引号不同。反引号用来安全地引用可能与已存在的 MySQL 关键词重复的表名或列名。

INSERT 中一个有意思的变化是 REPLACE。REPLACE 语句的作用是，如果使用的表的主键或唯一索引的值已经存在，那么 REPLACE 会更新存在的行；如果不存重复则会同 INSERT 一样插入新行。

### 选择数据

SELECT 查询使用以下语法返回与某一条件匹配的记录行：

``` sql
SELECT which_columns FROM which_table
```

最简单的 SELECT 查询是：

``` sql
SELECT * FROM tablename
```

星号意味着你想查看每一列。另外，还可以指定要返回的列，并用逗号把这些列相互隔开。

``` sql
SELECT column1, column3 FROM tablename
```

明确要选择哪些列有几个好处。第一个好处是性能，没有理由获取将不会使用的列。第二个好处是顺序，可以用一种不同于它们在表中布局的顺序返回列。第三个好处是，指定列允许你利用函数操纵那些列中的值。

### 使用条件语句

可以通过向 SELECT 查询中添加 WHERE 名词来实现限制查询条件。语法如下：

``` sql
SELECT which_columns FROM which_table WHERE condition(s)
```

可以结合使用各种运算符以及圆括号来创建更复杂的表达式，例如：

``` sql
SELECT * FROM items WHERE (price BETWEEN 10.00 AND 20.00) AND (quantity > 0)
SELECT * FROM cities WHERE (zip_code = 90210) OR (zip_code = 90211)
```

可以使用数学加法（+）、减法（–）、乘法（\*）和除法（/）运算符在查询内执行数学计算。

### 排序查询结果

为了以一种有意义的方式对它们进行排序，可以使用 ORDER BY 子句。例如：

``` sql
SELECT * FROM tablename ORDER BY column
```

还可以指定排序方式，默认为升序（ASC），若要降序，则使用 DESC，例如：

``` sql
SELECT * FROM tablenameORDER BY column1, column2 DESC
```

### 限制查询结果

在 SELECT 查询中，WHERE 指示返回哪些记录，ORDER BY 决定如何对这些记录进行排序，但是 LIMIT 用于指定要返回多少条记录。其用法如下：

``` sql
SELECT * FROM tablename LIMIT x
```

上面的查询将会返回前 x 条记录。还可以指定开始位置，如下：

``` sql
SELECT * FROM tablename LIMIT x，y
```

上面的语句将返回从 x 条记录开始的 y 条记录。

LIMIT 子句不会改进查询的执行速度，因为 MySQL 仍然必须把每一条记录集合到一起，然后截短列表。但在 mysql 客户或 PHP 脚本中，LIMIT 子句将把要处理的数据量减至最少。

### 更新数据

当表中的数据需要更新时，可以使用如下语句：

``` sql
UPDATE tablename SET column=value WHERE column5=value
```

更新（以及删除）是使用主键的最重要的原因之一。无论何时使用 UPDATE，都要使用 WHERE 条件语句，除非你希望更改会影响每一行。

### 删除数据

彻底从数据库中删除记录。要执行该操作，可以使用 DELETE 命令。语法如下：

``` sql
DELETE FROM tablename WHERE condition
```

使用 DROP 命令删除数据库和表，如：

``` sql
DROP DATABASE databasename
DROP TABLE tablename
```
