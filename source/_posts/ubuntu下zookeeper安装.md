---
title: ubuntu下zookeeper安装
date: 2017-11-03 18:09:16
tags: zookeeper
---

1.下载zookeeper, 并解压
```bash
  cd /opt
  wget http://mirror.bit.edu.cn/apache/zookeeper/stable/zookeeper-3.4.10.tar.gz
  tar -xvf zookeeper-3.4.10.tar.gz
```

2.创建数据文件
```bash
  mkdir -p /data/zookeeper
```

3.创建配置文件
```bash
   cd ./conf
   mv zoo_sample.cfg  zoo.cfg
```

4.设置数据文件目录, 更改zoo.cfg中配置：dataDir=/data/zookeeper 

5.启动服务
```
   cd ./bin
   ./zkServer.sh start
```
