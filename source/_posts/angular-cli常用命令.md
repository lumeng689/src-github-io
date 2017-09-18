---
title: angular-cli常用命令
date: 2017-09-18 14:14:49
tags: Angular 
---

NG常用命令
======

# ng help

打印帮助信息

```
    ng help
```

# ng new

创建新项目

```
    ng new PROJECT_NAME
    ng new sassy-project --style=sass #使用sass框架
```


# ng serve

启动服务

```
    ng serve #简单情况
    ng serve --host 0.0.0.0 --port 4201 --live-reload-port 49153 # 指定端口
```

# ng generate

简写 ng g ，用来生成angular2的组件，服务，接口等内容


|    名称    |    命令 |
| ------    | ------ | 
| Component | ng g component my-new-component |
| Directive | ng g directive my-new-directive |
| Pipe      | ng g pipe my-new-pipe |
| Service   | ng g service my-new-service |
| Class     | ng g class my-new-class |
| Interface | ng g interface my-new-interface |
| Enum      | ng g enum my-new-enum |
| Module    | ng g module my-module |

```
    ng g component my-new-component 
    ng g directive my-new-directive
    ng g pipe my-new-pipe
    ng g service my-new-service
    ng g class my-new-class
    ng g interface my-new-interface
    ng g enum my-new-enum
    ng g module my-module
```

创建路由：
  
```
    ng new PROJECT_NAME --routing     # 创建项目时就创建一个app-routing.module.ts文件
    ng g module my-module --routing  # 创建模块时创建一个my-module-routing.module.ts文件
```

# ng build

构建项目 配置文件是angular-cli.json的文件

```
    # 以下语句等价
    ng build --target=production --environment=prod
    ng build --prod --env=prod
    ng build --prod
    # 以下语句等价
    ng build --target=development --environment=dev
    ng build --dev --e=dev
    ng build --dev
    ng build
```


