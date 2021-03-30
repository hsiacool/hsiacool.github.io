---
title: git命令大全
date: 2020-11-13 13:13:01
tags: git
categories: 理解与总结
---
今天事情不多，对git 做一个总结，都是比较常规的用法，日常操作应该是够了
![](https://img-blog.csdnimg.cn/20190426154538504.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3Nvbmdoc2lh,size_16,color_FFFFFF,t_70)

### 一、常用命令
查看当前所有分支 git branch --all
创建dev分支，然后切换到dev分支：
```
git checkout -b dev
```
其中git checkout命令加上-b参数表示创建并切换，相当于以下两条命令：
```
git branch dev
git checkout dev   //只切换分支
```
用git branch命令查看当前所有分支：
```
git branch --all
```
查看当前状态：
```
git status
```

### 二、合并别人的远程分支
前提：保证两个分支暂存区无内容
```
git checkout hsia   //切换到hsia分支
git pull   //拉取代码
git merge origin/hf
```

### 三、新建分支并关联到远程
```
git checkout -b dev
git push --set-upstream origin dev
```

### 四、远程分支拉到本地
```
git pull origin dev
```

### 五、在A分支修改的内容需要提交到B分支，且A分支不做同步
（1）通过git stash将工作区恢复到上次提交的内容，同时备份本地所做的修改
```
git stash
```
（2）然后切换至B分支
```
git checkout B
```
（3）从git栈中获取到最近一次stash进去的内容，恢复工作区的内容，获取之后，会删除栈中对应的stash
```
git stash pop
```
（4）进行正常的提交代码步骤即可

### 六、已有仓库连接至远程git
在本地初始化git仓库
```
git init
```
新增远程仓库上游
```
git remote add origin 仓库地址
```
将项目中的所有文件与文件夹增加到本地库
```
git add .
```
提交
```
git commit -m 描述
```
上传至远程仓库
```
git push --set-upstream origin master
```
完成，至此项目已推送至远程，并且本地与远程仓库建立了连接。

### 七、使用https方式克隆远程https库时，出现了每次进行git操作都要验证账号密码的情况
原因是在添加远程库的时候使用了https的方式，所以每次都要用https的方式操作远程库
解决方案：
```
# 查看使用的传输协议:
git remote -v
```
origin https://github.com/XXXX/XXXX.git (fetch)
origin https://github.com/XXXX/XXXX.git (push)
此时可以确定是https传输
重新设置成ssh的方式:
```
git remote rm origin
git remote add origin ssh地址
git push -u origin 分支名
```
设置好了之后再看当前传输协议：
origin git@github.com:XXXX/XXXX.git (fetch)
origin git@github.com:XXXX/XXXX.git (push)
已经变成ssh方式



同时推荐一下使用的脑图软件：MindMaster ，非常好用
