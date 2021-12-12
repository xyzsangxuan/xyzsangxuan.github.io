---
title: 震惊！Ctfmon无法启动 任务栏输入法图标消失竟然是因为这个！
date: 2020-07-03 13:38:43
tags:   
    - Windows
categories: 
    - 杂项
cover: /img/cover8.png
top_img: /img/cover8.png
mathjax: false
description: 如题
---
## 前言

&ensp;&ensp;&ensp;&ensp;废话不多说，打算拿出我的数位板画几个小人，结果劳资的噩梦就来了...

&ensp;&ensp;&ensp;&ensp;首先我买的是高漫的便宜的板子，驱动是第三方下的旧版本驱动（吐槽一下官网最新的驱动，永远都是未连接设备）一切搞定后，试了试压感，调了笔，没有问题后我习惯性的重启一下电脑！

## 问题

&ensp;&ensp;&ensp;&ensp;问题来了，再开机的时候任务栏的输入法没了，谷歌和文本文档都无法使用中文，无法切换输入法了。

&ensp;&ensp;&ensp;&ensp;我一开始以为是中文语言的问题，排查之后莫得问题啊，然后我就开始了疯狂的百度，介绍的方法全都试了一遍，全都不行。

&ensp;&ensp;&ensp;&ensp;然后我又看了启动项，ctfmon启动—没问题，详细信息寻找ctfmon？？？竟然木有ctfmon...

&ensp;&ensp;&ensp;&ensp;最后确定问题在于ctfmon没有正常启动...

## 解决

&ensp;&ensp;&ensp;&ensp;所以现在问题就变成了如何启动ctfmon，我试过手动启动ctfmon，不行！修改注册表，不行！再修改注册表启动项还是不行！

&ensp;&ensp;&ensp;&ensp;就在我即将放弃的时候，我终于看到了贴吧一个大佬的提问“你们的win10有ctfmon.exe这个进程吗？”

&ensp;&ensp;&ensp;&ensp;我一瞬间感到一丝希望，顺着看下去

&ensp;&ensp;&ensp;&ensp;“我的解决方案：在任务计划板里找到     TextServicesFramework   这个，然后禁用掉就好啦，你们要是和我前提情况一样可以试试哦“

&ensp;&ensp;&ensp;&ensp;“当时我和我同学的电脑做了对比，最终我发现，他的tsf是 准备状态，我的则是运行中，我就干脆禁用掉，然后发现可行，我就赶紧来这发帖了”

&ensp;&ensp;&ensp;&ensp;正如我所见到一样，感谢大佬，不得不说，大佬是怎么想到呢！厉害了！

&ensp;&ensp;&ensp;&ensp;PS.不是很放心我就去百度了一下TSF的作用，貌似还是有点用的，后续有问题再解决吧！