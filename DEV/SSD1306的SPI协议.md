---
title: SSD1306的SPI协议 
tags: SSD1306,SPI
grammar_cjkRuby: true
---


近段时间调试小尺寸的OLED显示屏，虽然是SPI协议，接口上却写着SCL和SDA。所以要注意的是这种集成模块的OLED并不是使用IIC协议，而是SPI协议，而且并不用管CS，接低电平即可。
![OLED外观][1]

SSD1306的SPI协议时序图，因为这个OLED默认就把CS拉低了，所以每次传输可以不用去管CS，但没CS这几个IO就被独占了。从图上可以看到数据是在SCLK上升沿时被传入，高位在前。DC用于表示写入的是数据还是指令，DC为低时是指令写入，DC为高时是数据写入。
128*64的OLED在SSD1306的控制下，被分成8个页，每个页有8行128列，每个列对应一个字节。
![SSD1306SPI四线][2]

[参考网站][3]


  [1]: ./images/OLED.jpg "OLED.jpg"
  [2]: ./images/SSD1306SPI%E5%9B%9B%E7%BA%BF.png "SSD1306SPI四线.png"
  [3]: http://www.eeboard.com/bbs/forum.php?mod=viewthread&tid=22116