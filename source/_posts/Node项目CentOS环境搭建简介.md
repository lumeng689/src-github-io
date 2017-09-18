---
title: Node项目CentOS环境搭建简介
date: 2017-09-18 14:29:02
tags:
---

## 一、服务器基环境的配置
以下的命令都建议切换到管理员身份运行：
```shell
     sudo -i
```
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

### NGINX的安装
本安装针对于CentOS7的系统。首先需要添加nginx的源:
```shell
rpm -Uvh http://nginx.org/packages/centos/7/noarch/RPMS/nginx-release-centos-7-0.el7.ngx.noarch.rpm
```
然后执行命令安装nginx：
```shell
yum -y install nginx
```
启动nginx服务
```shell
systemctl start nginx.service
```

配置与系统一起启动
```shell
systemctl enable nginx.service
```

修改配置,配置文件存放目录：
``` shell
/etc/nginx/nginx.conf
/etc/nginx/conf.d/*.conf
```

测试配置：
```shell
nginx -t -c /etc/nginx/nginx.conf
```
重启nginx
```shell
nginx -s reload
```
 或者
```shell
  service nginx restart
```

CentOS7需要关闭selinux功能,否则端口转发时会出错
编辑selinux文件
```shell
 /etc/sysconfig/selinux
```
注释掉下面代码
```shell
#SELINUX=enforcing
```
将此行代码取消注释,修改后为:
```shell
SELINUX=disabled
```
设置 SELinux 状态
```shell
setenforce 0
```

执行命令,获取SELinux状态

```shell
getenforce
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
