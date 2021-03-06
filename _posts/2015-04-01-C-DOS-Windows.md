---
layout: post
title: C 编程、DOS、Windows 之间的关系
category: C
tags: [C, DOS, Windows, 编程]
latest: 2015年09月28日 20:01:44
---

我最开始接触的编程语言是 C，最深的记忆就是，在 Windows 的 DOS ( MS-DOS )，也就是那些酷酷的黑窗口。

DOS 和 C 语言编程
-

在进行 Win32 C 编程时，大部分都是在 DOS 环境下完成的，编程环境难免单调。为什么在 Windows 下学习 C 编程要从 DOS 环境开始呢？

一个刚刚入门的人想在 Windows 这样的多进程，多线程的操作系统下用 C 编程似乎又不太现实，因为需要了解在 Windows 下，一个 Win32 程序大体上是怎样执行的。

要对系统有比较多的了解才行，一个初学者暂时还不具备那么多的知识。

##### **说明**

Windows 上运行的不仅有程序，还有 **服务**（服务其实也是程序）。

另外，学 Win32 C 程序设计还有助于更深入地了解 Windows 的内幕和 Win32 API。

DOS 2 Windows
-

我们不能只停留在 DOS 里，而应该积极地从 DOS 向 Windows 转变。

在 DOS 时代，我们可以对 DOS 下编程留恋，但现在都是 Windows 横行霸道的时代了，我们就应用 C 语言编写 Windows 平台上的程序，**因时而变，学以致用，是时代使然** 。

整天面对"乌黑黑"的屏幕，也难怪有些人一看到一个用 C 语言描绘出来的像 Windows 窗口便以为是 C++ 的手笔。

其实，作为一种语言，可以在任何一种平台上编程，只是接口不同而已，只要找到适合该平台的编程工具即可，C 语言当然也能在 Windows下大放异彩。

眼界放宽，改变偏见，必有精彩发现。

#### 编程工具选择

在 DOS 下 C 编程，"很久" 以前我们常用 TC，在 Windows 下可以用 VC 来编程，最好用 Visual C++ 毕竟是微软的东西，只要微软一天不垮台，编程者的饭碗就不会丢。

记住：Windows操作系统是微软出的，其内幕微软是最清楚不过的了，在应用程序接口上，相信 VC 也是做得最好的。

#### 加深对 Windows 的了解

可以说编一个程序，就是用一种语言的语法形式将数据结构和表面的执行过程描述出来。

在不同的操作系统下，其程序的执行过程是不同的。我们应该对 Windows 的系统机制最起码有个大体的了解，才有可能编写windows的程序。

DOS 是单进程单线程的系统，进程从头到尾的顺序执行，而 Windows 是多进程、多线程的操作系统，是基于事件的，消息驱动的操作系统。

明白这些是在 Windows 下编程必不可少的，多学学它，你会发现 Windows  和 DOS 有很多的不同之处。

#### 比较学习

DOS 和 Windows 有许多共同和不同的地方，如果是从 DOS 学过来的话，在学习过程中不妨多进行比较，把不同的地方记下，相同的地方可以跳过。

这可以快速地了解系统的不同之处，迅速地学到东西。
