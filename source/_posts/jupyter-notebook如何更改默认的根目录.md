---
title: jupyter notebook如何更改默认的根目录
date: 2017-11-28 18:17:40
tags: Jupyter
categories: [jupyter,python]
---

Jupyter Notebook 是一款集编程和写作于一体的效率工具。

默认安装好改工具，启动完成后读取的是当前用户的根目录。如何更改工具的默认读取路径呢？

1. 打开终端工具	输入命令 jupyter notebook --generate-config

2. 系统提示

   ``Writing default config to: /Users/**/.jupyter/jupyter_notebook_config.py``

3. 进入到``jupyter_notebook_config.py``文件所在的目录，打开该文件

4. ![conf.jpg](https://raw.githubusercontent.com/heooos/heooos.github.io/master/img_res/jupyter/conf.jpg)参照上图  将202行的代码注释取消掉 然后引号后面的参数填写自己需要作为根目录的路径。

5. 保存，重启Jupyter Notebook 。 

6. Over~