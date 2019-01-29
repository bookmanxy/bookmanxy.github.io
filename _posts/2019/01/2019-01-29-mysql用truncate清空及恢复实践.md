---
layout: post
title:  "mysql用truncate清空及恢复实践"
categories: 数据库
tags:  mysql
author: watermelon
---
* content
{:toc}

![truncate清空及恢复](https://images.gitee.com/uploads/images/2019/0129/160108_c67fda06_1210188.jpeg)
## 前言
验证下truncate清空及恢复实践






### **1：为什么**
网上有说mysql中用了truncate就没办法恢复，我不信，搜了搜大神，果然有相关可恢复的案例，试试看。

### **2：是什么**
思路：
* 1：先创建个库表  
* 2：然后insert into 几条语句  
* 3：使用truncate 清空表的数据  
* 4：再insert into 几条语句，观察下此时的自增主键从1开始  
* 5：恢复到第一次请空前的库表数据

### **3：操作过程**
```sql
//1：先创建个库表  
CREATE TABLE IF NOT EXISTS `tb_user` (
  `user_id` bigint(20) NOT NULL AUTO_INCREMENT,
  `username` varchar(50) NOT NULL COMMENT '用户名',
  `mobile` varchar(20) NOT NULL COMMENT '手机号',
  `password` varchar(64) DEFAULT NULL COMMENT '密码',
  `create_time` datetime DEFAULT NULL COMMENT '创建时间',
  PRIMARY KEY (`user_id`)
) ENGINE=InnoDB AUTO_INCREMENT=2 DEFAULT CHARSET=utf8 COMMENT='用户';
```
![1](https://images.gitee.com/uploads/images/2019/0129/163919_99457253_1210188.jpeg)
![3](https://images.gitee.com/uploads/images/2019/0129/163952_cbd8bdd7_1210188.jpeg)  
  
```sql
//2：然后insert into 几条语句  
INSERT INTO `tb_user` ( `username`, `mobile`, `password`, `create_time`) VALUES
	( '小明', '18700000000', '000', '2017-03-23 22:37:41'),
	( '小华', '18700000000', '000', '2017-03-23 22:37:41'),
	( '小红', '18700000000', '000', '2017-03-23 22:37:41'),
	( '小丽', '18700000000', '000', '2017-03-23 22:37:41');
```
![2](https://images.gitee.com/uploads/images/2019/0129/163935_f99d3316_1210188.jpeg)
  
```sql
* 3：使用truncate 清空表的数据  
truncate tb_user

//此时库表清空
```
![3](https://images.gitee.com/uploads/images/2019/0129/163952_cbd8bdd7_1210188.jpeg)  


```sql
* 4：再insert into 几条语句，观察下此时的自增主键从1开始  
INSERT INTO `tb_user` ( `username`, `mobile`, `password`, `create_time`) VALUES
	( '小明二号', '18700000000二号', '000二号', '2017-03-23 22:37:41'),
	( '小华二号', '18700000000二号', '000二号', '2017-03-23 22:37:41'),
	( '小红二号', '18700000000二号', '000二号', '2017-03-23 22:37:41'),
	( '小丽二号', '18700000000二号', '000二号', '2017-03-23 22:37:41');
```
![4](https://images.gitee.com/uploads/images/2019/0129/164004_b788077d_1210188.jpeg)
  
```sql
* 5：恢复到第一次请空前的库表数据
show binary logs
```
注：如果遇到了“You are not using binary logging”，请移步：   [mysql的binary logs日志](https://www.jb51.net/article/65767.htm)  

引用：    
 [看这里：《MySQL中truncate误操作后的数据恢复案例》](https://www.jb51.net/article/65767.htm)  


