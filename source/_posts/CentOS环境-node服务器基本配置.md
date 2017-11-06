---
title: CentOS环境 node服务器基本配置
date: 2017-11-06 11:44:10
tags: CentOS Node PM2
---

### node环境安装

 执行以下命令：
 ```shell
     curl --silent --location https://rpm.nodesource.com/setup_6.x | bash -
 ```
 然后执行:
  ```shell
     yum -y install nodejs
  ```

### pm2安装
pm2和forever是启动Nodejs服务常用到的两个工具。使用这两个指令可以使node服务在后台运行，另外它们可以在服务因异常或其他原因被杀掉后进行自动重启。
当前项目选用pm2。
```shell
   npm install -g pm2
```

### MongoDB的安装

首先配置yum

```shell
  vi  /etc/yum.repos.d/mongodb-org-3.0.repo
```

然后填入内容:

```shell
   [mongodb-org-3.4]
   name=MongoDB Repository
   baseurl=https://repo.mongodb.org/yum/redhat/$releasever/mongodb-org/3.4/x86_64/
   gpgcheck=1
   enabled=1
   gpgkey=https://www.mongodb.org/static/pgp/server-3.4.asc
```

最后执行命令进行安装

```shell
   yum -y install mongodb-org
```

手动创建数据文件夹

```shell
   mkdir -p  /data/db
```

启动mongod服务

```shell
   service mongod start
```

### Redis的安装

首先检查环境
```
    yum install -y gcc-c++
    yum install -y tcl
    yum install -y wget
```

下载redis文件
```shell
    wget http://download.redis.io/releases/redis-3.2.6.tar.gz
```

解压并编译
```shell
    tar xzf redis-3.2.6.tar.gz
    cd redis-3.2.6
    make
```
如果出现错误 jemalloc/jemalloc.h: No such file or directory,则使用下面命令：

```shell
    make MALLOC=libc
```

将编译后的redis-server复制到/usr/bin

```shell
    cp src/redis-server /usr/bin/
```
