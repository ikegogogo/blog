---
title: 查看Java的汇编指令
date: 2020-07-31 01:23:03
tags:
- java
---

通过javap 命令，可以将字节码文件反编译。如通过下面的命令：

javap -c Xxxx.class

而有时候想看某些JDK底层实现，发现反编译得到的代码并没有什么帮助，因此本文介绍如何查看Java的汇编指令，查看Java代码最真实的运行细节。

Java本身提供这个支持，但需要引入而外的包（hsdis-amd64.dylib）。

Mac下：

https://github.com/evolvedmicrobe/benchmarks/blob/master/hsdis-amd64.dylib

下载下来后，将其放置到jre lib目录下即可。

查看Java的汇编指令

1、可以使用命令

java -XX:+UnlockDiagnosticVMOptions -XX:+PrintAssembly Main (Main是class文件)

2、在IDEA配置VM options，打印汇编指令，如下图。

-XX:+UnlockDiagnosticVMOptions -XX:+PrintAssembly

这种方式，在运行程序时，直接在控制台打印汇编指令。

如果遇到：

Java HotSpot(TM) 64-Bit Server VM warning: PrintAssembly is enabled; turning on DebugNonSafepoints to gain additional output 

Could not load hsdis-amd64.dylib; library not loadable; PrintAssembly is disabled

下载上面的库文件放到jre/lib下即可。