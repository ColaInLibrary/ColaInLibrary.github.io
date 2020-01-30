---
title: Win10下完美安装MathType的方法
description: 介绍在win10下完美安装MathType的方法。
date: '2019.06.21.21:30'
categories:
  - 工科生的基本功
  - 软件技术
tags:
  - Windows
  - Library
abbrlink: 56794
---

> 由于某些软件破解后再联网会导致激活失败，因此需要将该软件禁止联网。


<!-- more -->

MathType6.9安装方法：

下载地址：

[MathType 6.9b 简体中文版官方下载](http://www.mathtype.cn/xiazai.html)

这个安装后无法使用输入注册码的方法进行激活，需要在试用期到期后删除注册表以延长试用期，方法如下：

1.按`Win+R`键，打开运行；

2.输入regedit，打开注册表；

3.依次找到 `HKEY_CURRENT_USER ` -> `Software` -> `Install Options`，右侧显示`Options6.9`，将其删除。如下图所示。
![DeleteMathTypeRegedit]( /images/20190621/DeleteMathTypeRegedit.PNG)

4.重新打开MathType。

MathType7.4主要参考以下内容：
> 7.4的方法已经不再实用，注册码在2019-6-30到期了，而一旦到期就无法再次使用

[数学公式编辑器 MathType 7.4.2.480 for Windows](http://www.itxiaozhong.com/1963.html)(重点看蓝色字部分)
![InstallMathType]( /images/20190621/InstallMathType.PNG)

[win10系统怎么禁用某个程序联网，阻止软件联网](https://jingyan.baidu.com/article/dca1fa6f1a75aaf1a44052f1.html)

软件安装包已保存至网盘，相关链接和操作方法已在微信中收藏(标签为MathType7.4的安装方法)

