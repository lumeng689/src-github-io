---
title: MongoDB的导入导出
date: 2017-09-18 11:34:06
tags: MongoDB
---
MongoDB的导入导出分为 文本导出 和 二进制导出，文本导出一次导出一个集合，方便与其他数据库交换数据， 
二进制导出的是MongoDB自己的格式，可以导出整个数据库，体积小，速度快。

# 文本导出
## mongoexport 导出表
```bash
 -h, --host=<hostname>              主机
    --port=<port>                   端口
 -u, --username=<username>          用户名
 -p, --password=<passwd>            密码
 -d, --db=<database-name>           数据库名称
 -c, --collection=<collection-name> 集合名称
 -f, --fields=<field>[,<field>]*    逗号分隔的字段名称
     --type=<type>                  json或者csv，默认json
 --type=<type>
 -o, --out=<filename>               导出文件名称
```

举例：  导出adminusers集合
```bash
 mongoexport -h localhost -d cloudminds -c adminusers  -o ./adminusers.json
```

## mongoimport 导入数据

```bash
 -h, --host=<hostname>              主机
    --port=<port>                   端口
 -u, --username=<username>          用户名
 -p, --password=<passwd>            密码
 -d, --db=<database-name>           数据库名称
 -c, --collection=<collection-name> 集合名称
 -f, --fields=<field>[,<field>]*    逗号分隔的字段名称
     --type=<type>                  json或者csv，默认json
     --out=<filename>               要导入的文件名称
 --type=<type>
```

举例
```bash
 mongoimport -h localhost -d cloudminds -c adminusers  --file ./adminusers.json
```

# 二进制导出

## mongodump 导出二进制bson结构的数据及其索引信息
```bash
 -h, --host=<hostname>              主机
     --port=<port>                  端口
 -u, --username=<username>          用户名
 -p, --password=<passwd>            密码
 -d, --db=<database-name>           数据库名称
 -c, --collection=<collection-name> 集合名称
     --type=<type>
 -o, --out=<filename>               导出文件名称
```

导出cloudminds数据库中的数据到文件 bak中

```bash
  mongodump -d cloudminds -o bak
```

## mongorestore 导入二进制文件


导入备份文件bak中的数据

```bash
  mongorestore --drop bak
```

