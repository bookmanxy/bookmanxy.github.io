---
layout: post
title:  "写个windows的脚本bat"
categories: 计算机
tags:  windows 脚本
author: watermelon
---
* content
{:toc}

![bat](https://images.gitee.com/uploads/images/2019/0214/153002_02fa6fa0_1210188.jpeg)
## 前言
生成了可运行jar包，每次手动cmd命令行java -jar jar包地址感觉麻烦，看看windows有没有脚本，点点就能打开运行的。




### **一：思路**
我只要让脚本做到跟我手动输命令一样的效果就行了。

* 1、新建一个txt
* 2、输入内容（其实就是那段在命令行窗口输入的内容）
* 3、文件重命名：blog.bat

文件内容：
```xml
java -jar C:\Users\Administrator.DESKTOP-0CRK6JE\Desktop\blogs\blog.jar
```

搞定！！
