---
title: Node项目ubuntu环境搭建简介
date: 2017-09-18 14:30:48
tags:
---

### 〇 查看ubuntu的版本
执行命令：
```shell
    cat /proc/version  # 查看内核版本
    uname -a          # 查看内核版本
    cat /etc/issue  # 方法一
    lsb_release -a # 方法二
    cat /etc/lsb-release # 方法三
```


```
sudo apt-get install python-software-properties
sudo apt-get install software-properties-common
sudo add-apt-repository ppa:rwky/graphicsmagick
sudo apt-get update
sudo apt-get install graphicsmagick
```

## 一、服务器基环境的配置

### node环境安装
 执行以下命令：
 ```shell
     curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
 ```
 然后执行:
  ```shell
     apt-get install nodejs
  ```

### pm2安装
pm2和forever是启动Nodejs服务常用到的两个工具。使用这两个指令可以使node服务在后台运行，另外它们可以在服务因异常或其他原因被杀掉后进行自动重启。
当前项目选用pm2。
```shell
   npm install -g pm2
```

### NGINX的安装

### MongoDB的安装

1. 导入公钥

```shell
  sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 0C49F3730359A14518585931BC711F9BA15703C6
```


2. 创建list文件：
 12.04系统下：

```shell
    echo "deb [ arch=amd64 ] http://repo.mongodb.org/apt/ubuntu precise/mongodb-org/3.4 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.4.list
```

14.04系统下

```shell
    echo "deb [ arch=amd64 ] http://repo.mongodb.org/apt/ubuntu trusty/mongodb-org/3.4 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.4.list
```

16.04系统下

```shell
    echo "deb [ arch=amd64,arm64 ] http://repo.mongodb.org/apt/ubuntu xenial/mongodb-org/3.4 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.4.list
```

3. 更新本地包的数据

```shell
    sudo apt-get update
```

4. 最后执行命令进行安装

```shell
    sudo apt-get install -y mongodb-org
```

5. 启动mongod服务

```shell
   sudo service mongod start
```

### Redis的安装

1. 下载解压文件
```shell
    wget http://download.redis.io/redis-stable.tar.gz
    tar xvzf redis-stable.tar.gz
    cd redis-stable
    make
```

2. 将运行文件安装到 /usr/bin
```shell
make install
```

3. 创建配置文件夹和数据文件夹
```shell
    sudo mkdir /etc/redis
    sudo mkdir /var/redis
```

4. 将编译目录下的脚本拷贝到init.d文件夹下
```shell
    sudo cp utils/redis_init_script /etc/init.d/redis_6379
```

5. 拷贝配置文件
```shell
    sudo cp redis.conf /etc/redis/6379.conf
```

6. 为redis创建一个数据和工作目录
```shell
    sudo mkdir /var/redis/6379
```

7. 编辑/etc/redis/6379.conf
    * 把参数 daemonize 设置为 yes (默认是 no).
    * 设置 pidfile 为 /var/run/redis_6379.pid (可以根据需要改变端口).
    * 如果有需要可以改变 port 参数. 默认6379.
    * 设置 loglevel 参数为合适值.
    * 设置 logfile 为 /var/log/redis_6379.log
    * 设置 dir 为 /var/redis/6379 (此步骤很重要!)

8. 执行命令：
```shell
    sudo update-rc.d redis_6379 defaults
```

9. 启动程序
```shell
    sudo /etc/init.d/redis_6379 start
```
