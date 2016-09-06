---
title: uCOSIII应用之信号量应用
tags: uCOSIII,信号量
---

uCOSIII可以使用信号量，使用方法：

 1. 创建信号量变量

``` stylus
OS_SEM ActiveSem;		//激活信号量
```

 2. 创建信号量（创建前必须进入临界区）

``` stylus
OSSemCreate ((OS_SEM*)	&ActiveSem,				//创建应变片激活状态信号量
			   (CPU_CHAR*) "ActiveSem",
			   (OS_SEM_CTR)0,
			   (OS_ERR*)	&err);
```

 3. 相关指令

![uCOSIII信号量命令][1]


  [1]: ./images/uCOSIII%E4%BF%A1%E5%8F%B7%E9%87%8F%E5%91%BD%E4%BB%A4.jpg "uCOSIII信号量命令.jpg"