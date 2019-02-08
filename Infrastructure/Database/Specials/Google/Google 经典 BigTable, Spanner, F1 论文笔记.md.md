# Google 经典 BigTable/Spanner/F1 论文笔记.md

# BigTable

Bigtable 是一个分布式的结构化数据存储系统，它被设计用来处理海量数据：通常是分布在数千台普通服务器上的PB 级的数据。Google 的很多项目使用Bigtable 存储数据，包括Web 索引、GoogleEarth、Google Finance。

Bigtable是建立在其它的几个Google基础构件上的。BigTable 使用Google 的分布式文件系统(GFS)存储日志文件和数据文件。BigTable 集群通常运行在一个共享的机器池中，池中的机器还会运行其它的各种各样的分布式应用程序，BigTable 的进程经常要和其它应用的进程共享机器。BigTable 依赖集群管理系统来调度任务、管理共享的机器上的资源、处理机器的故障、以及监视机器的状态。

## 系统架构


## 存储结构

以一个存储Web 网页的例子的表的片段为例：

![](https://ww1.sinaimg.cn/large/007rAy9hly1fzz6uqvl1kj30fd03sab1.jpg)

Bigtable 通过行关键字的字典顺序来组织数据。表中的每个行都可以动态分区。每个分区叫做一个”Tablet”，Tablet 是数据分布和负载均衡调整的最小单位。访问控制、磁盘和内存的使用统计都是在列族层面进行的。

行名是一个反向URL。contents 列族存放的是网页的内容，anchor 列族存放引用该网页的锚链接文本（alex 注：如果不知道HTML 的Anchor，请Google一把）。CNN 的主页被Sports Illustrater和MY-look 的主页引用，因此该行包含了名为 “anchor:cnnsi.com” 和“anchhor:my.look.ca”的列。每个锚链接只有一个版本（alex 注：注意时间戳标识了列的版本，t9 和t8 分别标识了两个锚链接的版本）；而contents 列则有三个版本，分别由时间戳t3，t5，和t6 标识。

不同版本的数据通过时间戳来索引。Bigtable 时间戳的类型是64 位整型。
Bigtable 可以给时间戳赋值，用来表示精确到毫秒的“实时”时间；用户程序也可以给时间戳赋值。如果应用程序需要避免数据版本冲突，那么它必须自己生成具有唯一性的时间戳。数据项中，不同版本的数据按照时间戳倒序排序，即最新的数据排在最前面。为了减轻多个版本数据的管理负担，我们对每一个列族配有两个设置参数， Bigtable 通过这两个参数可以对废弃版本的数据自动进行垃圾收集。用户可以指定只保存最后n 个版本的数据，或者只保存“足够新”的版本的数据。


# Todos

- https://www.jianshu.com/p/cbdf895f9019
- https://www.jianshu.com/p/a42dbbdf9706?utm_campaign=maleskine&utm_content=note&utm_medium=seo_notes&utm_source=recommendation
