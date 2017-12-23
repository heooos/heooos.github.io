---
title: 在requests库中使用代理
date: 2017-12-07 21:46:54
tags: [python,requests库]
categories: Python
---

# 前言

一直以来都想学点Python相关的内容，最近有需要爬取一些网页，开始Python的学习之旅。

对于有一定其他语言基础的人来说，Python上手十分简单。基础的语法，基本的数据结构，常用函数等等这些入门知识在一两天内就可以学完。

到了网络方面，有了强大的第三方 requests库的支持，对于网络的访问，减少了我们很大的学习量，[附带官网地址](http://cn.python-requests.org/zh_CN/latest/) ，中文！很友善！！！

学会使用这个网络库就可以自己动手去练习爬取一些简单的网页了。

在练习过程中，我遇到了下面的问题：



# 遇到的问题以及解决思路

**问题：如何爬取国内无法正常访问的的网页？**

大家都知道，许多很多语言/IDE/第三方lib都是英文的，而且网站一般都架设在国外，访问起来比较慢或者有些根本就无法访问。

**解决办法：**

requests高级应用中可以让我们设置代理来对网站进行访问。使用代理的好处：1,可以突破部分网站对于IP访问限制的反爬虫机制。2.使用海外代理可以访问国内访问速度慢或者无法访问的网站。

1. 代理IP从什么地方获取？

   常见的免费的代理IP网站有：66ip，xicidaili，data5u，proxydb。 优点是数量多，取之不尽，免费，缺点是质量差，需要自己手动测试ip是否可用([自己建立一个IP代理池](https://zhuanlan.zhihu.com/p/25285987))

   收费的代理可以自己找一些知名代理商购买。优点是省心，可用性高，缺点是花钱(贫穷提高了我的技术)

2. 自己搭建代理服务器

   之前因需要查找资料，自己有购买过一台vps搭建ss 科学上网。但是刚开始一脸懵逼，并不知道如何才能在requests库中使用自己的vps进行代理上网。

   经过自己对官方文档的阅读([requests-代理](http://cn.python-requests.org/zh_CN/latest/user/advanced.html#proxies))以及知乎各位老师的帮助，逐渐搞清楚了一些概念性的东西。

   > ss那个东西好像传输层并不是标准的代理接口，它是由本地客户端实现的socks代理接口，然后封装成自己的协议传输至服务端，服务端再解析回socks的。所以无法做到本地不启动客户端，因为ss的协议属于私有协议，常见的库当然无法支持直接使用，必须要有它自己的客户端转换成socks才行。
   >
   > 作者：旅人链接：https://www.zhihu.com/question/263712538/answer/272203940来源：知乎著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。

   逐渐明白在Python中使用代理和自己使用ss客户端登录是不一样的。

   再通过资料查询，看到这么一片文章：[CentOS7 配置SOCKS5代理服务](http://blog.csdn.net/zjiang1994/article/details/74925039) 参考此文章最终完成在vps搭建代理服务器。



# 在VPS上搭建代理服务器

## 写在前面

本文内容将详细说明如何向自己的服务器添加代理功能(SOCKS5)。

## 环境

**服务器主机** ：DigitalOcean 512 MB Memory / 20 GB Disk 
**服务器操作系统**：CentOS 7.2 64位 
**客户端操作系统**：Mac(客户端无所谓，只是用来登录远程主机而已)

## 关于SOCKS5

这里只做简单介绍。 
SOCKS5 是一个代理协议，它在使用TCP/IP协议通讯的前端机器和服务器机器之间扮演一个中介角色，使得内部网中的前端机器变得能够访问Internet网中的服务器，或者使通讯更加安全。

正常情况下客户端和服务端的通信：**客户端<–>服务端**

使用了SOCKS5代理后的通讯：**客户端<–>代理服务器<–>服务端**

我接触这个是因为，我的客户端没有办法直接访问一部分服务端(被墙了),但是我可以访问代理服务器,而且代理服务器可以访问我需要的服务端。 
所以我尝试通过代理服务器来访问需要的服务端(翻墙)。

## 主机安装SS5

1. 通过yum安装ss5 **依赖包**：```yum install gcc openldap-devel pam-devel openssl-devel```

2. 安装成功之后,**安装ss5**：

   1. 首先下载ss5

      ```shell
      # 这个是一个日本大学的sourceforge镜像
      wget http://jaist.dl.sourceforge.net/project/ss5/ss5/3.8.9-8/ss5-3.8.9-8.tar.gz
      ```

      ![下载](https://raw.githubusercontent.com/heooos/heooos.github.io/master/img_res/vps_install_ss5/download_file.png)

   2. 然后解压压缩包：

      ```shell
      # 解压,"ss5-3.8.9-8.tar.gz"是刚才下载的压缩包
      # -v过程显示文件 -z解压/压缩gzip -x解压操作 -f 后面加要操作的文件
      tar -vzx -f ss5-3.8.9-8.tar.gz
      ```

      会解压出来很多文件，进入解压目录

      ```shell
      cd ss5-3.8.9/
      ```

      ![进入目录](https://raw.githubusercontent.com/heooos/heooos.github.io/master/img_res/vps_install_ss5/cd.png)

   3. 运行’./configure’

      ```shell
      # configure是一个shell脚本
      # 主要的作用是对即将安装的程序进行配置，
      # 检查当前的环境是否满足要安装程序的依赖关系.
      # 如果系统环境合适，就会生成makefile，否则会报错。
      ./configure
      ```

      ![运行config文件](https://raw.githubusercontent.com/heooos/heooos.github.io/master/img_res/vps_install_ss5/config.png)

      可以看到check通过了生成了makefile文件~

      这时，我们`ls`一下就会看到文件(红色方框)：

      ![makefile](https://raw.githubusercontent.com/heooos/heooos.github.io/master/img_res/vps_install_ss5/makefile.png)

   4. 接下来我们按照makefile中的规则编译ss5。

      ```shell
      # make是一个命令工具
      # 解释 Makefile 中的规则。
      # Makefile文件中描述了整个工程所有文件的编译顺序、编译规则。
      # 实际上make是执行Makefile中的第一条命令
      make
      ```

   5. 接下来开始安装刚刚编译的程序：

      ```shell
      # 执行Makefile中的install
      # 这些都可以在Makefile文件中看到
      # 可以使用vim Makefile查看文件
      make install
      ```

      这样安装就完成了。



## ss5基本配置

这时我们启动ss5

```shell
service ss5 start
```

可能会出现如下情况：

![权限问题](https://raw.githubusercontent.com/heooos/heooos.github.io/master/img_res/vps_install_ss5/start.png)

原因权限不足，我们修改一下权限：

```shell
# a+x 给所有人加上可执行权限(所有者，所属组，其他)
chmod a+x /etc/init.d/ss5
```

再启动ss5，就没有问题了~

![重新启动](https://raw.githubusercontent.com/heooos/heooos.github.io/master/img_res/vps_install_ss5/re_start.png)

目前为止只是安装上了ss5，也可以正常运行服务，但实际上代理服务还是用不了， 
需要配置一下文件。

首先我们打开ss5的配置文件。

```shell
vim /etc/opt/ss5/ss5.conf
```

![auth](https://raw.githubusercontent.com/heooos/heooos.github.io/master/img_res/vps_install_ss5/auth.png)

![permit](https://raw.githubusercontent.com/heooos/heooos.github.io/master/img_res/vps_install_ss5/permit.png)

把这两处的注释打开(就是auth,permit这两行)

保存并重启ss5(`service ss5 restart`)

这样一个最基本的代理功能就可以使用了

但是有时我们想设置用户，只允许他们使用代理。

这样，我们就需要将上面两处改为

```shell
auth 0.0.0.0/0 – u
```

```
permit u 0.0.0.0/0 – 0.0.0.0/0 – – – – -
```

就是将其中的一个’-‘用’u’代替。

然后打开`/etc/opt/ss5/ss5.passwd`

```shell
vim /etc/opt/ss5/ss5.passwd
```

在第一行加入你允许的用户名和密码,例如

![设置用户名密码](https://raw.githubusercontent.com/heooos/heooos.github.io/master/img_res/vps_install_ss5/uname_pwd.png)

别忘了 **重启ss5** (`service ss5 restart`)



## 测试代理是否成功

首先：

使用Python写一个简单的网页读取程序：

![demo](https://raw.githubusercontent.com/heooos/heooos.github.io/master/img_res/vps_install_ss5/demo.png)

关于proxies的规则，参考requests官方文档。

get()函数加入proxies参数之前

![fail](https://raw.githubusercontent.com/heooos/heooos.github.io/master/img_res/vps_install_ss5/fail.png)

添加代理之后

![](https://raw.githubusercontent.com/heooos/heooos.github.io/master/img_res/vps_install_ss5/success.png)

成功过墙读取到目标网页。



## 以上的命令汇总

```shell
yum install gcc openldap-devel pam-devel openssl-devel
wget http://jaist.dl.sourceforge.net/project/ss5/ss5/3.8.9-8/ss5-3.8.9-8.tar.gz
tar -vzx -f ss5-3.8.9-8.tar.gz
cd ss5-3.8.9/
./configure
make
make install
chmod a+x /etc/init.d/ss5
service ss5 start
vim /etc/opt/ss5/ss5.conf
# 修改配置文件
service ss5 restart
```





# 后续更新

上次创建代理成功之后，一直都使用的非常嗨皮~  但是，由于某次vps因故重启后，ss5竟然不工作了。

因为之前是将ss5的启动加入到自启动列表的，所以ss5应该是会自启动的，但是使用的时候，一直代理异常。于是：

* ssh登录到vps  手动启动一下ss5服务

  ```shell
  service ss5 start
  ```

  系统提示 ok。  但是测试代理 还是链接异常

* 通过命令查看当前启动的服务


  ```shell
  service --status-all
  ```

  返回：

  ```shell
  ● ss5.service - SYSV: This script takes care of starting and stopping ss5
     Loaded: loaded (/etc/rc.d/init.d/ss5; bad; vendor preset: disabled)
     Active: active (exited) since Sat 2017-12-23 08:34:53 UTC; 4min 2s ago
       Docs: man:systemd-sysv-generator(8)
    Process: 14104 ExecStart=/etc/rc.d/init.d/ss5 start (code=exited, status=0/SUCCESS)

  Dec 23 08:34:53 localname systemd[1]: Starting SYSV: This script takes care of starting and stopping ss5...
  Dec 23 08:34:53 localname ss5[14104]: [67B blob data]
  Dec 23 08:34:53 localname ss5[14104]: Can't unlink pid file /var/run/ss5/ss5.pid
  Dec 23 08:34:53 localname systemd[1]: Started SYSV: This script takes care of starting and stopping ss5.
  Dec 23 08:34:53 localname ss5[14104]: done
  ```

  其中一句：

  ```shell
  Can't unlink pid file /var/run/ss5/ss5.pid
  ```

  根据此句继续查找解决方案

* 创建 /var/run/ss5 目录后再启动 ss5 

  每次重启电脑后会将该文件夹删除。so，重建该文件夹后重新启动ss5 就ok了~

  ​