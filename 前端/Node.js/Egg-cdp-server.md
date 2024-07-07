## 介绍

基于CDP协议（Chrome DevTools Protocol），通过开发拥有CDP服务端能力的Egg插件，实现Egg应用与Chrome Devtool客户端之间的双向通信，目的是在Chrome Devtool客户端上监测插件收集的应用运行时数据（日志、网络I/O、系统I/O等），类似于Node V8 inspector。

## 插件架构

插件运行时包含三部分：Master、Agent、Worker。
- Agent进程在应用中作为单例存在，负责建立CDP服务，接收来自worker进程采集的数据，并发送至各CDP客户端。
## 进程间通信


## 特性
1. 利用Devtool的Sources面板，直观查看服务器中应用的部署代码，
