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


创建配置文件夹和数据文件夹
```shell
    sudo mkdir /etc/redis
    sudo mkdir /var/redis
```

将编译目录下的脚本拷贝到init.d文件夹下
```shell
    sudo cp utils/redis_init_script /etc/init.d/redis_6379
```

拷贝配置文件
```shell
    sudo cp redis.conf /etc/redis/6379.conf
```

为redis创建一个数据和工作目录
```shell
    sudo mkdir /var/redis/6379
```

编辑/etc/redis/6379.conf
* 把参数 daemonize 设置为 yes (默认是 no).
* 设置 pidfile 为 /var/run/redis_6379.pid (可以根据需要改变端口).
* 如果有需要可以改变 port 参数. 默认6379.
* 设置 loglevel 参数为合适值.
* 设置 logfile 为 /var/log/redis_6379.log
* 设置 dir 为 /var/redis/6379 (此步骤很重要!)

启动程序
```shell
    sudo /etc/init.d/redis_6379 start
```
