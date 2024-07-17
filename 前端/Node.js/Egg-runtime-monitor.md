> 环境：Node v12+、Egg v2+
## 介绍


## 能力

OMS接入插件后，可以便捷进行以下Node端调试。
### Node对外请求监测

### Sequelize操作监测
### 错误堆栈还原

### 部署环境代码快速预览

应用部署后，某些情况我们需要检查部署环境中的产物代码（构建中涉及条件编译的部分是否正确、部署后功能不生效/不存在时验证某些功能代码是否正确更新等等），此时可以切换到“Sources”面板进行产物代码的快速预览。插件会扫描并整理应用部署根目录下的文件结构，并在Devtool需要时再返回相应内容。

![部署环境代码快速预览](https://res.jscssfunny.com/fe/appcreator/asset/material/1720971366160-erm-1.png?x-oss-process=style/hq)






基于CDP协议（Chrome DevTools Protocol），通过开发拥有CDP服务端能力的Egg插件，实现Egg应用与Chrome Devtool客户端之间的双向通信，目的是在Chrome Devtool客户端上监测插件收集的应用运行时数据（日志、网络I/O、系统I/O等），类似于Node V8 inspector。

## 插件架构

插件运行时包含三部分：Master、Agent、Worker。
- Agent进程在应用中作为单例存在，负责建立CDP服务，接收来自worker进程采集的数据，并发送至各CDP客户端。
## 进程间通信


## 特性
1. 利用Devtool的Sources面板，直观查看服务器中应用的部署代码，


## 依赖包

- "fast-glob": "^3.3.2"
- "sdk-base": "^4.2.1"
- "cluster-client": "^3.7.0"
- nanoid
- egg-redis
## QA
### tsc编译时node_module中相关库报错：
tsconfig中设置："skipLibCheck": true


"build": "easy build --devtool source-map",

## 相关资料

### sourceMap
- [sourceMap协议详情](https://sourcemaps.info/spec.html#h.lmz475t4mvbx)
- [stack-trace](https://www.npmjs.com/package/stack-trace)
- [egg-onerror](https://github.com/eggjs/egg-onerror/blob/master/lib/error_view.js)
- https://zhaomenghuan.js.org/blog/chrome-devtools.html#electron-%E9%9B%86%E6%88%90-devtools
- [V8堆栈跟踪api](https://v8.dev/docs/stack-trace-api)
- https://zhuanlan.zhihu.com/p/703285960?utm_medium=social&utm_psn=1789956778395582465&utm_source=wechat_session

## redis

### cdp客户端连接管理
单节点和多节点部署下，所有cdp客户端在建立连接时都将其唯一id保存到redis的set中，set的有效期是1d。
