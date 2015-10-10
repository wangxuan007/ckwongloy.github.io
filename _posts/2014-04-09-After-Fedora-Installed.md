---
layout: post
title: Fedora 安装结束后的那些事
category: Auxiliary
tags: [Linux, Fedora]
latest: 2014年04月09日 11:01:21
---

删除多余的内核
-

内核升级后就旧版本内核或者安装好后出现在启动菜单中不想看见的内核怎么删除？ 

由于 Fedora 更新升级后会留下旧的内核，时间久了有必要清除陈旧的内核，方法如下：

1、查看当前系统中已安装的内核相关包

```
# rpm -qa | grep kernel

abrt-addon-kerneloops-1.1.14-1.fc13.x86_64 
kernel-2.6.34.7-66.fc13.x86_64 
arm-gp2x-linux-kernel-headers-2.6.12.0-4.fc12.noarch
kernel-devel-2.6.34.7-61.fc13.x86_64 
kernel-devel-2.6.34.8-68.fc13.x86_64
kernel-headers-2.6.34.8-68.fc13.x86_64
kernel-devel-2.6.34.7-66.fc13.x86_64
kernel-2.6.34.8-68.fc13.x86_64
```

或者 ( 推荐  )

```
# rpm -q kernel

kernel-2.6.34.7-66.fc13.x86_64
kernel-2.6.34.8-68.fc13.x86_64
```

2、查看当前使用的内核

```
# uname -r 
```

2.6.34.8-68.fc13.x86_64

3、确定要删除的内核

这里为：kernel-2.6.34.7-66.fc13.x86_64

4、删除内核

# yum remove kernel-2.6.34.7-66.fc13.x86_64  <--推荐 或者： rpm -e kernel-2.6.34.7-66.fc13.x86

6、说明： 

_1.使用yum remove删除， yum 会自动移除 ： /boot/grub/menu.lst 中的相关启动项，不用再手动修改启动文件。 

_2.自动清理内核：grub2-mkconfig -o /boot/grub2/grub.cfg 查看所有内核：rpm -qa | grep kernel

2.无线都能上有线能识别网卡驱动并已经获取到ip地址却还是不能上外网？

3.音视频解码器？ 

加入163源，不然不能安装 MP3 和RM解码器 
	
```
su -c 'yum localinstall --nogpgcheck http://mirrors.163.com/rpmfusion/free/fedora/rpmfusion-free-release-stable.noarch.rpm http://mirrors.163.com/rpmfusion/nonfree/fedora/rpmfusion-nonfree-release-stable.noarch.rpm
```

安装 mp3 和其它音频支持

```
sudo yum install gstreamer-plugins-good gstreamer-plugins-bad gstreamer-plugins-ugly libtunepimp-extras-freeworld xine-lib-extras-freeworld
```

视频解码库

```
sudo yum install ffmpeg ffmpeg-libs gstreamer-ffmpeg libmatroska xvidcore
```

4.KMplaer

um install kmplayer即可。

5."/var/run/yum.pid 已被锁定,PID 为 3021 的另一个程序正在运行。" 


直接在终端运行 rm -f /var/run/yum.pid 将该文件删除，然后再次运行yum。


Fedora KDE
-

Command:yum-complete-transactionProblem:1. root 账户不能运行 Chrome 


Fedora上编程环境的搭建和配置
-

### Eclipse的下载和安装以及配置下载和安装

用系统自带的“软件”里面的开发工具选择下载。完了“软件”自动安装。

#### 配置

下载 CDT 插件拓展 C/C++ 编程环境

### Code::Blocks的下载安装和配置下载和安装

同 Eclipse 配置：一开始安装好后提示没有合适的编译器，这时我们先在终端更新软件包：`yum update`。