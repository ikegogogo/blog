---
title: mac下idea卡顿问题解决
date: 2019-09-30 13:10:07
tags:
- idea
---

idea在加载相对来说比较大的系统时，经常性出现卡顿，就是直接卡死，写起代码特别难受



解决步骤：

1. 修改custom vm options：help=====>Edit custom vm options...
2. 或同时修改/Applications/IntelliJ IDEA.app/Contents/bin/idea.vmoptions

修改后的配置如：

```
-Xms2048m
-Xmx4096m
-XX:ReservedCodeCacheSize=750m
-XX:+UseCompressedOops
-Dfile.encoding=UTF-8
-XX:+UseConcMarkSweepGC
-XX:SoftRefLRUPolicyMSPerMB=50
-ea
-XX:CICompilerCount=2
-Dsun.io.useCanonPrefixCache=false
-Djava.net.preferIPv4Stack=true
-Djdk.http.auth.tunneling.disabledSchemes=""
-XX:+HeapDumpOnOutOfMemoryError
-XX:-OmitStackTraceInFastThrow
-Djdk.attach.allowAttachSelf
-Dkotlinx.coroutines.debug=off
-Djdk.module.illegalAccess.silent=true
-Xverify:none

-XX:ErrorFile=$USER_HOME/java_error_in_idea_%p.log
-XX:HeapDumpPath=$USER_HOME/java_error_in_idea.hprof
```

-Xms最小内存  -Xmx最大内存 。个人电脑为16G，

设置完重启idea即可