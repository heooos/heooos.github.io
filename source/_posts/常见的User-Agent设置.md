---
title: 常见的User Agent设置
date: 2017-12-03 01:39:49
tags: [python,web]
categories: Python
---

##User Agent简介

User Agent中文名为用户代理，简称 UA。

它是一个特殊字符串头，使得服务器能够识别客户使用的操作系统及版本、CPU 类型、浏览器及版本、浏览器渲染引擎、浏览器语言、浏览器插件等信息。

## User Agent各字段的解释

```java
Mozilla/5.0 (Windows NT 6.3; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/33.0.1750.29 Safari/537.36
//Safari浏览器的UA：Mozilla/5.0 (平台;加密类型;操作系统或CPU;语言）AppleWebKit/AppleWebKit版本号(KHTML, like Gecko) Safari/Safari 版本号
//Chrome浏览器的UA：Mozilla/5.0 (平台;加密类型;操作系统或CPU;语言)AppleWebKit/AppleWebKit版本号 (KHTML, like Gecko) Chrome/ Chrome 版本号 Safari/Safari 版本号
```

- ``Mozilla/5.0``  网景公司浏览器的标识，由于互联网初期浏览器市场主要被网景公司占领，很多服务器被设置成仅响应含有标志为Mozilla的浏览器的请求，因此，新款的浏览器为了打入市场，不得不加上这个字段。
- ``(Windows NT 6.3; WOW64)``
  - ``Windows NT 6.3 ``  Windows 8.1的标识符
  - ``WOW64``  32位的Windows系统运行在64位的处理器上
- `` AppleWebKit/537.36 ``  苹果公司开发的浏览器引擎，常见其他的有：Gecko（Mozilla Firefox 等使用）和Trident（也称MSHTML，IE 使用）
- ``KHTML``  是Linux平台中Konqueror浏览器的呈现引擎KHTML
- ``Geckeo``  呈现引擎
- ``like Gecko``  表示其行为与Gecko浏览器引擎类似

## 常见的User Agent整理

- Android

  - ```
    Mozilla/5.0 (Linux; Android 4.1.1; Nexus 7 Build/JRO03D) AppleWebKit/535.19 (KHTML, like Gecko) Chrome/18.0.1025.166 Safari/535.19
    ```

  - ```
    Mozilla/5.0 (Linux; Android 4.1.1; Nexus 7 Build/JRO03D) AppleWebKit/535.19 (KHTML, like Gecko) Chrome/18.0.1025.166 Safari/535.19
    ```

  - ```
    Mozilla/5.0 (Linux; Android 4.1.1; Nexus 7 Build/JRO03D) AppleWebKit/535.19 (KHTML, like Gecko) Chrome/18.0.1025.166 Safari/535.19
    ```

- Firefox

  - ```
    Mozilla/5.0 (Windows NT 6.2; WOW64; rv:21.0) Gecko/20100101 Firefox/21.0
    ```

  - ```
    Mozilla/5.0 (Android; Mobile; rv:14.0) Gecko/14.0 Firefox/14.0
    ```

- Google Chrome

  - ```
    Mozilla/5.0 (Windows NT 6.2; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/27.0.1453.94 Safari/537.36
    ```

  - ```
    Mozilla/5.0 (Linux; Android 4.0.4; Galaxy Nexus Build/IMM76B) AppleWebKit/535.19 (KHTML, like Gecko) Chrome/18.0.1025.133 Mobile Safari/535.19
    ```

- iOS

  - ```
    Mozilla/5.0 (iPad; CPU OS 5_0 like Mac OS X) AppleWebKit/534.46 (KHTML, like Gecko) Version/5.1 Mobile/9A334 Safari/7534.48.3
    ```

  - ```
    Mozilla/5.0 (iPod; U; CPU like Mac OS X; en) AppleWebKit/420.1 (KHTML, like Gecko) Version/3.0 Mobile/3A101a Safari/419.3
    ```



