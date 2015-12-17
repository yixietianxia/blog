---
layout: article
title: Zookeeper研究
category: ky
---
* ###Zookeeper研究
#####1.什么叫zookeeper

      ZooKeeper 是一个为分布式应用所设计的分布的、开源的协调服务。分布式的应用可以建立在同步、配置管理、分组和命名等服务的更高级别的实现的基础之上。 ZooKeeper 意欲设计一个易于编程的环境，它的文件系统使用我们所熟悉的目录树结构。

#####2.ZooKeeper的工作原理
      Zookeeper的核心是原子广播，这个机制保证了各个Server之间的同步。实现这个机制的协议叫做Zab协议。Zab协议有两种模式，它们分别是恢复模式（选主）和广播模式（同步）。当服务启动或者在领导者崩溃后，Zab就进入了恢复模式，当领导者被选举出来，且大多数Server完成了和leader的状态同步以后，恢复模式就结束了。状态同步保证了leader和Server具有相同的系统状态。
      为了保证事务的顺序一致性，zookeeper采用了递增的事务id号（zxid）来标识事务。所有的提议（proposal）都在被提出的时候加上了zxid。实现中zxid是一个64位的数字，它高32位是epoch用来标识leader关系是否改变，每次一个leader被选出来，它都会有一个新的epoch，标识当前属于那个leader的统治时期。低32位用于递增计数。
      每个Server在工作过程中有三种状态：
      LOOKING：当前Server不知道leader是谁，正在搜寻
      LEADING：当前Server即为选举出来的leader
      FOLLOWING：leader已经选举出来，当前Server与之同步



