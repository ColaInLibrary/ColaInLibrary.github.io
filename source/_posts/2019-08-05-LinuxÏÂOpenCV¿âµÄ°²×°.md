---
title: Linux下OpenCV库的安装
description: 介绍OpenCV库的安装方法。
date: '2019.08.05.11:00'
categories:
  - 工科生的基本功
  - 快乐码农
tags:
  - Linux
  - OpenCV
  - C++
  - Library
abbrlink: 56535
---

> 开发环境：Ubuntu16.04 LTS、 OpenCV3.4.1。 

<!-- more -->

# 前言

OpenCV 是一个开源的计算机视觉库，可以从 http://opencv.org 获取。OpenCV包含的模块以及组成结构参见：http://c.biancheng.net/view/1101.html。

# OpenCV库的安装

## 下载安装包

官网下载sources版本(For Linux)：http://opencv.org/releases.html。

解压，并进入解压后的目录：

```c++
unzip opencv-3.4.1.zip 			//解压安装包，也可以右键解压
cd opencv-3.4.1				//打开安装包存放路径
```

## 安装过程

在Terminal中，打开安装包存放路径，执行下列语句进行安装。

```c++
sudo apt-get install build-essential libgtk2.0-dev libavcodec-dev libavformat-dev libjpeg.dev libtiff4.dev libswscale-dev libjasper-dev
					//上述指令是为了安装依赖库
mkdir build && cd build 		//打开编译目录并进入
cmake -D CMAKE_BUILD_TYPE=Release -D CMAKE_INSTALL_PREFIX=/usr/local ..	
					//编译目录
					//或者cmake -D CMAKE_BUILD_TYPE=RELEASE -D CMAKE_INSTALL_PREFIX=/usr/local -D WITH_TBB=ON -D BUILD_NEW_PYTHON_SUPPORT=ON -D WITH_V4L=ON -D WITH_QT=ON -D WITH_OPENGL=ON ..
make -j$(nproc)				//编译
sudo make install 			//安装
sudo /bin/bash -c 'echo "/usr/local/lib" > /etc/ld.so.conf.d/opencv.conf'	
					//环境配置添加库路径
sudo ldconfig				//更新系统库
sudo gedit /etc/bash.bashrc 		//配置bash，打开后在末尾添加下面两句：
					//PKG_CONFIG_PATH=$PKG_CONFIG_PATH:/usr/local/lib/pkgconfig  
					//export PKG_CONFIG_PATH  
					//保存并退出
sudo -s 
source /etc/bash.bashrc			//激活配置
sudo updatedb  				//更新database
```

> 参考链接：[官网安装(英文版)](https://docs.opencv.org/master/d7/d9f/tutorial_linux_install.html).
>          [Ubuntu16.04安装Opencv3.4.1教程](https://www.cnblogs.com/Shuqing-cxw/p/9195303.html).
>          [sudo: source: command not found](https://blog.csdn.net/ezbuy/article/details/80570189).

# 测试

自己新建一个文件夹，用来存放工程文件，目录如下：

![01.png]( /images/20190805OpenCV/01.png)

> 其中，lena.jpg由自己保存一张图片并以该名字命名，与.cpp存放于同级目录。

## CMakeLists.txt

```c++
cmake_minimum_required(VERSION 2.8)

project( DisplayImage )

find_package( OpenCV REQUIRED )

add_executable( opencv_test opencv_test.cpp )

target_link_libraries( opencv_test ${OpenCV_LIBS} )
```

## opencv_test.cpp

```c++
#include <iostream>
#include <opencv2/opencv.hpp>

using namespace cv;
using namespace std;

int main(int argc, char** argv) {
    if ( argc != 2 ) {
	cout << "Need to load a picture..." << endl;
	return -1;
    }
    Mat image;
    image = imread(argv[1], 1);
    if ( image.empty() ) {
	cout <<"No image data!" << endl;
	return -1;
    }
    namedWindow("Display Image", WINDOW_AUTOSIZE);
    imshow("Display Image", image);
    waitKey(0);
    return 0;
}
```

## 结果

在build文件夹中编译，运行程序：

```c++
cd build
cmake ..						
make
./opencv_test ../lena.jpg		//运行可执行程序，并输入图片名作为参数。其中../表示上一级目录，./表示本级目录下的可执行程序。
```

执行上述程序后，可看到自己保存的图片lena.jpg。
