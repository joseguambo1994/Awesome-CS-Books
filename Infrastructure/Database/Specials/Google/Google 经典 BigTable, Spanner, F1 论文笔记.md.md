# Google 经典 BigTable/Spanner/F1 论文笔记.md

# BigTable

Bigtable 是一个分布式的结构化数据存储系统，它被设计用来处理海量数据：通常是分布在数千台普通服务器上的PB 级的数据。Google 的很多项目使用Bigtable 存储数据，包括Web 索引、GoogleEarth、Google Finance。

## 系统架构


## 存储结构

以一个存储Web 网页的例子的表的片段为例：

![](https://ww1.sinaimg.cn/large/007rAy9hly1fzz6uqvl1kj30fd03sab1.jpg)

行名是一个反向URL。contents 列族存放的是网页的内容，anchor 列族存放引用该网页的锚链接文本（alex 注：如果不知道HTML 的Anchor，请Google一把）。CNN 的主页被Sports Illustrater和MY-look 的主页引用，因此该行包含了名为 “anchor:cnnsi.com” 和“anchhor:my.look.ca”的列。每个锚链接只有一个版本（alex 注：注意时间戳标识了列的版本，t9 和t8 分别标识了两个锚链接的版本）；而contents 列则有三个版本，分别由时间戳t3，t5，和t6 标识。

# Todos

- https://www.jianshu.com/p/cbdf895f9019
- https://www.jianshu.com/p/a42dbbdf9706?utm_campaign=maleskine&utm_content=note&utm_medium=seo_notes&utm_source=recommendation
