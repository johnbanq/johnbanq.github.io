---
layout: ../../layouts/post.astro
title: "并发编程：参考与推荐资源清单"
pubDate: 2021-06-01
description: 这里就是我在写作《并发编程：内存模型无责任导引》时读过看过（或者应该看过）的一些资源，以及我对它们的一些评价......
author: "johnbanq"
excerpt: 这里就是我在写作《并发编程：内存模型无责任导引》时读过看过（或者应该看过）的一些资源，以及我对它们的一些评价......
image:
  src:
  alt:
tags: ["软件工程", "并发编程"]
---

这里就是我在写作《并发编程：内存模型无责任导引》时读过看过（或者应该看过）的一些资源，以及我对它们的一些评价。下面的资料集合大致可以分成语言内存模型和处理器内存模型两块。语言内存模型按语言进一步细分，处理器内存模型按内存模型的“强度”进一步细分。我会试着从每个细分小结里选出一个资源作为强推，如果你只打算看一样，就去看它吧！

正如文中所说，下面涉及到的资源基本都是标准，经典或者需要真正对付并发问题的家伙写的东西。不过也是挂一漏万，建议读者从这些地方着手，围绕着作者/会议去进一步搜索。

我想阅读学习也遵循八十二十原则——也许二手资料（例如我的文章）能让你用百分之二十的时间理解百分之八十，但是如果你想要剩下的百分之二十，就只能自己去挖。

祝你好运！

PS：下面提到的书籍可以去搜罗各个公众号，英文书也可以去libgen。libgen的地址谷歌百度都可，我就不贴了，不然这个站可能要危。

## 语言内存模型

### 通用

#### 参考书籍

《The Art of Multiprocessor Programming》（中文名：《多处理器编程的艺术》）

评价：没看，传说中的并发编程圣经。据说难度不低，但不够实用。

《Is Parallel Programming Hard, And, If So, What Can You Do About It?》（中文名：《深入理解并行编程》）

评价：建议希望深入了解并发编程的程序员阅读。Paul E. McKenney老先生的大作，给C/偏底层程序员的经典作品。涵盖了编写并发程序的基本工具，有锁和无锁数据结构的编写方式，证明并发程序正确性的方法等等有用的工具技巧。这本书同时讨论了访存顺序问题和编译器与CPU缓存系统的关系。另外，可惜中文译名丢掉了英文名里的那股趣味，直译应该是《并发编程难吗？如果难的话，我们能做些啥呢？》，不妨简称《并发两问》:D

#### 其它资料

