---
title: CONTIKI应用之static和extern的使用
tags: CONTIKI,static和extern
grammar_cjkRuby: true
---


在Contiki进程中如果不用static声明变量，变量的值会在程序切换或退出时丢失。所以在编写Contiki用户程序时，如果需要变量的值一直保持，就必须在声明变量时用static。

但使用static后，声明的变量或函数只能在该文档中使用。如果你的变量需要在整个工程中使用，就不能用static，而是定义一个全局变量，在使用时再用extern声明。