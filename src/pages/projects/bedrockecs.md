---
layout: ../../layouts/post.astro
title: BedrockECS
description: 一个基于ECS & 数据库的MC:BE服务端原型
pubDate: 2022-10
endDate: 2022-11
image:
  src: /bedrock-ecs-assets/Bedrock_JE2_BE2.webp
  alt:
tags: ["软件工程"]
---

>
>    好，我行，我上！
>    <br/> —— johnbanq
>

## 摘要

我们在此提出BedrockECS——一种基于类函数式/ECS的Minecraft基岩版服务器架构，及其原型实现。我们讨论了现有工作在架构上的问题，以及在开发运维体验上的缺失。并从游戏程序的本质进行推导，结合ECS架构与类函数式编程，提出了我们的架构。我们的工作继承了类函数式编程在解耦和可理解性上的优势，ECS架构在性能，可扩展性上的优势。而这两个范式的结合又令热重载和代码生成变得容易实现，令可观测性变得易于达成。而这些都是良好开发运维体验的基础。我们相信这是一个大有可为的设计思路，可供后续工作作为参考。

## 代码
* Github

## 博文目录
* 关于我写了个Minecraft基岩版服务端这件事（一）：动机与目标
* 关于我写了个Minecraft基岩版服务端这件事（二）：设计与实现
* 关于我写了个Minecraft基岩版服务端这件事（三）：回望与尾声