---
title: centos安装php7.1
date: 2019-04-15 00:09:23
tags:
- php
---

1，更改yum源：

```
rpm -Uvh https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
rpm -Uvh https://mirror.webtatic.com/yum/el7/webtatic-release.rpm
```

2，yum查询安装php71w

```
yum search php71w
```

3，yum 安装php71w和各种拓展，选自己需要的即可

```
yum install php71w php71w-cli php71w-common php71w-devel php71w-embedded php71w-fpm php71w-gd php71w-mbstring php71w-mysqlnd php71w-opcache php71w-pdo php71w-xml php71w-pecl-redis
```

4，安装完成之后，#whereis php 可以看到php的安装目录，

```
whereis php
```

5，查看php及php-fpm版本

```
php -v
php-fpm -v
```

