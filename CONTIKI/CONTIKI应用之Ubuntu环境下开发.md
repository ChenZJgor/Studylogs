---
title: CONTIKI应用之Ubuntu环境下开发
tags: CONTIKI,Ubuntu
grammar_cjkRuby: true
---


CONTIKI系统默认是在Ubuntu下使用SDCC开发的，因为SDCC采用的是GCC编译器，与Windows下的IAR或KEIL还是有很大的不同。

 1. 使用SDCC必须要写好Makefile文件，这样编译器才能在编译时找到相应的文件。
 2. 因为GCC编译器是使用标准C，所以在IAR上能编译成功不代表在SDCC上也能编译成功。例如我在编译时遇到一个问题，提示“变量初始化的值不能为变量”。这是因为标准C规定变量初始化时一定要为常量，如果要用变量赋值，必须要在函数或宏定义中。
 3. 因为CC2530的栈空间不够，所以CONTIKI系统CC2530平台上的UDP-IPV6例程有重启的问题。所以对于CC2530平台，在没有修改UIP协议栈的情况下，不能作为ROOT节点。解决方法是使用sensinode分支的源代码，该分支的版本是CONTIKI2.6，修改了部分文件的代码减少堆栈开销。