---
title: eclipse环境下如何配置tomcat
date: 2018-08-20 13:35:46
categories:
 - Java Web学习
tags:
 - Java
 - Eclipse
 - Java EE
 - 新技能
description: myeclipse是一个好东西，但是pro只给三十天的免费时间，有点头疼。有听说破解容易翻车，头又在隐隐作痛。老牌的eclipse说实在的 还是挺好用的
photos: "https://i.loli.net/2018/08/20/5b7a605658f8b.jpg"
---


开了虚拟机 弄了下基本的安装 在下还是萌新 解释可能没有太详细

### 配置必备

>JDK
>Eclipse
>Tomcat

#### 安装简介
jdk 一路next 直接默认的没问题
eclipse 选择java_ee 选择路径 ok
Tomcat 无太大操作空间 可以直接一路默认

#### Eclipse安装图解
真的默认 无

#### Eclipse安装图解
![0.8](How-to-configure-Tomcat-in-eclipse-environment/0.8.png)
![0.9](How-to-configure-Tomcat-in-eclipse-environment/0.9.png)

#### Tomcat安装图解
![0.1](How-to-configure-Tomcat-in-eclipse-environment/0.1.png)
![0.2](How-to-configure-Tomcat-in-eclipse-environment/0.2.png)
![0.3](How-to-configure-Tomcat-in-eclipse-environment/0.3.png)
![0.4](How-to-configure-Tomcat-in-eclipse-environment/0.4.png)
![0.5](How-to-configure-Tomcat-in-eclipse-environment/0.5.png)
![0.6](How-to-configure-Tomcat-in-eclipse-environment/0.6.png)
![0.7](How-to-configure-Tomcat-in-eclipse-environment/0.7.png)


### 配置

#### 配置Tomcat

**Window** --> **Preferences** --> **Server** --> **Runtime Environment** --> **Add**

Add你的Tomcat 

选择你的版本
>我的版本是v9.0

![1](How-to-configure-Tomcat-in-eclipse-environment/1.png)
![2](How-to-configure-Tomcat-in-eclipse-environment/2.png)

Next

选择你的安装路径

![3](How-to-configure-Tomcat-in-eclipse-environment/3.png)

#### 选择jdk版本


![4](How-to-configure-Tomcat-in-eclipse-environment/4.png)

一般情况下 这个是系统默认的 这里为了一些后续方便
>Workbench default JRE

Add你的jdk
>我的jdk版本是v9.0.1

选择你的安装路径

![5](How-to-configure-Tomcat-in-eclipse-environment/5.png)

ok 搞定

### 部署
新建项目
**File** --> **New** --> **Other** --> **web** -->**Dynamic Web Project**

![6](How-to-configure-Tomcat-in-eclipse-environment/6.png)

设置项目名

![7](How-to-configure-Tomcat-in-eclipse-environment/7.png)

这里可以不用管
![8](How-to-configure-Tomcat-in-eclipse-environment/8.png)

这个时候我们需要看到我们的server
![9](How-to-configure-Tomcat-in-eclipse-environment/9.png)
![10](How-to-configure-Tomcat-in-eclipse-environment/10.png)


#### 部署server

![11](How-to-configure-Tomcat-in-eclipse-environment/11.png)

将之前创建的Test项目add到 server
![12](How-to-configure-Tomcat-in-eclipse-environment/12.png)
![13](How-to-configure-Tomcat-in-eclipse-environment/13.png)

启动 server
可以右键 也可以直接点击这个绿色启动键
![14](How-to-configure-Tomcat-in-eclipse-environment/14.png)


#### 设置主界面index
**Test** --> **Webcontent (之前自己设置的，这是默认的)** --> `index.jsp`

![15](How-to-configure-Tomcat-in-eclipse-environment/15.png)

```jsp
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN">
<html>
<head>
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
<title>在此处插入标题</title>
</head>
<body>
helloworld
</body>
</html>
```
Ctrl+F11 ok 打开了内置的浏览器 运行成功
或者手动打开浏览器
`http://localhost:8080/Test/`

![16](How-to-configure-Tomcat-in-eclipse-environment/16.png)

#### Others
这里也可以修改path设置成Tomcat的目录 (了解一下)

原
![17](How-to-configure-Tomcat-in-eclipse-environment/17.png)

改
![18](How-to-configure-Tomcat-in-eclipse-environment/18.png)
