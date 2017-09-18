---
title: Express项目安全建议
date: 2017-09-18 14:33:17
tags:
---
参照文档 [http://expressjs.com/zh-cn/advanced/best-practice-security.html](http://expressjs.com/zh-cn/advanced/best-practice-security.html)

1. 使用 Helmet
   Helmet 通过适当地设置 HTTP 头，帮助您保护应用程序避免一些众所周知的 Web 漏洞。

   * csp 用于设置 Content-Security-Policy 头，帮助抵御跨站点脚本编制攻击和其他跨站点注入攻击。
   * hidePoweredBy 用于移除 X-Powered-By 头。
   * hpkp 用于添加公用密钥固定头，防止以伪造证书进行的中间人攻击。
   * hsts 用于设置 Strict-Transport-Security 头，实施安全的服务器连接 (HTTP over SSL/TLS)。
   * ieNoOpen 用于为 IE8+ 设置 X-Download-Options。
   * noCache 用于设置 Cache-Control 和 Pragma 头，以禁用客户端高速缓存。
   * noSniff 用于设置 X-Content-Type-Options，以防止攻击者以 MIME 方式嗅探浏览器发出的响应中声明的 content-type。
   * frameguard 用于设置 X-Frame-Options 头，提供 clickjacking 保护。
   * xssFilter 用于设置 X-XSS-Protection，在最新的 Web 浏览器中启用跨站点脚本编制 (XSS) 过滤器。
安装：
```
    $ npm install --save helmet
```
使用：
```
    var helmet = require('helmet');
    app.use(helmet());
```

2. 禁用 X-Powered-By 头
   如果使用 helmet.js，它会为自动屏蔽改header，没有使用的话，可以使用下面的代码禁用。
```
    app.disable('x-powered-by');
```

3. 安全地使用 cookie
需要更改session的name ，默认是 'connect.sid' ，修改为sessionId
```
    var session = require('express-session');
    app.set('trust proxy', 1) // trust first proxy
    app.use( session({
       secret : 's3Cur3',
       name : 'sessionId',
      })
    );
```

4. 检查依赖包的安全性

有两个工具可选，功能类似： nsp 和 requireSafe

```
    npm install -g nsp
    npm install -g requiresafe
```

使用nsp的话，命令为：
```
    nsp audit-package
```

使用requiresafe的话，命令为：
```
    requiresafe check
```
