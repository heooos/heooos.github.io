---
title: 通过Anaconda管理多版本Python
date: 2018-01-27 21:27:18
tags: [python,工具]
categories: Python
---

## Anaconda简介

Anaconda是一个**Python科学计算环境**，支持 Linux, Mac, Windows系统。它可以让用户非常方便地进行包管理与环境管理，而且可以解决多版本python并存、切换以及各种第三方包安装问题。Anaconda利用图形化界面/命令行`conda`来进行包管理与环境管理，并且已经包含了Python和相关的配套工具。当然还很方便的一键安装好Jupyter Notebook，Console，Spyder等常用模块。

## Anaconda安装

直接到[官网](https://www.anaconda.com/download/)选择合适的版本进行下载、安装即可~

## Python多版本之间切换

很多设备自身安装的Python版本为2.X，但是Python3.X逐渐成为主流版本，为了兼容老项目又要跟随潮流，所以需要经常切换Python版本。

幸运的是，有Anaconda这样的神器，使得这个过程变得十分轻松。

### 通过命令行进行创建与切换

#### 安装Python3.6

因为我所使用的Mac自身自带有Python2.7版本，所以我创建一个3.6版本的。

打开终端，输入：

```
conda create --name python36 python=3.6
```

目的是创建一个新的Python 3.6的环境。然后，终端会请求安装新的包到目录`/Applications/anaconda/envs/python36`下，按`y`同意请求（Anaconda之前选择装在了应用程序下，其实Python 3的包就单独装在`.../envs/`下）

#### 激活Python3.6

激活新建的Python 3.6环境，终端输入:

```
source activate python36
```

激活后，会发现terminal输入的地方多了python36的字样, 再输入

```
python --version
```

可以看到系统已经成功切换到了Python 3.6的环境。

#### 退出当前版本

如果要退出Python 3.6环境，输入：

```
source deactivate python36
```

可以看到系统退回Python 2.7环境。

### 通过可视化界面进行操作

打开安装好的Anaconda工具

![](https://raw.githubusercontent.com/heooos/heooos.github.io/master/img_res/anaconda/anaconda_launcher.png)

很清晰的操作界面。通过可视化界面也可以很轻松的创建管理Python版本。