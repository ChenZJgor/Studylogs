---
title: CONTIKI应用之传感器驱动编写
tags: CONTIKI,传感器驱动
grammar_cjkRuby: true
---


在用CONTIKI系统做开发时，免不了编写各种传感器的驱动。现把开发时遇到的问题和得出的经验记录下来，以便以后总结。

CONTIKI系统的传感器驱动都封装在sensor这个结构体内

    struct sensors_sensor {
        char *       type; //传感器名称
        int          (* value)     (int type); //指向读取传感器数据函数的指针
        int          (* configure) (int type, int value); //指向传感器配置函数的指针
        int          (* status)    (int type); //指向读取传感器状态函数的指针
    };

在编写完传感器的驱动程序后，必须通过宏定义声明各个函数

    SENSORS_SENSOR(button_1_sensor, BUTTON_SENSOR, value_b1, configure_b1, status_b1);
    
并且在"smartrf-sensors.c"的结构体中

    const struct sensors_sensor *sensors[] = {
    #if ADC_SENSOR_ON
    &adc_sensor,
    #endif
    #if BUTTON_SENSOR_ON
    &button_1_sensor,
    #if MODELS_CONF_CC2531_USB_STICK
    &button_2_sensor,
    #endif
    #endif
    0
    };
添加你所编写的驱动的名称。



系统会在"sensors.c"中，搜索*sensors[]数组中的值

    for(i = 0; sensors[i] != NULL; ++i) {
        sensors_flags[i] = 0;
        sensors[i]->configure(SENSORS_HW_INIT, 0);
    }
用"sensors_changed"函数标记传感器事件的发生，并传递给用户程序。

用"sensors_find"函数查找传感器驱动

    sensor =(struct sensors_sensor *) sensors_find(ADC_SENSOR);