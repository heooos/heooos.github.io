---
title: Linux(CentOS)中运行Python脚本
date: 2017-12-12 01:00:25
tags: [python,linux,脚本]
categories: Linux
---

Python爬虫脚本完成之后，是需要长期/定时执行 爬取相关的内容。所以，我们通常将脚本上传到服务器进行执行(本文在CentOS环境下测试)。

- Python脚本如何在服务器上运行？

  1.确保服务器安装有所需要的Python版本和相关依赖

  2.直接在终端中输入python script.py进行执行。

  ```java
  [root@centos ~]# python script.py
  Script is running!
  Script is running!
  Script is running!
  Script is running!
  Script is running!
  ...
  ```

  这种方式运行的时候，我们的shell不能关闭，否则会中断任务的进行。

- Python脚本在服务器上后台运行？

  直接用unhup命令来让程序在后台运行，命令格式如下：

  ```shell
  nohup python 文件名.py (> ***.log )&
  ```

  在这个命令中，python指定我们要执行的文件为python文件，后面的文件名.py即是我们要执行的文件。括号内容表示可以将平时输出到控制台中的内容重定向到***.log这个文件中，这个是可选的，如果没有这个，则会默认输出到nohup.out文件中。括号后面你的&表示后台运行。

  ```java
  [root@centos ~]# nohup python -u main.py > out.log 2>&1 &
  [1] 25839   //返回执行PID  
  ```

  此时，我们的script.py脚本已经在后台执行  而且输出的信息在 out.log文件中。

  **现在当我们直接关闭shell窗口，再连接上服务器，查看Python的进程，发现进程还在**

- 如何查看脚本是否在后台执行？

  1.通过ps -e命令可以查看所有后台运行的进程

  ```java
  [root@centos ~]# ps -e
  PID TTY          TIME CMD
      1 ?        00:00:00 init
      ...
  25839 pts/1    00:00:00 python  //可以看到我们的程序正在运行
  ```

  2.通过jobs命令可以查看后台运行的程序(重新链接到终端后，该方法无效，请使用ps命令)

  ```
  [root@centos ~]# jobs
  [1]+  Running                 nohup python -u main.py > out.log 2>&1 &
  ```

- 如何停止脚本运行？

  - 前台程序：使用Ctrl+c
  - 后台程序：通过kill命令  ``kill %mm``（mm可以通过jobs获得）或者```kill mm```（mm可以通过ps获取pid）



常见命令：

- ```&``` 加在命令的最后，可以把这个命令放到后台执行
- **ctrl + z** 将一个正在前台执行的命令放到后台，并且处于暂停状态。
- ``jobs``  查看当前有多少在后台运行的命令，jobs -l选项可显示所有任务的PID，jobs的状态可以是running, stopped, Terminated。
- ``fg`` 将后台中的命令调至**前台**继续运行。如果后台中有多个命令，可以用fg %jobnumber（是命令编号，不是进程号。通过jobs查看）将选中的命令调出。
- ``bg`` 将一个在后台暂停的命令，变成在**后台**继续执行。如果后台中有多个命令，可以用bg %jobnumber将选中的命令调出

