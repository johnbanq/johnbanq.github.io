---
layout: ../../layouts/post.astro
title: 骚操作杂记：如何从grub引导进ubuntu安装盘
pubDate: 2022-04-26
description: 上星期我的一个同学手贱，把实验室电脑上的ubuntu系统搞挂了，连命令行都进不去。万般无奈之下只能重装系统......
author: "johnbanq"
excerpt: 上星期我的一个同学手贱，把实验室电脑上的ubuntu系统搞挂了，连命令行都进不去。万般无奈之下只能重装系统......
image:
  src:
  alt:
tags: ["杂谈"]
---


> 
> 临时OS，也是OS嘛~
> <br/>grub，还能这样用啊？
> <br/>—— 改自《十万个冷笑话》
>

## 背景

上星期我的一个同学手贱，把实验室电脑上的ubuntu系统搞挂了，连命令行都进不去。万般无奈之下只能重装系统。这按理来说不难，搞根刷了ubuntu安装镜像的U盘插上去，引导进去走流程就行了。

但问题，就出在了引导上：学校的IT部门给系统BIOS上了锁，这让我们没法修改启动顺序，而默认优先级就是硬盘先于U盘。

这下尴尬了，引导不进U盘，就装不了系统，我们就只能对着grub界面干发愁......

找IT？一般学校的IT，水平你懂的......

**等等，grub是有shell的！假设grub可以读取U盘上的文件系统，linux是一个OS，U盘上的liveCD也是一个OS，那么我们能不能用grub的shell引导进去呢？**

于是我查了查，还真可以：https://szymonkrajewski.pl/how-to-boot-system-from-usb-using-grub/，说干就干！

## 操作流程

把ubuntu安装U盘插到电脑上，在grub引导界面按C，进入命令行。

在命令行里运行ls，确定能否识别U盘分区。由于安装盘的文件系统格式是FAT32，按照（硬盘号，分区号）的格式，ls结果里应该会以（$硬盘号$,msdos1）的形式出现。

运行set root=($硬盘号$,msdos1)，选择这个分区为当前根目录。

运行 ls /，确认是不是真的进了ubuntu的安装盘

运行 ls /efi/boot，看看bootx64.efi是不是真在里面

运行 chainloader /efi/boot/bootx64.efi，让grub下一步把引导控制权交给这个UEFI应用

运行 boot，开始移交

没想到还真进去了，进安装界面，装好重启，收工！

## 原理

虽然操作系统课上教的引导流程还是基于MBR的，但是现代电脑基本都在使用UEFI引导流程。

UEFI会在初始化阶段结束后寻找可以运行的引导程序。默认情况下，它会按某个顺序去每个硬盘的特定分区的特定位置，在那里找符合当前计算机架构的UEFI应用（.efi文件）运行。

对使用GPT分区表的硬盘而言，这个特定分区是GUID为C12A7328-F81F-11D2-BA4B-00A0C93EC93B的分区。对使用MBR分区表的硬盘，是分区表里类型为EF的分区。这个分区必须使用FAT32文件系统，UEFI会到这个分区的/efi/boot文件夹里找和机器类型相对应的efi文件（对x86_64架构而言这个文件是bootx64.efi）。这个文件就是grub/windows启动管理器的入口。

简单来说，在UEFI引导流程中，操作系统的引导入口就是一个UEFI应用（一个EFI文件），而grub支持链式引导——把自己手上的引导控制权交给另一个UEFI应用，我让它把权力交给安装盘上的UEFI引导应用，就完事了。

## 结语

旁观者：那为啥不在开机的时候按组合键进引导媒介菜单呢

![CNM我怎么早没想到](public/booting-ubuntu-from-grub-assets/patrick-bateman-with-an-axe-banner.jpg)

一顿操作猛如虎，最后像个二百五

## 参考资料

搜到的资料：

https://szymonkrajewski.pl/how-to-boot-system-from-usb-using-grub/

关于UEFI的一些资料：

https://superuser.com/questions/731362/how-does-efi-find-bootloaders

https://zhuanlan.zhihu.com/p/25992179

《UEFI原理与编程》
