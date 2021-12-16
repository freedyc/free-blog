---
title: 你应该知道的英文
date: 2021-12-04 22:55:53 
tags: style
comments: true
---


# 解决var不支持IE问题

第1思路使用postcss解决，由于项目是create-react-appc创建的，条件是在不在弹出create-react-app配置请下支持

## 选择需要的库
@rescripts/cli postcss-preset-env rescript-use-postcss-config

## .rescriptrc文件
```
modules.exports = [['use-postcss-config']];
```
## .postcssrc.js
```
module.exports = {
  map: false,
  plugins: {
    'postcss-preset-env': {
      stage: 0,
      browserslist: [
        "last 2 chrome version",
        "last 2 firefox version",
        "last 2 safari version",
        "IE 11",
      ]
    }
  }
}
```
以上操作大功告成
结果试了一下代码中的变量依然么有被替换掉

解决办法：
最后变量写到:root中
```
:root {
    --primary-color: #fof
}
```
这样试了一下完成，适配IE妥妥的