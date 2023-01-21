---
title: Git理解与总结
date: 2023-01-21 12:55:44
tags:
  -	建站
categories:
  -	杂
---

Git是一个开源的分布式版本控制系统。

# 工作原理

其工作原理大致为：把代码A备份一份B，再把B备份一份C，修改C后，确认一下提交到B，再确认一下提交到A，就完成了代码的修改。

其中为什么有B呢？因为从C修改到B，可以一段一段的**分段修改提交**，但从B到A则是作为一整份提交（也叫“**原子性提交**”，因为之前认为原子不可分割）。可以理解为B作为暂存区，是把C修改的各种零碎都收集起来，合并汇总后提交。这样阶段性、分段性的特性有助于项目开发。

另一种类似的理解是对应工厂，B是半成品区，A是成品区，C是加工区。

# 名词理解

接下来从下图入手，解释各个名词的含义。

![图1 工作区与版本库](https://secure2.wostatic.cn/static/7LmBk21iBkpgDL23mtvPe7/image.png?auth_key=1674275494-vj8qNj4H9MLEbY6cJnFDp9-0-b79c5ec8eacd812a5760067cc4df4b2d)

主要原理有三个区：

- **工作区**：编辑代码的地方。所谓工作，就是在这里修改。对应前面说的C。
- **暂存区**（Index or Stage）：暂放一下，作为最终提交前的备份。对应前面说的B。
- **HEAD**：像是个指针，指向master、dev这种分支，代表最终成果。对应前面说的A。

其中暂存区和HEAD合起来叫做**版本库**。

对象库Objects是版本库的一个库，个人理解Index和Head之间交换文件的方式是对象（Index和工作区交换文件的方式是文件）。不是很准确，详细可以看[Git官方解释](https://git-scm.com/book/zh/v2/Git-内部原理-Git-对象)。

上面都是在说本地仓库，下面引入远程仓库的概念，例如本地上传github这种云平台。将版本库分为本地和远程两个，与上面区别不大，只是多了一个层级。

![图2 本地仓库和远程仓库](https://secure2.wostatic.cn/static/cCJayA6zuHGDW7JHNJNCpa/image.png?auth_key=1674275192-d3fbdqXw9gk7iUoPixPmKN-0-2a2db9c0304605ee3f9b759e4731dd53)

# Git实战

主要命令在上图里都已经出现过了。下面主要讲这些命令实战怎么用还有要注意些什么。

## 正常修改（常用）

正常修改完提交的流程，也是最常用的流程，是下面这些：

```PowerShell
git add .
git commit -m "xxx" 
```

（生成目录树在powershell中用tree命令，参见[这篇博客](https://blog.csdn.net/chengyq116/article/details/108569070)）

## 图形化界面

鼠标右键，Git GUI here

## 回退版本

有三种方式完成：

1. 图形化界面点击
2. 其他的自己百度吧一大堆懒得抄了。

# Bug & Fixing

## 1.路径问题

需要注意各种命令后面URL都可以是绝对路径也可以是相对路径，其中相对路径是前面没有斜杠的。

如在Blog文件夹中的themes子文件夹有个Next文件夹，那么用相对路径索引就是themes/next文不是/themes/next，或者用./themes/next应该也行。

```PowerShell
C:.
├─themes
│  ├─next
```

## 2.Waiting for your editor to close the file…

- 问题描述：在git commit后出现
- 问题原因：没有加注释
- 解决方案：
  - git commit -m "xxx" 或者git commit -am "xxxxxx"
  - 或者直接在她弹出的编辑器里输入文字作为描述（不需要额外加引号）

# 参考链接

[Git 教程 | 菜鸟教程 (runoob.com)](https://www.runoob.com/git/git-tutorial.html)

[git --暂存区存在的意义_Chasing__Dreams的博客-CSDN博客_git 暂存区的意义](https://blog.csdn.net/Chasing__Dreams/article/details/108573586)
