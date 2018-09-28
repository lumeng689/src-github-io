---
title: bezierEasingMixin被禁用问题的解决
date: 2018-09-28 14:53:41
tags: Angular, LESS
---

在 node_modules\@angular-devkit\build-angular\src\angular-cli-files\models\webpack-configs\styles.js line 136和142行
（由于版本不一样文件的位置也不一样），lessPathOptions这个对象，加入属性lessPathOptions.javascriptEnabled = true。

```
 let lessPathOptions = { paths: [], javascriptEnabled: true};
    if (......);
        lessPathOptions = {
            paths: includePaths,
            javascriptEnabled: true
        };
    }
```
