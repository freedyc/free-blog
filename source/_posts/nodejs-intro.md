---
title: Nodejs 介绍
date: 2021-12-19 19:55:54
tags: nodejs
---

**# Nodejs 简单介绍**

\1. Node.js是一个基于Chrome V8引擎的Javascript运行环境。

\2. Node.js使用了一个事件驱动、非阻塞I/O的模型，轻量又高效



**## Nodejs 的非阻塞 I/O**

\1. I/O 即 Input/Output，一个系统的输入和输出

\2. 阻塞I/O和非阻塞I/O的却别就在于系统接受输入再到输出期间，能不能接受其他输入



**## Node.js异步编程 - callback**

\1. 回调函数格式规范

​    \- error-first callback

​    \- node-style callback

\2. 第一个参数是error, 后边参数是结果



**## 异步 IO**

EventLoop是什么 ? 



一个循环，每次循环叫tick每次循环的代码叫task



**## RPC调用**

\1. Remote Procedure Call（远程过程调用）



\2. 和Ajax有什么相同点

\- 都是两个计算机之间网络通信

\- 需要双方约定一个数据格式



\3. 不同点 

\- 不一定使用DNS作为寻址服务

\- 应用层协议一般不使用 HTTP

\- 给予 TCP 或 UDP 协议



\4. 寻址/负载均衡: RPC：使用特有服务进行寻址

\5. TCP 通信方式: 单工通信、 半双工通信、全双工通信

\6. 二进制协议，更小的数据包体积、更快的编解码速率





**## nodejs 可以让我们前端做的更多**



**### BFF(Backend for frontend) 服务于前端的后端**

\> 通俗的讲是浏览器和服务器端的中间渲染层



\> 把后台微服务返回的数据组装成前端所需的数据



\1. 对用户侧提供HTTP服务

\2. 使用后端RPC服务





**### SSR (ServerSideRendering) 服务端渲染**

特性：

\1. 提高搜索引擎抓取网络的效果

\2. 提高网页首屏加载的速度



**## npm 上的大神**



[TJ Holowaychunk](https://github.com/tj) 作品：

\- node版本管理工具：[n](https://github.com/tj/n)，

\- 命令行工具：[Commander.js](https://github.com/tj/commander.js)

\- Reids会话存储：[connect-redis](https://github.com/tj/connect-redis)

\- 基于generators流程控制: [co](https://github.com/tj/connect-redis)

\- git 操作: [git-extras](https://github.com/tj/git-extras)



[Mathias Buus](https://github.com/mafintosh) 作品：

\- 视频播放器[playback](https://github.com/mafintosh/playback)

\- CSV 流解析器[csv-parser](https://github.com/mafintosh/csv-parser)



[Dominictarr](https://github.com/dominictarr) 作品：

\- 流解析 JSON.parse[JSON Stream](https://github.com/dominictarr/JSONStream)

\- 随机姓名[random-name](https://github.com/dominictarr/random-name)

\- 点对点日志存储[ssb-server](https://github.com/ssbc/ssb-server)
