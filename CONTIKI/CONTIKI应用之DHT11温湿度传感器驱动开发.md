---
title: CONTIKI应用之温湿度传感器DHT11驱动开发 
tags: CONTIKI,驱动
grammar_cjkRuby: true
---


参加学校的挑战杯比赛，我们小组的项目是基于CONTIKI系统的，使用CC2530平台，所以需要为传感器开发底层驱动。

DHT11是一款单总线数据格式的温湿度传感器，数据的输入和输出公用一个端口，对时序的要求比较高。

在开发过程中我遇到了一下几个问题:

 1. 关闭CONTIKI的看门狗才能在程序中调用单片机的IO口。原因可能是打开看门狗后不能用IAR的单步调试。（暂解决）
 2. 用示波器捕捉波形发现，主机发送开始信号后，DHT11没有进入采集模式，无数据输出。原因是驱动时序出错，当DHT11输出“1”时，没有先等DHT11拉低就进入了下一位的读取，导致整个时序出错。（已解决）
 ![DHT11输出“1”][1]

### **在做Contiki开发遇到问题的时候，不要去怀疑系统任务调度或系统时钟，一般这方面出错的几率很小。应该关注时序或I/O口设置，这方面出错的可能性很大。**

 
 
 


  [1]: ./images/DHT11%E8%BE%93%E5%87%BA%E2%80%9C1%E2%80%9D.jpg "DHT11输出“1”.jpg"