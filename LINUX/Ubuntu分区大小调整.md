---
title: Ubuntu分区大小调整
tags: Ubuntu,分区
grammar_cjkRuby: true
---

如果要调整系统分区，就要用到光盘版的GParted-LiveCD。

可能存在的问题：
可能会发生swap分区丢失的情况，可在终端中用“free -m”命令查看swap分区是否激活(是否显示容量)，如果未激活，可用“sudo mkswap /dev/sdaX”命令(X为swap分区的编号)进行激活，并将激活所得的UUID码替换掉“/etc/fstab”文件(需要管理员权限)中原来 swap分区的UUID编码，重启后即可自动激活挂载。

警告：对swap分区的激活操作及对fstab文件的修改应谨慎，必需仔细核对修改的值。

[参考网站1][1]
[参看网站2][2]


  [1]: http://www.linuxidc.com/Linux/2013-06/85747.htm
  [2]: http://www.linuxidc.com/Linux/2015-03/115027.htm