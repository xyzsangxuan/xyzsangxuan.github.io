---
title: UC-（1）Unix/Linux系统的基本概述
date: 2016-9-13 17:05:03
tags: 
    - UC
categories: 
    - C
    - UC
cover: /img/cover4.png
top_img: /img/cover4.png
mathjax: false
description: 如题
---
Unix/Linux系统下的高级c编程的主要内容：

[（1）Unix/Linux系统的基本概述](https://xyzsangxuan.github.io/2016/09/13/Categories_C/UC/)

[（2）Unix/Linux系统下的编程基础以及开发方式](https://xyzsangxuan.github.io/2016/09/15/Categories_C/UC1/)

[（3）Unix/Linux系统下的内存管理技术](https://hexo.io/)

[（4）Unix/Linux系统下的文件管理和目录操作](https://hexo.io/)

[（5）Unix/Linux系统下的进程管理](https://hexo.io/)

[（6）Unix/Linux系统下的信号处理](https://hexo.io/)

[（7）Unix/Linux系统下的进程间通信](https://hexo.io/)

[（8）Unix/Linux系统下的网络编程](https://hexo.io/)

[（9）Unix/Linux系统下的多线程编程](https://hexo.io/)


# Unix/Linux系统的简介

## Unix系统的简介
C语言：诞生于1972年
Unix操作系统诞生于1971年具有多用户，多任务，多处理器的特点
内事不决问百度，外事不决问谷歌。
1.2linux系统的简介
Linux系统是一款自由免费开放源代码的类Unix操作系统，早期Linux只是用来表示系统的内核，后来大家都习惯于将以LInux为内核的操作系统统称为Linux系统。

# GCC的基本使用
## 基本概念
原名叫GNU C   Compiler（GNU的C语言编译器）后来做了一些扩展，包括支持了c++和oc等语言的编译，因此该名为：GNU Compiler Collection（gnu编译器集合）
## 基本功能：
gcc  xxxx.c
包含四部分功能：
（1）预处理：主要实现对头文件的包含以及宏替换等 -c
（2）编译：将高级语言转换为汇编语言 
（3）汇编：将汇编语言翻译成机器指令，得到目标文件
（4）链接：主要将目标文件和库文件进行链接，生成可执行文件
## 常见的编译选项
遇见xxxx_t的数据类型都认为是int类型

必须熟练掌握的选项
-E  进行预处理     预处理的结果默认输出到控制台，使用gcc  -E  xxx.c  -o  xxx.i将于处理结果定义到xxx.i文件中，预处理之后的文件主要包含：头文件，类型的别名，各种函数的声明等等。

-S    进行编译处理    生成汇编文件xxx.s 
-c    进行汇编处理，生成目标文件xxx.o
gcc/cc xxx.o    链接处理，生成可执行文件a.out
gcc/cc -E xxx.c -o  xxx.i=>预处理，生成.i文件
gcc/cc -S xxx.i/xxx.c =>编译，生成.s文件
gcc/cc -c xxx.s/xxx.i/xxx.c =>汇编，生成.o文件
gcc/cc  xxx.o/xxx.s/xxx.i/xxx.c  =>链接生成a.out文件

（2）熟悉的选项
-std：主要用于指定编译时遵循的c标准
-Wall：主要用于尽可能的产生警告信息
-Wellor：主要用于将警告当错误进行处理

（3）了解的选项
-v 主要用查看gcc的版本信息
-g主要用于生成调试信息（gdb调试）
-O主要用于进行优化处理
-x主要用于显示指令指定源代码的编程语言

（4）扩展的选项：
man gcc/cc 查看gcc更多的选项信息。
2.4常见的文件后缀
.h	头文件
.c	源文件
.i	预处理之后的文件
.s	汇编文件
.o	目标文件

.a	静态库文件
.so	共享库文件

# 多文件结构的编程
3.1	多文件的结构
.h	头文件，主要存放结构体的定义，函数的声明等等
.c	源文件，主要存放函数的定义/变量等
.a	静态库文件，主要对功能文件的打包
.so	共享库文件，主要对功能代码的打包
3.2	头文件中的详细内容
（1）头文件的卫士
```
#ifndef xxx_H
#define xxx_H
#endif
```
（2）包含其他的头文件
```
#include <stdio.h>
#include <stdlib.h>
```
（3）宏定义
```
#define PI 3.14159265354
```
（4）数据类型的定义以及给类型起别名
```
typedef struct Node
{
int data;
struct Node * next;
}Node;
```
（5）变量/函数的声明
```
extern/*外部的*/ int num;
void show(void);
```
注：变量或者函数的定义不要放在头文件中，避免出现变量/函数的重定义的错误

4：预处理指令
4.1	复习预处理指令
```
#include		主要用于包含头文件
#define		进行宏定义
#undef		取消宏定义
#if			如果......
#ifdef		若果定义
#ifndef		如果没有定义
#elif			否则如果
#else		否则
#endif		结束如果
```
4.2学习新的预处理指令
```
#line  整数n		表示从下一行起，行号变更为第n行
#warning 字符串	表示产生一个警告信息
#error 字符串		表示产生一个错误信息
```
```
注：#if主要用于在编译阶段进行条件的判断
if主要用于在运行期间进行条件的判断
#pragma  GCC dependency 文件名
```
表示当前文件依赖于指定的文件名，如果指定的文件最后一次修改时间晚于当前文件，则产生警告信息
扩展：文件要用“”或者<>
```
#pragma GCC poison  标识符
```
表示设置指定的标识符为毒药，一旦使用该标识符，产生错误信息；使用宏定义可以偷偷略过
```
#pragma pack(整数n)
```
表示按照n的倍数进行对齐和补齐，超过4，还是按照4的倍数进行，并且对齐和补齐的形式必须是2的较小次方；调整对齐和补齐方式就是为了节省内存

扩展：
对齐：表示指结构体的每一个成员的起始地址都是该成员的整数倍
补齐：表示整个结构体的大小是这个结构体的最大成员的整数倍，如果不够，则补齐
4.3	预定义宏
```
__BASE_FILE__		获取正在编译的文件名  %s
__FILE__			获取当前宏所在的文件名 %s
__LINE__			获取当前宏所在的行号  %d
__FUNCTION__		获取当前宏所在函数名	%s
__DATA__			获取日期		%s
__TIME__			获取时间		%s
```