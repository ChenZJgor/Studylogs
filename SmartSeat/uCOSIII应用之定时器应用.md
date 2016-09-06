---
title: uCOSIII应用之定时器应用
tags: uCOSIII,定时器
---

uCOSIII系统的定时器可以实现定时（精度不高）。使用方法：

 1. 创建定时器变量和声明回调函数

``` stylus
OS_TMR 	tmr_active;		//激活定时器
void tmr_active_callback(void *p_tmr, void *p_arg); 	//激活定时器回调函数

```

 2. 创建定时器

``` stylus
	//创建应变片激活定时器
OSTmrCreate((OS_TMR		*)&tmr_active,		//激活定时器
			(CPU_CHAR	*)"tmr active",		//定时器名字
			(OS_TICK	 )0,			//0
			(OS_TICK	 )100,          //100*10=1000ms
			(OS_OPT		 )OS_OPT_TMR_PERIODIC, //周期模式
			(OS_TMR_CALLBACK_PTR)tmr_active_callback,//激活定时器回调函数
			(void	    *)0,			//参数为0
			(OS_ERR	    *)&err);		//返回的错误码
```

 3. 编写回调函数

``` stylus
//激活定时器的回调函数
void tmr_active_callback(void *p_tmr, void *p_arg)
{
    ......
}
```

 4. 启动、关闭定时器

``` stylus
(1)OSTmrStart(&tmr_active, &err); //启动定时器
(2)OSTmrStop (&tmr_negative,OS_OPT_TMR_NONE,0,&err); //关闭定时器
```


