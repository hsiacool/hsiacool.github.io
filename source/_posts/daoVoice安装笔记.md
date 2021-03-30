---
title: daoVoice安装笔记
date: 2020-10-30 13:40:23
tags: daoVoice
categories: 教程与记录
---
daoVoice是一款客服沟通运营平台，给公司官网加客服，接触了一下daoVoice，操作简单方便，注册用户 5000 位以内免费。

参考资料：
Api：[daoVoice's api](http://docs.daovoice.io/api/)
官方指导文档：[daoVoice 官方指导文档](http://guide.daocloud.io/dcs)

接入：
一、注册一个新账号 [daoVoice注册新账号](http://dashboard.daovoice.io/get-started)

![](https://img-blog.csdnimg.cn/20210207160357657.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3Nvbmdoc2lh,size_16,color_FFFFFF,t_70)
二、安装并接入 [安装手册](http://guide.daocloud.io/daovoice/%E5%BF%AB%E9%80%9F%E5%AE%89%E8%A3%85-5871096.html)

![快速接入](https://img-blog.csdnimg.cn/20210207160411859.png)
将生成的代码写在所要添加daovoice页面的</head>标签之前，马赛克处是不同开发者项目的appId（页面自动生成）
三、调用下面的daovoice代码进行初始化，对客户的不同登录状态进行不同回复的设置

ejs写法：
![ejs写法](https://img-blog.csdnimg.cn/2021020716044083.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3Nvbmdoc2lh,size_16,color_FFFFFF,t_70)

判断用户是否登陆，登陆就初始化项目的appId，同时存入用户的Id、email和mobile，未登录就只初始化项目的appId
其中app_id和user_id为必填项，email便于与用户沟通
四、开启项目，连接成功

使用：
1.客服人员进入后台即可与客户进行即时沟通
2.对于未登录游客会自动回复，同时页面上出现一个请客户留下联系方式的弹框，不会流失任何一个有需求的客户。

整个操作简单方便不耗时，非常适合产品类网站建设。
