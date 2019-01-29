---
layout: post
title:  "mysql的general logs日志"
categories: 数据库
tags:  mysql
author: watermelon
---
* content
{:toc}

![general logs日志](https://images.gitee.com/uploads/images/2019/0129/191948_3f6fe9bd_1210188.jpeg)
## 前言
有时候需要查查看mysql的sql啥时候执行






### **1：为什么**
总觉得能够查到sql执行记录，及响应时间，慢查询等等会更有安全感，可能是信息同步到会更靠谱点吧。  
工作中经常遇到这样的问题：mysql数据访问能量很大，想要从sql方面优化。研发经常会问到能看到哪些SQL执行比较频繁吗？  
回道：不能哦，只能看到当前正在运行的SQL和慢日志里记录的SQL。  
因为为了性能考虑，一般general log不会开启。  
slow log可以定位一些有性能问题的sql，而general log会记录所有的SQL。然而有时候生产上的mysql出现性能问题，短时间开启general log，来获取sql执行的情况，对排查和分析mysql的性能问题，还是有很大的帮助的。  
或者是有时候，不清楚程序执行了什么sql语句，但是又要排除错误，找不到原因的情况下，也是可以短暂的开启这个general log日志的。  

### **2：怎么用**
##### 1：永久有效
更改my.cnf配置文件
 [mysql之general_log日志介绍](http://blog.51cto.com/wujianwei/2146109?source=dra)  

##### 2：下次重启前
```xml
set global general_log=on;
```