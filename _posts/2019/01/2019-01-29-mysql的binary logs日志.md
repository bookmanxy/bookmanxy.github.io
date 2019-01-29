---
layout: post
title:  "mysql的binary logs日志"
categories: 数据库
tags:  mysql
author: watermelon
---
* content
{:toc}

![binary logs日志](https://images.gitee.com/uploads/images/2019/0129/164404_2b65e52e_1210188.jpeg)
## 前言
数据库一般都会有日志、快照等设计，接触过的oracle就有flashback，mysql也有个binary logs






### **0：binary log是什么**  
与大多数关系型数据库，日志文件是MySQL数据库的一个重要组成部分。MySQL有几种不同的日志文件，通常包括错误日志文件，二进制日志，通用日志,慢查询日志，等等。  
这些日志能够帮助我们定位mysqld内部发生的事件，数据库性能故障。记录数据的变更历史，用户恢复数据库等等。  

Binary log 用来记录数据库中发生的修改情况，比如数据的修改、表格的创建及修改等，它既可以记录涉及修改的SQL，也可以记录数据修改的行变化记录，同时也记录了执行时间。  
比如，执行sql：update tabname set cola='a' where id between 1 and 5，修改了5行记录。  
当开启binlog记录的时候，根据设置的binlog格式，可能记录的是这一条SQL语句，也可能记录的是5行数据记录的修改情况，也可能两者都有。  
  
跟general log区分下，binnary log是记录数据库内部的修改情况，而general log是记录所有数据库的SQL操作情况，比如像select或者show这种语句，不会发生数据修改，则不会记录到binnary log，但是属于数据库操作记录，会记录到general log。  

### **1：binary log日志开启和关闭**
在实践truncate 清空表的数据  并要恢复时遇到了个“You are not using binary logging”的问题。
有可能是未打开日志模式。执行语句
```sql
//查询
show variables like 'log_bin'
```
![showvariables](https://images.gitee.com/uploads/images/2019/0129/165106_672bbd72_1210188.jpeg)
果然，没有打开，那接下来问题的焦点就是如何打开和关闭了。  

##### **1：打开日志**
* 1：找到数据库安装目录（或者通过环境变量找），目录下找到“my.ini”文件，如果没有的话那一定是有“my-default.ini”文件的，复制（或直接修改）名为 my.ini 的文件即可。  
* 2：记事本打开，修改配置
```text
[mysqld]
...
log_bin = mysql_bin
```

* 3：重启下mysql
```text
如果不知道咋重启，可以试试这个办法
1： win + R键命令行小窗口，输入：services.msc
2：服务列表中找到mysql，点击重启即可
```
* 4:再查一次： show variables like 'log_bin'  这时候已经打开了。
![on](https://images.gitee.com/uploads/images/2019/0129/170430_cb8c12e6_1210188.jpeg)


##### **2：关闭日志**
* 1：加# 注释掉log_bin = mysql_bin
* 2：重启mysql即可（如果能不重启mysql，做到动态关闭那是最好的，有方案的话直接投稿微信公众号：海码充电站 联系我哦~）

### **2：如何清理及自动清理**
 [关于binary log那些事](https://blog.csdn.net/m48o8gewuc/article/details/72888092)  
 [MySql自动清除binary logs日志](https://blog.csdn.net/hanchao5272/article/details/79227325)  
