---
title: C#中的套接字编程
date: 2020-07-15 18:23:08
tags: 
    - 套接字编程
categories: 
    - C#
cover: /img/cover4.png
top_img: /img/cover4.png
mathjax: false
description: 如题
---
&ensp;&ensp;[浅析C#中的套接字编程](https://www.cnblogs.com/Aioria0622/archive/2007/12/03/980880.html)

&ensp;&ensp;[C# Socket网络编程精华篇](https://www.cnblogs.com/asdyzh/p/9839775.html)

&ensp;&ensp;[[总结]学习Socket编写的聊天室小程序](https://www.cnblogs.com/fenglingyi/p/4754785.html)

&ensp;&ensp;[[C#]手把手教你打造Socket的TCP通讯连接（一）](http://www.cnblogs.com/Kation/archive/2013/03/06/2946761.html)

&ensp;&ensp;[.net平台下C#socket通信（上）](http://www.cnblogs.com/ysyn/p/3399351.html)


&ensp;&ensp;[C#服务器与客户端通过Socket传递JSON格式数据](https://blog.csdn.net/m0_37764065/article/details/104419190?utm_medium=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-1.nonecase&depth_1-utm_source=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-1.nonecase)

## 异步通信

* 1.创建服务器Socket->绑定IPEndPoint->新建state类，绑定必要的信息
* 2.beginaccept()异步接收请求连接
```
ServerSocket.BeginAccept(new AsyncCallback(Accept), ServerSocket);
```
## C#服务器与客户端通过Socket传递JSON格式数据
* 在.Net阵营中，Json.Net是由官方推荐的高性能开源序列化/反序列化工具