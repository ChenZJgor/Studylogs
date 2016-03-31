---
title: OLED(SSD1306驱动芯片)的IIC协议 
tags: SSD1306,IIC
grammar_cjkRuby: true
---


下面是OLED(SSD1306驱动芯片)IIC协议的摘要中文翻译

 1. SCL和SDA都要接上拉电阻
 2. RES接口用于设备初始化
 3. DC接口作为从设备选择位，当R/W为1时是读取模式，R/W为0时是写入模式。 
              ![从设备地址示意图][1]
 4. ACK信号在一个SCL的高电平时输出，0为成功，1为失败
 5. SCL写入的顺序
(1)开始信号
(2)从设备地址
(3)写入控制字节和数据字节。控制字节为CO+D/C+6个0。
如果CO为0，表示接下来的信息之包含数据没有命令。
如果D/C为0，表示写入命令；D/C为1，表示写入数据，数据将储存在GDDRAM中，GDDRAM中的数据指针会自动加1
(4)每一次写入都会有ACK
![enter description here][2]
(5)IIC开始信号为SDA由高到底，结束信号为由低到高，SCL都要为高
![enter description here][3]
 6. List item

  [1]: ./images/%E4%BB%8E%E8%AE%BE%E5%A4%87%E5%9C%B0%E5%9D%80.jpg
  [2]: ./images/IIC%E5%86%99%E5%85%A5.jpg "IIC写入.jpg"
  [3]: ./images/QQ%E6%88%AA%E5%9B%BE20160331172652.jpg