---
title: node-sass安装不成功解决办法
date: 2017-09-18 14:17:10
tags: node
---

# 方法一、 设置国内的镜像
windows下分两个命令执行
```bash
    SET SASS_BINARY_SITE=https://npm.taobao.org/mirrors/node-sass/  # --设置环境变量
    npm install node-sass   # 安装
```
linux下一个命令就可以了
```bash
    SASS_BINARY_SITE=https://npm.taobao.org/mirrors/node-sass/ npm install node-sass
```

# 方法二、 利用代理

```bash
  npm config set proxy http://127.0.0.1:1080
  npm install node-sass   # 安装
```
