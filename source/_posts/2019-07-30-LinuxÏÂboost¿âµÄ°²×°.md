---
title: Linux下boost库的安装
description: 介绍boost库的安装方法。
date: '2019.07.30.11:00'
categories:
  - 工科生的基本功
  - 快乐码农
tags:
  - Linux
  - Library
abbrlink: 45371
---

> 开发环境：Ubuntu16.04 LTS、 boost 1.69。 

<!-- more -->

# 前言

boost库是子Linux环境下用来做串口通信的一个库，本篇主要介绍该库的安装方法。

# boost库的安装

## 下载安装包

可以从[此链接](https://sourceforge.net/projects/boost/files/boost/1.69.0/)下载相应的boost 1.69的安装包，也可以自行从官网上下载安装包。下载完成后，右键解压，极好存放的路径。

## 安装过程

在Terminal中，打开安装包存放路径，执行下列语句进行安装。

```c++
cd 安装包存放路径
./boostrap.sh
./b2
sudo ./b2 --prefix=/usr/local install
```

> 参考链接[Linux下编译安装boost 1.69库全过程](https://www.linuxidc.com/Linux/2019-03/157605.htm)

# 低版本boost库的安装

由于在学习中科院的ROS安装过程中，编译时出现了如下错误，看错误应该是在/usr/local/boost库中调用出错，查资料应该是boost库安装版本过高(当然也可能是由于安装时路径出错，应该在/usr/local路径中)。

![03.png]( /images/20190730boost/03.png)

![02.png]( /images/20190730boost/02.png)

于是本节开始提到的两个路径中使用`sudo rm -rf boost`强制删掉boost，重新在/usr/local路径中安装boost，再次编译，通过！

![01.png]( /images/20190730boost/01.png)
