---
title: VMware下Ubuntu的磁盘扩容问题
description: 介绍使用Gparted工具为Ubuntu扩容
date: '2019.07.31.21:30'
categories:
  - 工科生的基本功
  - 软件技术
tags:
  - VMware
  - Library
abbrlink: 48591
---

> 本文中的环境为Ubuntu16.04LTS + VMware10 + gparted-live-1.0.0-3.

<!-- more -->

# 前言

由于刚开始使用虚拟机时，随便分配了一块硬盘大小，至今发现虚拟机下的Ubuntu硬盘空间告急，因此需要在不损失原有硬盘文件的情况下进行扩容。在VMware10中对虚拟机进行扩容主要分为两部分：

1. 在VMware中进行设置，修改预设磁盘大小；

2. 将额外划分出来的磁盘与原虚拟机中Ubuntu的磁盘进行合并(本文介绍)或添加。

> 在进行扩容前，需要下载好gparted-live-1.0.0-3.iso文件，注意这不是在Ubuntu的Terminal中用apt-get来下载。文件下载链接[请点这里](https://sourceforge.net/projects/gparted/files/)。(该网页下载速度缓慢，可能需要开启VPN或者另寻他处)

# 扩容方法

1.首先将下载好的gparted-live.iso文件装载到虚拟机的虚拟光驱中，如下图所示。这是由于在Ubuntu正常开启状态时，磁盘处于mount状态，无法扩容。因此，需要采用类似用U盘安装系统那样来启动系统进行磁盘扩容。

![01.png]( /images/20190731VMware/01.png)

2.点击：虚拟机 --> 设置，对硬盘进行扩容，如下所示，要从“实用工具”的下拉列表中选择“扩展”，等待扩展完成(笔者是从60G扩展到70G的，但是前面几张图是后补的，所以直接显示是70G)。

![02.png]( /images/20190731VMware/02.png)
![03.png]( /images/20190731VMware/03.png)
![04.png]( /images/20190731VMware/04.png)

3.打开虚拟机，在下面画面出现时快速按下 ESC 键。

![05.png]( /images/20190731VMware/05.png)

出现 Boot Menu，从中选择 CD-ROM Drive，如下所示。

![07.png]( /images/20190731VMware/07.png)

4.CD启动的就是GParted Live，如下所示：

![08.png]( /images/20190731VMware/08.png)

选择第一个，弹出下面的画面：

![09.png]( /images/20190731VMware/09.png)

直接点回车即可，接下来进入语言选择。

![10.png]( /images/20190731VMware/10.png)

在上图的圆圈处输入`26`，选择中文。稍后出现下面的画面，并输入`0`。

![11.png]( /images/20190731VMware/11.png)

5.之后即可正常进入CD启动的系统，如没有自动进入下面画面，请在桌面点击`GParted`，进入。

![12.png]( /images/20190731VMware/12.png)

从上图可以看到，已经使用57.99G，有10G未分配，还有2G是用来做swap区的。依次将第一个下面的`extended`和`linux-swap`都删除，可以得到下面的图片。

![13.png]( /images/20190731VMware/13.png)

从上图可以看到，未分配的空间已经从10G变成了12G。接下来，就准备对sda1进行扩容。右键点击，选择调整大小，留下2G空间作swap，如下图所示。

![14.png]( /images/20190731VMware/14.png)

扩容后的效果如下图所示。

![15.png]( /images/20190731VMware/15.png)

从上图中，可以看到sda1已经由原来的58G变为68G，说明扩容成功。还剩下2G，需要分配为`linux-swap`。在未分配的区域右键选择新建，将其创建为`扩展分区`，如下图所示。

![16.png]( /images/20190731VMware/16.png)

创建好后的效果如下图所示。

![17.png]( /images/20190731VMware/17.png)

再从上图的未分配磁盘处右键选择新建，将其创建为`逻辑分区`，文件系统选为`linux-swap`，如下图所示。

![18.png]( /images/20190731VMware/18.png)

创建好后的效果如下图所示。

![19.png]( /images/20190731VMware/19.png)

接下来，按下对勾，完成扩容操作。

![20.png]( /images/20190731VMware/20.png)

6.扩容完成后的效果如下图所示，在下图中，点击圈出来的底部区域，可返回桌面，选择退出。

![21.png]( /images/20190731VMware/21.png)
![22.png]( /images/20190731VMware/22.png)
![23.png]( /images/20190731VMware/23.png)

此时，可点击虚拟机 --> 设置，将CD/DVD的启动挂载取消掉，如下图所示。

![24.png]( /images/20190731VMware/24.png)

在GParted退出时出现的页面直接点击回车即可。

![25.png]( /images/20190731VMware/25.png)

扩容完成后的效果如下图所示。

![26.png]( /images/20190731VMware/26.png)

# ubuntu16.04开机等待1分30秒(1min30s)解决方法

在扩容后，笔者开启Ubuntu启动出现了需要等待1min30s的情况，参照[ubuntu16.04开机等待1分30秒(1min30s)解决方法](https://jingyan.baidu.com/article/63acb44ac9c05b61fdc17e61.html)进行解决。

> 参考链接[VMware11下对虚拟机Ubuntu14.10系统所在分区sda1进行磁盘扩容](https://www.linuxidc.com/Linux/2015-08/121674.htm)