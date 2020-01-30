---
title: MATLAB函数———newrb
description: newrb神经网络函数学习。
date: '2019.05.11.09:00:00'
categories:
  - 工科生的基本功
  - 快乐码农
tags:
  - MATLAB
  - Library
abbrlink: 48200
---

> MATLAB函数学习篇之newrb函数。

<!-- more -->

## newrb函数介绍

`newrb`是MATLAB中用于建立径向基函数神经网络(radial basis function network，RBF network)的函数，函数的两种调用格式如下：

```
net = newrb
[net,tr] = newrb(P,T,goal,spread,MN,DF)
```

径向基网可用于近似函数。 newrb函数将神经元添加到径向基网络的隐藏层，直到它满足指定的均方误差目标。

第一种函数调用方式`net = newrb`用于创建一个新的网络，matlab给出各种参数，不实用。

常用的是第二种调用方式`[net,tr] = newrb(P,T,goal,spread,MN,DF)`，其中的参数含义如下：

 - P -- $R \times Q$维矩阵，Q维输入向量
 - T -- $S \times Q$维矩阵，Q维目标类向量
 - goal -- 均方误差目标(MSE),默认为0
 - spread -- 径向基函数(RBF)速度，默认为1
 - MN -- 最大神经元数，默认为Q
 - DF -- 在显示之间添加的神经元数量，默认为25
 - 返回值为径向基网络。
 
速度(spread)越大，函数逼近越平滑。 速度太大意味着需要很多神经元才能适应快速变化的功能。 
太小的速度意味着需要许多神经元来适应平滑的功能，并且网络可能不会很好地概括。 
使用不同的速度调用newrb以找到给定问题的最佳值。
 
## 示例程序

MATLAB给出的[官方示例程序](https://ww2.mathworks.cn/help/deeplearning/examples/radial-basis-approximation.html?searchHighlight=newrb&s_tid=doc_srchtitle)或者在MATLAB命令窗口输入以下命令。

```
openExample('nnet/demorb1')
```

另外从YouTube上搜`newrb`找到的一个例程如下：

```
clear;
clc;
close all;
x = linspace(0,4*pi,3000);
y = (sin(x) + cos(x) + tanh(x)) + rand(1,3000);
net = newrb(x,y,0.1,1,100,10);
view(net);
result = sim(net,x);
scatter(x,y);
hold on;
plot(x,result,'LineWidth',2,'MarkerSize',10);
R = regression(y,result)
```
