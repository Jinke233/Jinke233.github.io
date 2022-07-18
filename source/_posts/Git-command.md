---
title: Git command
date: 2020-09-24 22:21:12
tags: Git 
---

###  推送已有目录到Git远程仓库

##### 1.初始化仓库

git init

##### 2. 和远程仓库建立链接

两种方式

```bash
git remote add origin git@github.com:Username/Projectname.git
或者是 
git remote add origin 项目的网络地址
```

##### 3. 推送文件到远程目录

```bash
git push origin master -f
```

