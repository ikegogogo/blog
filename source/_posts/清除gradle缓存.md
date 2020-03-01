---
title: 清除gradle缓存
date: 2019-09-30 13:17:08
cover: https://tva1.sinaimg.cn/large/00831rSTgy1gcewj4vv9sj30rs0ijgmf.jpg
tags:
- gradle
- java
---

#### 一，背景

gradle java项目引用jar包后，jar包更新经常没发即使拉取到最新的jar包

#### 二，解决办法

执行命令：

```
gradle clean build --refresh-dependencies
```

如果还不行，删除gradle文件夹缓存

```
cd .gradle/caches/modules-2/files-2.1/

rm 相应jar
```

