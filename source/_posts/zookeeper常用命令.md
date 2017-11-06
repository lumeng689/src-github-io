---
title: zookeeper常用命令
date: 2017-11-03 18:09:16
tags: zookeeper
---

zookeeper 安装目录下有 zkCli工具（windows下 zkCli.cmd, linux 下 zkCli.sh）
```
   ./zkCli.sh  # 连接本地 zookeeper
   ./zkCli.sh -server 10.1.1.3:2181 # 连接远程zookeeper
```

以下命令均是在zkCli下输入。

1. ls
查看节点
```bash
  ls /
```
输出：
```bash
  [zookeeper, hhh, xyz]
```

2. ls2
查看节点详细数据
```bash
  ls2 /
```
输出：
```
[hhh, a, b, zookeeper, dubbo]
cZxid = 0x0
ctime = Thu Jan 01 08:00:00 CST 1970
mZxid = 0x0
mtime = Thu Jan 01 08:00:00 CST 1970
pZxid = 0x1c0
cversion = 9
dataVersion = 0
aclVersion = 0
ephemeralOwner = 0x0
dataLength = 0
numChildren = 5
```

节点信息介绍
```
cZxid：节点创建时的zxid
ctime：节点创建时间
mZxid： 节点最新一次更新发生时的zxid
mtime： 节点最新一次更新发生时间
pZxid： 0x198
cversion： 其子节点的更新次数
dataVersion： 节点数据的更新次数
aclVersion： 节点ACL(授权信息)的更新次数
ephemeralOwner： 如果该节点为ephemeral节点, ephemeralOwner值表示与该节点绑定的session id. 如果该节点不是ephemeral节点, ephemeralOwner值为0
dataLength： 节点数据的字节数
numChildren： 子节点个数
```

3. create 
创建节点， 其中-e 代表临时节点 -s代表持久节点 默认是-s。
```
  create -e /node data # 创建临时节点
  create -s /node data
```

4. get
获取节点数据
```
  get /node
```

5. set
更新节点数据
```
  set /node data
```

6. delete
删除节点 （子节点为空时会删除失败）
```
  delete /node
```

7. rmr
删除节点 （存在子节点仍能删除成功）
```
  rmr /node
```

8. stat
获取节点信息
```
  stat /node
```

9. sync
```
  delete /hari
  rmr /hari
```

10. getAcl
获取权限数据
```
  getAcl /dubbo
```
输出：
```
'world,'anyone
: cdrwa
```
简单说ACL 和UGO（User，Group，Other）一样，都是权限控制的方式，acl字段分为 scheme:id:permission
上面的权限模式是'world,'，授权对象ID是anyone，权限是cdrwa（create, delete, read, write, admin）

11. setAcl
```
  setAcl /node world:anyone:crdwa
  setAcl /newnode ip:127.0.0.1:crdwa
  
  addauth digest user_abc:pwd_abc # 先添加auth信息
  setAcl /newnode digest:user_abc:pwd_abc:crdwa
```

12. setquota
setquota ：设置子节点的个数（-n：子节点个数的限制，-b：数据数据节点数据长度的限制）
```
  setquota -n 3 /node
```

13. delquota
删除数据节点配额的情况
```
  delquota /node
```

14. listquota
查看数据节点配额的情况
```
  listquota /node
```

15. sync
```
  sync /aa
```
