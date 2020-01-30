---
title: Linux环境下Emacs的配置方法
description: 介绍Emacs的安装方法。
date: '2019.06.14.21:30'
categories:
  - 工科生的基本功
  - 快乐码农
tags:
  - Linux
  - Library
abbrlink: 20916
---

> 为提升自己的开发速度，因此需要熟练掌握一种编辑器，Emacs就是备受推崇的一种优秀编辑器。本文主要针对对Emacs了解较少的初学者，所使用系统环境是Ubuntu16.04。
> 本文主要参考了[Emacs初学者配置文件](https://github.com/linweiyang/emacs.starter)，但是该文最后所描述的rtags安装有些问题，这是由于其所需的clang版本和rtags版本不匹配造成的。

<!-- more -->

# Emacs简介

Emacs是一款优秀的编辑器。

# Emacs的安装

1.cmake的安装：

```javascript
sudo apt install cmake          //安装cmake是因为后面需要用它来编译
```

2.对于Ubuntu LTS 14.04或以上，安装指令如下：

```c++
sudo add-apt-repository ppa:kelleyk/emacs
sudo apt update
sudo apt install emacs26		//获取高版本的emacs
```

3.Emacs初学者配置：

```
git clone https://github.com/linweiyang/emacs.starter   	
cd emacs.starter
./install.sh
```

> 至此，Emacs已经安装完毕。

# 个性化配置

> 由于自己常用的是C++编程，因此进行以下适合程序员的一些配置。

## 一、安装Google Docs的C++语法检查工具

```c++
sudo apt-get install python-pip
sudo pip install cpplint		
```

## 二、安装Zeal工具

安装Zeal工具并下载语言函数手册库：
```c++
sudo apt-get install zeal
```

使用方法：快捷键为`Ctrl+c D`

## 三、rtags工具的安装

rtags能使开发者在emacs中快速查找变量的声明和定义，是开发的利器！安装rtags要求clang的版本与其相匹配。截止笔者写稿之前，用LLVM/Clang的6.0版本可以与其相配。安装方法如下(首先新打开一个终端)：

```
sudo apt-get install llvm-6.0-dev clang-6.0 libclang-6.0-dev openssl
git clone --recursive https://github.com/Andersbakken/rtags.git
cd rtags
mkdir build
cd build
source ~/.bashrc 
cmake ..
make -j2
sudo make install
```

其中`make -j2`是采用双核编译。

这里，需要注意的是，如果以上过程无法安装rtags，应该是clang版本与rtags版本不匹配造成的，可用如下方法来查看：

```c++
clang --version
sudo apt-get remove clang* llvm*   //移除旧版本
sudo apt-get update
sudo apt-get install llvm-6.0-dev clang-6.0 libclang-6.0-dev openssl	//安装新版本
```

rtags的使用方法：快捷键为`Crtl+c r`，等待两三秒后，右侧将显示所有的快捷键，这里只给出前三个：

```c++
Ctrl+c r ,   //当前变量参考
Ctrl+c r .   //当前变量定义
Ctrl+c r /   //当前变量所有参考
```

## 四、CapsLock与Ctrl键的交换

由于Emacs严重依赖于快捷键组合，或者说严重依赖于`Ctrl`键，因此为了方便操作，需要将`CapsLock`与`Ctrl`两个按键进行交换。方法如下：

1.新打开一个终端，输入

```c++
emacs .xmodmap		//用emacs打开xmodmap文件，如没有，将创建
```

2.在.xmodmap中输入

```c++
remove Lock = Caps_Lock
remove Control = Control_L
keysym Control_L = Caps_Lock
keysym Caps_Lock = Control_L
add Lock = Caps_Lock
add Control = Control_L
```

> Emacs中粘贴的快捷键是`Ctrl+Y`。

3.在终端中执行：

```c++
xmodmap .xmodmap
```

> 至此，完成了Emacs环境的配置，但是对于Emacs的快捷键，还需要花很多时间去摸索和学习。