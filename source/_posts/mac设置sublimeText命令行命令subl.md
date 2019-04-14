---
title: mac设置sublimeText命令行命令subl
date: 2019-04-14 23:27:27
tags:
- sublime 
- mac
---

#### 环境：

Mac + iterm + zsh

#### 配置方法：

vi ~/.zshrc

文末增加：

```
alias subl='open -a "Sublime Text"'
```

source ~/.zshrc

#### 使用方法：

```
//使用sublime打开当前目录
subl .
//使用sublime在当前目录创建文件
subl test.txt
//打开subl
subl
```

