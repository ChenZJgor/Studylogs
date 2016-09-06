---
title: uCOSIII应用
tags: uCOSIII,应用
---

智能坐垫的设计用到了uCOSIII实时操作系统。uCOSIII系统使用说明：

 1. 创建任务块

``` stylus
//任务优先级
#define START_TASK_PRIO		3
//任务堆栈大小	
#define START_STK_SIZE 		512
//任务控制块
OS_TCB StartTaskTCB;
//任务堆栈	
CPU_STK START_TASK_STK[START_STK_SIZE];
//任务函数
void start_task(void *p_arg);
```

 2. 在main函数中初始化系统，创建START任务

``` stylus
OSInit(&err);		//初始化UCOSIII
OS_CRITICAL_ENTER();//进入临界区
//创建开始任务
OSTaskCreate((OS_TCB 	* )&StartTaskTCB,		//任务控制块
			 (CPU_CHAR	* )"start task", 		//任务名字
			 (OS_TASK_PTR )start_task, 			//任务函数
			 (void		* )0,					//传递给任务函数的参数
			 (OS_PRIO	  )START_TASK_PRIO,     //任务优先级
			 (CPU_STK   * )&START_TASK_STK[0],	//任务堆栈基地址
			 (CPU_STK_SIZE)START_STK_SIZE/10,	//任务堆栈深度限位
			 (CPU_STK_SIZE)START_STK_SIZE,		//任务堆栈大小
			 (OS_MSG_QTY  )0,					//任务内部消息队列能够接收的最大消息数目,为0时禁止接收消息
			 (OS_TICK	  )0,					//当使能时间片轮转时的时间片长度，为0时为默认长度，
			 (void   	* )0,					//用户补充的存储区
			 (OS_OPT      )OS_OPT_TASK_STK_CHK|OS_OPT_TASK_STK_CLR, //任务选项
			 (OS_ERR 	* )&err);				//存放该函数错误时的返回值
OS_CRITICAL_EXIT();	//退出临界区	 
OSStart(&err);  //开启UCOSIII
```

3. 在START任务中进行系统设置
(1)统计任务、中断关闭时间测量、时间片轮转功能使能
``` stylus
#if OS_CFG_STAT_TASK_EN > 0u
   OSStatTaskCPUUsageInit(&err);  	//统计任务                
#endif
	
#ifdef CPU_CFG_INT_DIS_MEAS_EN		//如果使能了测量中断关闭时间
    CPU_IntDisMeasMaxCurReset();	
#endif
	
#if	OS_CFG_SCHED_ROUND_ROBIN_EN  //当使用时间片轮转的时候
	 //使能时间片轮转调度功能,时间片长度为1个系统时钟节拍，既1*5=5ms
	OSSchedRoundRobinCfg(DEF_ENABLED,1,&err);  
#endif		
```
(2)创建定时器(如果有使用)

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
(3)创建信号量和各任务(如果有使用)
**注意：创建之前必须进入临界区**`	OS_CRITICAL_ENTER();	//进入临界区`

``` stylus
OSSemCreate ((OS_SEM*)	&ActiveSem,				//创建应变片激活状态信号量
			   (CPU_CHAR*) "ActiveSem",
			   (OS_SEM_CTR)0,
			   (OS_ERR*)	&err);

```


----------


``` stylus
//创建系统核心任务
OSTaskCreate((OS_TCB 	* )&CORETaskTCB,		
			 (CPU_CHAR	* )"core task", 		
			 (OS_TASK_PTR )core_task, 			
			 (void		* )0,					
			 (OS_PRIO	  )CORE_TASK_PRIO,     
			 (CPU_STK   * )&CORE_TASK_STK[0],	
			 (CPU_STK_SIZE)CORE_STK_SIZE/10,	
			 (CPU_STK_SIZE)CORE_STK_SIZE,		
			 (OS_MSG_QTY  )0,					
			 (OS_TICK	  )0,					
			 (void   	* )0,					
			 (OS_OPT      )OS_OPT_TASK_STK_CHK|OS_OPT_TASK_STK_CLR,
			 (OS_ERR 	* )&err);
```

(4)挂起任务和退出临界区

``` stylus
OS_TaskSuspend((OS_TCB*)&StartTaskTCB,&err);		//挂起开始任务			 
OS_CRITICAL_EXIT();	//退出临界区								 

```

 4. 各任务函数编写

每一个任务必须是死循环，在死循环中加入一个可以挂起任务的函数，以实现任务调度

``` stylus
void active_task(void *p_arg)
{
	OS_ERR err;
	p_arg = p_arg;
	
	while(1){
	
	......

		OSTimeDlyHMSM(0,0,1,0,OS_OPT_TIME_HMSM_STRICT,&err); //延时1s
	}
}
```


----------


## 注意

 - 最后一个参数都是错误反馈

