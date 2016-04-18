---
title: CONTIKI应用之网络功能应用 
tags: CONTIKI,网络
grammar_cjkRuby: true
---


学校挑战杯项目是关于物联网的，需要用到CONTIKI系统的网络功能。在开发过程中遇到不少问题，所以把问题记录下来，以便以后总结。

 1. 用contiki-wsn2530dk例程里的第9个“RPL-Collect”时“Sink”节点不调用collect_common_set_send_active()函数就不能接受节点的数据。
因为在Contiki2.7中send_active变量初始化为0，需要调用collect_common_set_send_active()给send_active变量赋值为1。而Contiki3.0中send_active变量初始化为1，并不需要再赋值。
 2. `    uip_ipaddr_copy(&server_conn->ripaddr, &clientipaddr);
    uip_udp_packet_send(server_conn, "GET", sizeof("GET"));
    uip_create_unspecified(&server_conn->ripaddr);`
主机给节点发送数据需要用到上面的函数，而用
`          uip_udp_packet_sendto(server_conn, buf, strlen(buf),
                      &clientipaddr, UIP_HTONS(UDP_CLIENT_PORT));`
这个函数却不能把数据发送的节点，原因暂时不明。
