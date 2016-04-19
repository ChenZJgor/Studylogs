---
title: CONTIKI应用之串口应用 
tags: CONTIKI,串口
grammar_cjkRuby: true
---


在CONTIKI开发时经常用到串口，所以把遇到的问题记录下来，以便以后总结。

 1. CC2530的串口驱动有一个BUG，会导致串口不能接收数据，现已修正。serial-line.c是串口的驱动程序，里面有一个“int”类型的“c”变量用来判断是否收到串口数据，而ringbuf_get()函数是用来轮询串口是否有数据输入的，返回一个“int”类型的数值。“c”变量与ringbuf_get()函数的返回值必须是同类型的，而在原来的程序中两者的类型并不相等，导致数据溢出，不能进入串口数据处理进程。

![CC2530平台串口BUG_1][1]
![CC2530平台串口BUG_2][2]


  [1]: ./images/CC2530%E5%B9%B3%E5%8F%B0%E4%B8%B2%E5%8F%A3BUG_1.jpg "CC2530平台串口BUG_1.jpg"
  [2]: ./images/CC2530%E5%B9%B3%E5%8F%B0%E4%B8%B2%E5%8F%A3BUG_2.jpg "CC2530平台串口BUG_2.jpg"