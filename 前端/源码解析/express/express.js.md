`express.js` 文件是 Express 框架的核心部分之一，它定义了创建 Express 应用程序的主要逻辑。下面是对该文件中代码的详细解释：

```js
  
/*!  
 * express * Copyright(c) 2009-2013 TJ Holowaychuk * Copyright(c) 2013 Roman Shtylman * Copyright(c) 2014-2015 Douglas Christopher Wilson * MIT Licensed 
 **/  
'use strict'; // 启用严格模式  
  
/**  
 * Module dependencies. 
 * */
var bodyParser = require('body-parser'); // 用于解析请求体的中间件  
var EventEmitter = require('events').EventEmitter; // Node.js 事件模块  
var mixin = require('merge-descriptors'); // 用于合并对象属性的工具函数  
var proto = require('./application'); // 应用程序原型  
var Route = require('./router/route'); // 路由构造函数  
var Router = require('./router'); // 路由器构造函数  
var req = require('./request'); // 请求原型  
var res = require('./response'); // 响应原型  
  
/**  
 * Expose `createApplication()`. */exports = module.exports = createApplication; // 导出 `createApplication` 函数  
  
/**  
 * Create an express application. * * @return {Function}  
 * @api public  
 */function createApplication() {  
  // 创建一个新的 Express 应用程序实例  
  var app = function(req, res, next) {  
    app.handle(req, res, next); // 处理传入的请求  
  };  
  
  // 将 EventEmitter 的属性混合到 app 实例中  
  mixin(app, EventEmitter.prototype, false);  
  // 将应用程序原型的属性混合到 app 实例中  
  mixin(app, proto, false);  
  
  // 暴露将被设置在请求上的原型  
  app.request = Object.create(req, {  
    app: { configurable: true, enumerable: true, writable: true, value: app }  
  });  
  // 暴露将被设置在响应上的原型  
  app.response = Object.create(res, {  
    app: { configurable: true, enumerable: true, writable: true, value: app }  
  });  
  app.init(); // 初始化应用程序  
  return app; // 返回应用程序实例  
}  
  
/**  
 * Expose the prototypes. */exports.application = proto; // 导出应用程序原型  
exports.request = req; // 导出请求原型  
exports.response = res; // 导出响应原型  
  
/**  
 * Expose constructors. */exports.Route = Route; // 导出路由构造函数  
exports.Router = Router; // 导出路由器构造函数  
  
/**  
 * Expose middleware 
 * */

exports.json = bodyParser.json; // 导出 JSON 解析中间件  
exports.query = require('./middleware/query'); // 导出查询字符串解析中间件  
exports.raw = bodyParser.raw; // 导出原始请求体解析中间件  
exports.static = require('serve-static'); // 导出静态文件服务中间件  
exports.text = bodyParser.text; // 导出文本请求体解析中间件  
exports.urlencoded = bodyParser.urlencoded; // 导出 URL 编码请求体解析中间件  
  
/**  
 * Replace removed middleware with an appropriate error message. */var removedMiddlewares = [  
  'bodyParser',  
  'compress',  
  'cookieSession',  
  'session',  
  'logger',  
  'cookieParser',  
  'favicon',  
  'responseTime',  
  'errorHandler',  
  'timeout',  
  'methodOverride',  
  'vhost',  
  'csrf',  
  'directory',  
  'limit',  
  'multipart',  
  'staticCache'  
];  
  
// 为每个已移除的中间件定义一个 getter，当访问这些中间件时，抛出错误提示用户这些中间件已被移除  
removedMiddlewares.forEach(function (name) {  
  Object.defineProperty(exports, name, {  
    get: function () {  
      throw new Error('Most middleware (like ' + name + ') is no longer bundled with Express and must be installed separately. Please see https://github.com/senchalabs/connect#middleware.');  
    },    configurable: true  
  });  
});
```
### 详细解释


1. **版权声明和严格模式**：
    
    - 文件开头包含了版权声明和许可信息。
    - `'use strict';` 启用严格模式，以捕获更常见的编程错误并提高性能。
2. **模块依赖**：
    
    - 导入所需的模块，如 `body-parser`、`EventEmitter`、`merge-descriptors`、`application`、`route`、`router`、`request` 和 `response`。
3. **导出 `createApplication` 函数**：
    
    - `exports = module.exports = createApplication;` 将 `createApplication` 函数导出为模块的主要导出对象。
4. **创建 Express 应用程序**：
    
    - `createApplication` 函数创建并返回一个新的 Express 应用程序实例。
    - 应用程序实例是一个函数，可以处理 HTTP 请求。
    - 使用 `mixin` 函数将 `EventEmitter` 和 `proto` 的属性混合到应用程序实例中。
    - 创建 `app.request` 和 `app.response` 对象，分别用于处理请求和响应的原型。
    - 调用 `app.init()` 进行初始化。
5. **导出原型和构造函数**：
    
    - 导出 `application`、`request` 和 `response` 原型。
    - 导出 `Route` 和 `Router` 构造函数。
6. **导出中间件**：
    
    - 导出常用的中间件，如 `json`、`query`、`raw`、`static`、`text` 和 `urlencoded`。
7. **替换移除的中间件**：
    
    - 定义一个包含已移除中间件名称的数组 `removedMiddlewares`。
    - 为每个已移除的中间件定义一个 `getter`，当访问这些中间件时，抛出错误提示用户这些中间件已被移除，并提供安装链接。