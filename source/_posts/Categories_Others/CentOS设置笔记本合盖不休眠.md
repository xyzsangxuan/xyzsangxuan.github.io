---
title: CentOS设置笔记本合盖不休眠
date: 2020-07-03 13:32:39
tags: 
    - Centos
categories: 
    - 杂项
cover: /img/cover9.png
top_img: /img/cover9.png
mathjax: false
description: 如题
---
## 前言

&ensp;&ensp;&ensp;&ensp;本来想在虚拟机里面装环境搞一搞事情，折腾完发现，虚拟机要一直开机真的很不方便，突然想起来我还有一台老旧笔记本。索性照着虚拟机把这个老旧的笔记本变成服务器算了。

&ensp;&ensp;&ensp;&ensp;折腾了一圈终于搞成了，但是屏幕，键盘总亮着，笔记本总张开着，还是不够方便。

&ensp;&ensp;&ensp;&ensp;so，就有了这篇记录

## 操作

### 配置文件

&ensp;&ensp;&ensp;&ensp;配置CentOS7的合上笔记本的行为响应的文件，目录为：/etc/systemd/logind.conf

```
vim /etc/systemd/logind.conf
```

### 修改配置

&ensp;&ensp;&ensp;&ensp;配置文件中修改项有很多，主要看这三个

```
HandlePowerKey 按下电源键后的行为，默认power off
HandleSleepKey 按下挂起键后的行为，默认suspend
HandleHibernateKey 按下休眠键后的行为，默认hibernate
HandleLidSwitch 合上笔记本盖后的行为，默认suspend
```



&ensp;&ensp;&ensp;&ensp;我们需要把HandleLidSwitch后面的suspend修改为lock，这样合上笔记本盖子的时候就会变成锁屏状态，计算机继续工作，而不是挂起。

PS.默认logind.conf文件中基本上都被注释掉了，记得去掉注释。

&ensp;&ensp;&ensp;&ensp;使用如下命令使配置生效

```
systemctl restart systemd-logind
```

```
ignore 忽略，跳过
power off 关机
eboot 重启
halt 挂起
suspend shell内建指令，可暂停目前正在执行的shell。若要恢复，则必须使用SIGCONT信息。所有的进程都会暂停，但不是消失（halt是进程关闭）
hibernate 让笔记本进入休眠状态
hybrid-sleep 混合睡眠，主要是为台式机设计的，是睡眠和休眠的结合体，当你选择Hybird时，系统会像休眠一样把内存里的数据从头到尾复制到硬盘里 ，然后进入睡眠状态，即内存和CPU还是活动的，其他设置不活动，这样你想用电脑时就可以快速恢复到之前的状态了，笔记本一般不用这个功能。
lock 仅锁屏，计算机继续工作。
```

