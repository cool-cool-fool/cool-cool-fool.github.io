---
title: Hexo+Github建站配置过程
date: 2023-01-20 20:42:37
tags:
  - 建站
categories:
  - [杂]
---

# Hexo建站

跟着[这个教程](https://zhuanlan.zhihu.com/p/26625249)一步一步走。

需要注意的点有：

1. _config.yaml中，最后的deploy片段中的branch写main而不是master（因为github把master改名叫main了）

```YAML
deploy:
  type: git
  repository: git@github.com:coool-sheep/coool-sheep.github.io.git
  branch: main
```

# Hexo主题设置-NexT

------

看了一圈还是NexT主题最合我心意。（还有一个主题也不错：[Cactus](https://link.zhihu.com/?target=https%3A//github.com/probberechts/hexo-theme-cactus)，留着备用）

（官网链接看：[Hexo官方](https://github.com/theme-next/hexo-theme-next)，但是完全没有文档，如有需要建议看hexo[中文官网](https://hexo.io/zh-cn/)）

配置过程看中文官网连接：[开始使用 - NexT 使用文档 (iissnan.com)](http://theme-next.iissnan.com/getting-started.html)，写得很清楚。

# Hexo常用命令

------

在Blog的**根文件夹**右键选择git bash here。

**1.更新文档**

更新文档三步走：

1. hexo clean
2. hexo g
3. hexo d

其中g是generate（生成）的缩写，d是deploy（部署）的缩写。

**2.测试网站**

hexo s —debug

在debug期间会生成一个本地的网址以供浏览 http://localhost:4000/，命令行Ctrl+C退出。

测试网站因为是本地的没有推送到云端，因此**直接修改后刷新页面就可以了，比较方便**。

**3.其他常用命令**

> npm install hexo -g #安装Hexo

npm update hexo -g #升级

hexo init #初始化博客

命令简写 ：

hexo n "我的博客" == hexo new "我的博客" #新建文章

hexo g == hexo generate #生成

hexo s == hexo server #启动服务预览

hexo d == hexo deploy #部署

hexo server #Hexo会监视文件变动并自动更新，无须重启服务器

hexo server -s #静态模式

hexo server -p 5000 #更改端口

hexo server -i 192.168.1.1 #自定义 IP

hexo clean #清除缓存，若是网页正常情况下可以忽略这条命令

# FQA

------

## 1.Troubleshooting

[Troubleshooting | Hexo](https://hexo.io/docs/troubleshooting.html)

## 2.重新部署不更新

解决方法1：先hexo clean

解决方法2：删除根目录下`.deploy_git`里的内容（注意不是删除这个文件夹，是删里面的东西），之后重新三步走。

## 3.Spawn Falied

在上面还有个这个报错：

not a git repository (or any of the parent directories): .git

解决方法：是git出问题了，没有.git文件，在命令行里git init一下就行

## 4."modified content, untracked content"问题

- 问题描述：在修改了next的config后去hexo三步走，结果一直提示修改的文件没有进入stage库，即使手动git add或者通过GUI界面操作也不行。
- 问题原因：这个提示的意思是看到了修改的文件，但是没办法track。
- 解决方案：删除next中的.git文件，重新添加git add themes/next，之后git commit -a。最后hexo三步走就正常了。
- 参考：[用git提交项目的时候提示“no changes added to commit”_Advancer的博客-CSDN博客](https://blog.csdn.net/qq_23043541/article/details/103023547)

## 5.Hide "Keep on posting" in Archive Page

见[这个链接](https://theme-next.js.org/docs/advanced-settings/custom-files.html#Hide-quot-Keep-on-posting-quot-in-Archive-Page)。

# 附录

1. NexT中的图标网站

[Find Icons with the Perfect Look & Feel | Font Awesome](https://fontawesome.com/icons/heart?s=solid&f=classic)，使用的时候用fa-heart就行

# 参考链接

[GitHub+Hexo 搭建个人网站详细教程 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/26625249)

[modified: (modified content, untracked content)_彭世瑜的博客-CSDN博客](https://blog.csdn.net/mouday/article/details/80287683)

[SHIQI's Blog (ursocute.github.io)](http://ursocute.github.io/)（参考NexT主题模板）

[hello,hxjBLog](https://hxjblog.github.io/)（友情链接）https://zhuanlan.zhihu.com/p/26625249)
