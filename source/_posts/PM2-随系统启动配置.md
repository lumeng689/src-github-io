---
title: PM2 随系统启动配置
date: 2017-09-06 18:09:16
tags: PM2
---

1. 自动配置启动脚本
```
  pm2 startup 
```

2. 保存当前的进程信息（已启动的服务）
```
  pm2 save
```

3. 手动的测试下保存是否有效
```
  pm2 resurrect
```

4. 如果要取消，启动
```
  pm2 unstartup
```