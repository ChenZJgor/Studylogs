---
title: CONTIKI应用之IO口应用 
tags: CONTIKI,I/O口
grammar_cjkRuby: true
---

在开发CONTIKI应用时，遇到的有关IO口的问题和得出的经验都记录在下文，以便以后总结。

CONTIKI系统CC2530平台下的IO口驱动有一个BUG，该BUG在port.h文件中

    #define PORT_CLEAR(port,pin)         PORT_CLEAR_X(port,pin) PORT_CLEAR_X(port,pin)
    #define PORT_TOGGLE(port,pin)        PORT_TOGGLE_X(port,pin) PORT_TOGGLE_X(port,pin)
PORT_CLEAR和PORT_TOGGLE的宏定义错误。