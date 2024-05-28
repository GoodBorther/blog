---
title: Network13-静态路由
date: 2024-05-28 21:49:33
tags:
- network
- 基础知识
categories: 数据通信
cover: https://tuchuang-1258743955.cos.ap-beijing.myqcloud.com/image/20240528215027.png
---
## 前言
为了实现跨多个网段的通信，我们必须使用到路由协议，而静态路由是其中最简单的协议。
## 静态路由在华为设备上的实现
只需要简单的一行命令：
```
ip route-static X.X.X.X（目的网段） X.X.X.X（目的掩码） X.X.X.X（下一跳）
```
路由是一来一回的，所以别忘记写回程路由，这样才是合理的：
![image.png | 800](https://tuchuang-1258743955.cos.ap-beijing.myqcloud.com/image/20240528213810.png)
## 静态路由的一些特点
- 写了静态路由后，除非配置下一跳地址的网口down，否则静态路由会一直存在，不会失效
	- 静态路由和NQA或者BFD联动会解决这个问题
- 静态路由的默认优先级是60
- 多条静态路由，目的网段一致，优先级一致，下一跳不一致，会形成负载分担