[Preshing on Programming](https://preshing.com/20120612/an-introduction-to-lock-free-programming/)

评价：Preshing关于无锁并发编程的博文。也是一篇入门导引级别的文章，想的话可以去那里转转。

#### 使用建议

酌情阅读吧¯\\_(ツ)_/¯，这两本书一本比一本难啃，除非你真打算彻底精通这玩意儿，我不是很建议你去看。

### Java

#### 参考书籍

《Java Concurrency in Practice》（中文名：《Java并发编程实战》）

评价：Java并发编程必读。涵盖了如何使用语言里的各种并发工具（synchronized，j.u.c等），一些基本的使用模式（例如如何优雅关闭队列），最后提了一嘴Java内存模型。这本书没讲无锁编程，想知道的可能要去C++社区蹭点。

《深入理解Java虚拟机》第12章与第13章

评价：已经有第三版了。面试题之源，所以写Java的迟早都要读。我在正文里也吐槽过里面过时的主内存-工作内存模型，真的不只是修订了，整个砍掉了。先行发生（happens-before）模型是对的，顺带提了一嘴准备发布的Project Loom，还不错。

《Java并发编程的艺术》

评价：没看，但看到有人推荐这本书，但是豆瓣评分看起来不是特别理想。

#### 其它资料

[JMM Pragmatics](https://shipilev.net/blog/2014/jmm-pragmatics/)

评价：打算真正看懂Java内存模型的一定要看。红帽工程师，Hotspot JVM开发者的手笔。而且被Brian Goetz（Java语言架构师）和Doug Lea（j.u.c作者与维护者）审阅过。彻底解读了Java语言规范第17章的重要部分。

[Close Encounters of The Java Memory Model Kind](https://shipilev.net/blog/2016/close-encounters-of-jmm-kind/)

评价：如果JMM Pragmatics说的是JMM是什么，这说的就是JMM不是什么。内容就是一堆对JMM常见的误解，可以用来检查自己的理解。

[shipilev的个人网站](https://shipilev.net)

评价：这些东西的作者的个人网站，上面也有其它关于Java并发的演讲，自己去逛吧



[The JSR-133 Cookbook for Compiler Writers](http://gee.cs.oswego.edu/dl/jmm/cookbook.html)

评价：打算深入理解的人可以一看，Doug Lea的作品。讲JVM如何在各种硬件上实现Java内存模型，可惜有点年头了。

[Using JDK 9 Memory Order Modes](http://gee.cs.oswego.edu/dl/html/j9mm.html)

评价：真的打算深入理解的人可以一看，还是Doug Lea的作品。讲如何使用和理解Java 9 VarHandle里各种奇怪内存访问方式的用法。建议在看它之前了解C++的内存模型，因为看来就是抄它们的。

[Doug Lea的个人网站](http://gee.cs.oswego.edu/)

评价：上面两个文章的作者的个人网站，不少东西都有些年头了，但是还是有些有趣的东西，例如[AQS的原版论文](http://gee.cs.oswego.edu/dl/papers/aqs.pdf)



[Java 语言规范 第17章](https://docs.oracle.com/javase/specs/)

评价：真的打算深入理解的人必看，标准规范，看完第17章就真的知道内存模型到底长啥样了。

[JSR-133 Public Review版本](http://www.cs.umd.edu/~pugh/java/memoryModel/PostPublicReview.pdf)

评价：如果你打算看JSR-133的话，建议你看Public Review版本。因为里面包含了一些设计动机方面的内容，形式定义就算了，还是去看规范吧。有趣的是，这份资料和Doug Lea早年写的一本书是我在英文资料里为数不多找到原子性，可见性，有序性三大定义的地方。破案了？

[Java内存模型项目页](http://www.cs.umd.edu/~pugh/java/memoryModel/)

评价：存放和JSR-133修订相关的资料的网站，考古学家可以去逛逛

#### 使用建议

建议先阅读《深入理解Java虚拟机》第12章与第13章了解内存模型的基础，再阅读《Java并发编程实战》学习并发编程，之后再考虑《Java并发编程的艺术》。如果真的打算弄清楚Java内存模型，建议先阅读JMM Pragmatics和JMM Unlearning experience起手，然后再阅读语言规范第17章和JSR-133。如果打算知道内存模型发展趋势的话，先了解C++的内存模型，再去阅读Using JDK 9 Memory Order Modes。

### C++

#### 参考书籍

《C++ Concurrency in Action》（中文名：C++并发编程实战）

评价：有第二版了，搞C++的看吧，因为讲C++并发的书籍不多，估计你没得选。曼宁出版社+标准提案作者，讲了工具用法，内存模型，无锁编程等。感觉第5章内存模型举的例子有些晦涩了，本质上还是happens-before。

《Linux多线程服务端编程》

评价：翻了一点点，muduo作者陈硕的作品。重点貌似不在多线程上，但是不少人提到这个¯\\_(ツ)_/¯

#### 其它资料

这个我有不少：

**（强推）[C++ atomic<> Weapons 第一部分](https://www.youtube.com/watch?v=A8eCGOqgvH4) [第二部分](https://www.youtube.com/watch?v=KeLBd2EJLOU)**

评价：走进C++内存模型最好的讲座之一。__标准律师们的王，__（前）C++标准委员会主席Herb Sutter教你做事系列。也是入门导引类型的讲座，从根本问题引出acquire-release，然后讨论各种实现，最后提一嘴relaxed atomics和volatile。我文章的acquire-release模型有一块就是从这里嫖走的。

[Lock-Free Programming (or, Juggling Razor Blades) 第一部分](https://www.youtube.com/watch?v=c1gO9aB9nbs&ab_channel=CppConCppCon) [第二部分](https://www.youtube.com/watch?v=CmxkPChOcvw&ab_channel=CppCon)

评价：讲如何编写无锁数据结构的讲座。Herb Sutter继续教你做事系列。

[Live Lock-Free or Deadlock (Practical Lock-free Programming) 第一部分](https://www.youtube.com/watch?v=lVBvHbJsg5Y&ab_channel=CppCon) [第二部分](https://www.youtube.com/watch?v=1obZeHnAwz4&t=2249s&ab_channel=CppCon)

评价：另一个无锁编程讲座。如果Herb Sutter是在吓你，让你不要玩骚操作的话。Fedor Pikus就是在告诉你如何正确地玩骚操作。讲的非常漂亮。

[Cppcon 油管频道](https://www.youtube.com/channel/UCMlGfpWw-RUdWX_JbLCukXg)

评价：Cppcon可能是我见过的质量最高的语言社区会议之一了，上面的后两个讲座全部来自cppcon，上面还有大量我没提及的关于并发的好讲座，去看吧！

[cppreference上关于内存顺序的描述](https://en.cppreference.com/w/cpp/atomic/memory_order)

评价：关于C++规范里内存顺序的人话版。我不是标准律师，真读不动规范。

#### 使用建议

这个建议有点不好给。我认为可以先看《C++ atomic<> Weapons》打底，然后去看《C++ Concurrency in Action》的无锁编程部分试验一下自己的理解，最后去看cppcon上的讲座，最后再去怼语言内存模型

### 其它语言（Golang / Rust / ...）

[golang内存模型标准](https://golang.org/ref/mem)

评价：golang作为一个在内存模型上躺平任艹的语言，语言标准其实非常简单，理解了happens-before看起来就是砍瓜切菜，用golang的去看吧

**（强推）[Russ Cox关于golang内存模型的讲座的PPT](http://nil.csail.mit.edu/6.824/2016/notes/gomem.pdf)**

评价：也是入门导引级别的资料，从并发编程基本问题到硬件内存模型，再到SC-DRF和Java/C++的内存模型，最后再到golang的内存模型。深入浅出，不错。

[Explaining Atomics in Rust](https://cfsamsonbooks.gitbook.io/explaining-atomics-in-rust/)

评价：解释Rust里relaxed atomic的一篇长文，我就放这里供各路Rustacean参考。

## 处理器内存模型

### 通用

《A Primer on Memory Consistency and Cache Coherence》

评价：如果让我挑一本讲处理器内存模型的教科书，估计我会挑它。深入讲解了处理器对缓存一致性的实现，以及各种常见的处理器内存模型。这本书有第二版，相当的新。

### 强内存一致性模型（x86）

[《Intel® 64 and IA-32 Architectures Software Developer Manuals:System Programming Guide》8.1-8.3节](https://software.intel.com/content/www/us/en/develop/download/intel-64-and-ia-32-architectures-sdm-combined-volumes-3a-3b-3c-and-3d-system-programming-guide.html)

评价：x86内存模型的标准规范，不长。8.1讲原子性保证，8.2和8.3讲访存顺序保证。不想读的话记住用lock指令前缀，读可能被重排到写的后面即可。

### 弱内存一致性模型（ARM/RISC-V）

**（强推）[RISC-V Memory Consistency Model Tutorial](https://www.youtube.com/watch?v=QkbWgCSAEoo)**

评价：RISC-V 2018峰会上的一个workshop。一个搞内存模型的博士对RISC-V内存模型的讲解。为了引出RISC-V内存模型，之前也讲了一下x86和ARM的内存模型。算是一个不错的简介，不打算了解RISC-V内存模型的也可以看看。

[A Tutorial Introduction to the ARM and POWER Relaxed Memory Models](https://www.cl.cam.ac.uk/~pes20/ppc-supplemental/test7.pdf)

评价：一群学者做了一堆研究问了一堆人之后写的关于PowerPC和ARM内存模型的报告。前面主要在介绍x86/ARM内存模型的心智模型，后面就是在各种玄学litmus test了。建议看看前面即可。

## 其它清单

[OpenJDK上的JMM阅读清单](http://cr.openjdk.java.net/~jrose/jvm/JMM-Readings.html)

评价：某个OpenJDK项目里的人列出来的Java内存模型阅读清单，和本清单有不少重合

