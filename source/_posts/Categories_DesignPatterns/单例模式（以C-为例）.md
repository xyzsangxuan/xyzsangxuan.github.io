---
title: 单例模式（以C#为例双检锁）
date: 2020-07-06 13:09:26
tags: 
    - 单例模式
categories: 
    - 设计模式
cover: /img/cover5.png
top_img: /img/cover5.png
mathjax: false
description: 如题
---
## 前言
* 设计模式（Design pattern），提供了在软件开发过程中面临的一些问题的最佳解决方案，是开发者必修的一门课程。主要分创建型模式、结构型模式和行为型模式。其中接下来我们要写的是单例模式，属于创建型模式。
* 单例模式，顾名思义就是只有一个实例，并且她自己负责创建自己的对象，这个类提供了一种访问其唯一的对象的方式，可以直接访问，不需要实例化该类的对象。主要有五种实现方式：懒汉式、饿汉式、双检锁、静态内部类、枚举
## 双检锁
```
using System;
using System.Collections.Generic;
/// <summary>
/// 适用于在多线程的情况下保证只有一个实例化对象的情况，例如银行的操作系统
/// </summary>
namespace DoubleLockInstance
{
	//----------------------------------
	// 双重锁定单例
	public sealed class Singleton
	{
		// 定义一个类对象，用于内部实现
		private static Singleton myInstance;
 
		// readonly   -   这个成员只能在“类初始化”时赋值  ,所谓的类初始化，就是直接在类里面初始化
		// 变量标记为 readonly，第一次引用类的成员时创建实例
		private static readonly object lockRoot = new object ();
 
		// 设置构造方法为私有，这样就不能在外部实例化类对象了
		private Singleton ()
		{
		}
 
		// 实例化对象的方法
		public static Singleton GetInstance ()
		{
			// 外部不能实例化对象，但是能调用类里面的静态方法
			// 外部需要调用这个方法来使用类对象，如果对象不存在就创建
			// 这里面使用两个判断是否为null的原因是，我们不需要每次都对实例化的语句进行加锁，只有当对象不存在的时候加锁就可以了
			if (myInstance == null) {
				// 锁定的作用就是为了保证当多线程同时执行这句代码的时候保证对象的唯一性
				// 锁定会让同时执行这段代码的线程排队执行
				// lock里面需要用一个已经存在的对象来判断，所以不能使用myInstance
				lock (lockRoot) {
					// 这里还需要一个判断的原因是，如果多线程都通过了外层的判断进行排队
					// 那将会实例化多个对象出来，所以这里还需要进行一次判断，保证线程的安全
					if (myInstance == null) {
						myInstance = new Singleton ();
					}
				}
			}
			return myInstance;
		}
	}
}
```
此实现是线程安全的。线程取消对共享对象的锁定，然后在创建实例之前检查是否已创建实例。这会解决内存屏障问题（因为锁定确保在获取锁之后逻辑上发生所有读取，并且解锁确保在锁定释放之前逻辑上发生所有写入）并确保只有一个线程将创建实例（仅限于一次只能有一个线程可以在代码的那一部分中——当第二个线程进入它时，第一个线程将创建实例，因此表达式将计算为false）。不幸的是，每次请求实例时都会获得锁定，因此性能会受到影响。

请注意，我没有像这个实现的某些版本那样锁定typeof(Singleton)，而是锁定了类私有的静态变量的值。锁定其他类可以访问和锁定的对象（例如类型）会导致性能问题甚至死锁。这是我的风格偏好——只要有可能，只锁定专门为锁定目的而创建的对象，或者为了特定目的（例如，等待/触发队列）而锁定的文档。通常这些对象应该是它们所使用的类的私有对象。这有助于使编写线程安全的应用程序变得更加容易。
## 泛型双检锁
```
using System;
using System.Collections.Generic;
/// <summary>
/// 单例模式基类模块
/// 需要具备：
/// 1.C#中 泛型的知识
/// 2.设计模式中 单例模式的知识
/// 3.多线程时加双锁
/// </summary>
namespace DoubleLockInstance
{
	//----------------------------------
	// 双重锁定单例
	public sealed class Singleton<T> where T:new()//添加泛型约束—T必须要public的无参构造函数new()才能作为i参数传进来
	{
		// 定义一个类对象，用于内部实现
		private static T myInstance;
 
		// readonly   -   这个成员只能在“类初始化”时赋值  ,所谓的类初始化，就是直接在类里面初始化
		// 变量标记为 readonly，第一次引用类的成员时创建实例
		private static readonly object lockRoot = new object ();
 
		// 设置构造方法为私有，这样就不能在外部实例化类对象了
		private T ()
		{
		}
 
		// 实例化对象的方法
		public static T GetInstance ()
		{
			// 外部不能实例化对象，但是能调用类里面的静态方法
			// 外部需要调用这个方法来使用类对象，如果对象不存在就创建
			// 这里面使用两个判断是否为null的原因是，我们不需要每次都对实例化的语句进行加锁，只有当对象不存在的时候加锁就可以了
			if (myInstance == null) {
				// 锁定的作用就是为了保证当多线程同时执行这句代码的时候保证对象的唯一性
				// 锁定会让同时执行这段代码的线程排队执行
				// lock里面需要用一个已经存在的对象来判断，所以不能使用myInstance
				lock (lockRoot) {
					// 这里还需要一个判断的原因是，如果多线程都通过了外层的判断进行排队
					// 那将会实例化多个对象出来，所以这里还需要进行一次判断，保证线程的安全
					if (myInstance == null) {
						myInstance = new T ();
					}
				}
			}
			return myInstance;
		}
	}
}
```

## 懒汉式
* 在开发过程中，倘若不涉及到多线程可采用普通的懒汉式 
```
package com.seven.exercise.testEception;
 
/**
 * 懒汉式
 * @author Seven
 *
 */
public class SingleDemo {
    
    /**
     * 私有化构造函数
     */
    private SingleDemo(){
        
    }
    
    private static SingleDemo singleDemo = null;
    
    /**
     * 提供获取实例的方法
     * @return
     */
    public static SingleDemo getInstance(){
        if(singleDemo==null){
            singleDemo = new SingleDemo();
        }
        return singleDemo;
    } 
}
```

Ps.如果想要更安全的单例模式，可以参照这篇博客
[c#中单例模式和双重检查锁](https://blog.csdn.net/zhongliangtang/article/details/81564749)