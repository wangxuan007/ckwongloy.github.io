---
layout: post
title: 《The C Programming Language》 学习笔记
category: C
tag: C
latest: 2015-12-28 17:02:44
---

#### 流

流是与磁盘或者其他外围设备关联的数据的源或者目的地,指的是 一个地址,由于 UNIX 中磁盘和外围设备都被看作文件,所以流 其实也就是文件指针。

打开一个流,将把该流和一个文件或设备连接起来,关闭流则会断开这种链接。

打开一个文件,将返回一个指向 FILE 类型对象的指针,该指针记 录了控制该流的所有必要信息。

每个程序开始执行的时候,stdin、stdout、stderr 这三个流已 经处于打开的状态。

C 标准库中提供了两种类型的流:文本流和二进制流。 文本流

由文本行组成的序列,每一行包含 0 或者多个字符,并以 `\n` 结尾。

在某些环境中,可能需要将文本流转换为其他表示形式,比 如把  `\n` 映射成回车或者换行。或者,从其他表示形式转换 为文本流。

- 二进制流

二进制流是由未经过处理的字节构成的序列,这些字节记录着内部数据,并具有以下特征:如果在同一系统中写入二进制流,然后再读取该二进制流,则读出和写入的数据完全相同。

然而在 UNIX 中,文本流和二进制流是相同的。

#### 头文件

里面存放的通常是对函数原型的定义宏定义。

头文件的包含顺序是任意的,并可以多次包含,但是必须在使用头

文件中的声明之前包含头文件。

`<stdio.h>` 中定义的输入输出函数、类型以及宏的数目,几乎占了 整个 C 语言标准库的三分之一。

#### 文件指针和文件描述符

调用 open() 等低级 I/O 系统调用接口返回的是文件描述符。 调用 fopen() 等高级输入输出标准库函数返回的是一个文件指针。

文件指针记录的是控制文件流的所有必要信息，文件指针和流指的是一个东西。
  
#### 系统调用与标准库

标准库是某种语言为了实现一些功能而编写的函数集合。

系统调用是指操作系统内的函数,可以被用户程序所调用,用以完成标准库中没有的功能。

ANSI C 的标准库是以 UNIX 为系统建立起来的。

标准库并不是 C 语言本身的构成部分,但是支持标准 C 的实现会 提供该函数库中的函数声明、类型以及宏定义。

#### 预处理

包括头文件包含的 include 指令,宏定义的 define 等预处理指令 也包括 ifdef else endif undef 等条件编译指令

#### UNIX 系统接口

- 文件描述符

UNIX 中一切都是文件系统中的文件,键盘和显示器也一样。所以所有的输入输出都要通过读文件或者是写文件来完成。而程序的功能就是接受数据的输入,计算,然后输出计算结果,所以文件可以被看成是程序与外围设备通信的接口。

当程序需要读写文件的时候,首先要做的事情就是打开文件或者创建文件。如果通过了系统检测文件是否存在和检测用户权限是否匹配,那么操作系统将向该程序返回一个很小的非负整数,也被称为文件描述符。

任何时候对文件的输入输出都是通过文件描述符来标识文件的,而非文件名。

UNIX 中的文件描述符类似于 Windows 中的文件句柄。 系统负责维护已打开文件的所有信息,而用户程序只能通过文件描述符引用文件。

UNIX 中最常见的文件描述符是:

0:标准输入:默认与键盘相关
1:标准输出:默认与显示器相关 
2:标准错误:默认与显示器相关
这三个文件在通过 Shell 运行一个程序的时候,都会被 UNIX 所打 开,只要执行的程序是从文件 0 中读数据,从文件 1、2 中写数据,那么程序就不用再关心文件的打开问题而直接进行输入输出。

- 文件重定向

在 Shell 中,可以通过 `<` 和 `>` 分别来重定向程序的 I/O:

```
prog < 输入文件名 > 输出文件名
```

此时,与文件描述符 0 和 1 相关联的文件不一定是键盘和显示 器,而被重新赋值为用户指定的文件。而文件描述符 2 映射的文件通常也是显示器,所以上面的程序执行时的所有错误信息仍然会
被输出到显示器。

与管道相关联的 I/O 原理也类似。Shell 下程序的执行对文件赋值的改变都不是由程序来完成而是由 Shell 来完成的。所以,只要程序使用 0 作为输入,1 和 2 作为输出,它就不会知道程序的输入从哪里来、输出到哪里去。

- 低级 I/O:read 和 write

UNIX 处理输入和输出是通过 read 和 write 这两个系统调用来实
现的。

C 语言中使用这两个系统调用类似如下:

``` c
int n_read = read( int file_descriptor, char * buf, int bytes ) ;
int n_write= write( int file_descriptor, char * buf, int bytes ) ;
```

其中,第一个参数指文件描述符,第二个参数指程序中存放读或写的数据的字符数组,第三个参数指要传输的字节数。

其中,数据读写的字节数可以为任意大小,但是更大的值调用这两 个函数可以获得更高的效率,因为系统调用的次数减少了。最常用 的值是 1,代表的是无缓冲读写文件,但是最常见的值是 1024、4096 这样的与外围设备的物理大小相应的值。

两个调用的返回值都是实际传输的字节数。其中: 读文件时,read() 函数的返回值可能会小于请求的字节数。如果返回 0 则表示已达文件末尾;如果返回 -1 则表示发生了某种错误。 写文件时,write() 函数的返回值在正常情况下应该与请求写入的字节数相同,若不相等,则说明发生了错误。

open creat close unlink

除标准输入、标准输出、标准错误这三个文件的读写不需要显示地 打开/创建之外,其他任何文件的读写都必须在读写之前显示地使 用 open/creat 这两个系统调用显示地打开。

open() 返回一个 int 类型的文件描述符,如果发生错误,比如打开 了一个不存在的文件则返回 -1。它的定义如下:

``` c
int open( char *name, int flags, int perms ) ;
```

与 fopen() 一样,第一个参数代表的是包含文件名的字符串,第二 个参数说明了以何种方式打开文件,其值为 int 类型,如下所示:

``` c
O_RDONLY # 以只读打开 O_WRONLY # 以只写打开 O_RDWR # 以读写打开
```

这些常量定义的头文件可能会由于 UNIX 版本的不同而不同,比 如 System V UNIX 是在 <fcntl.h>,而 Berkeley BSD UNIX 的是 在 <sys/file.h> 中定义。
第三个参数代表的是执行 open() 操作的权限。 同理,creat() 的定义如下:
   
``` c
int creat( char *name, int perms ) ;
```

如果 creat 以 perms 指定的权限成功创建了一个文件,则返回该文 件的文件描述符,否则返回 -1。
如果创建一个已经存在的文件,并不会报错,而是会把已经存在的 文件长度截断为 0,即丢弃原文件的内容。