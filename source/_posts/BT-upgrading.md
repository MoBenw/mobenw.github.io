---
title: 宝塔专业版破解方案
date: 2018-09-26 20:26:53
categories: 安装新东西
tags:
 - 安装与配置
description: 或许你的宝塔需要这些操作
photos: https://i.loli.net/2018/11/27/5bfd4a846b299.png
---

本方法用水大佬提供，献上水大佬的网站 [https://www.gksec.com/](https://www.gksec.com/
)

### 破解思路
 1. 安装宝塔
 2. 将宝塔升级至专业版
 3. 修改配置文件!



### 安装方法
使用 SSH 连接工具，如宝塔远程桌面助手连接到您的 Linux 服务器后，根据系统执行相应命令开始安装（大约2分钟完成面板安装）： 
>Centos安装脚本 `yum install -y wget && wget -O install.sh http://download.bt.cn/install/install_pro.sh && sh install.sh`
>Ubuntu/Deepin安装脚本 `wget -O install.sh http://download.bt.cn/install/install-ubuntu_pro.sh && sudo bash install.sh`
>Debian安装脚本 `wget -O install.sh http://download.bt.cn/install/install-ubuntu_pro.sh && bash install.sh`
>Fedora安装脚本 `wget -O install.sh http://download.bt.cn/install/install_pro.sh && bash install.sh`

### 升级方法
>使用 SSH 连接工具，如宝塔远程桌面助手连接到您的 Linux 服务器后，执行以下命令，升级专业版不会对网站环境有任何影响。 
>免费版升级专业版脚本 `wget -O update.sh http://download.bt.cn/install/update_pro.sh && bash update.sh pro`

### 修改配置

**明确目标**

进入该目录下
`/www/server/panel/class/` 
修改这三个文件
> `commmon.py`
> `panelAuth.py`
> `panelPlugin.py`


首先你需要一个神器

**[MobaXterm_Personal_10.2.exe](https://www.lanzous.com/i1ytvvg)**

使用神器 ssh 登入你的服务器
![1.png](https://i.loli.net/2018/11/27/5bfd58e09054e.png)

登入后你就会发现 这个软件居然有目录
![2.png](https://i.loli.net/2018/11/27/5bfd58edd81a1.png)

进行下一步之前，我们需要将我们的宝塔升级至专业版

升级到专业版后 你会发现你进入宝塔需要支付才能进入

这里不要慌 我们继续看我们的神器

将我们的文件目录调至`/www/server/panel/class/`

然后找到我们的需要修改的第一个文件`commmon.py`拖到桌面上来 源目录下的这两个文件`commmon.py` `commmon.pyc`可以删了，然后打开我们拖出来的这个文件 进行修改 修改完了 再放回去
![3.png](https://i.loli.net/2018/11/27/5bfd58edda341.png)

修改内容：
注释该行`raise web.seeother('/vpro');`
将这个跳转页面注释了
![4.png](https://i.loli.net/2018/11/27/5bfd58f05c4ad.png)

同理操作
删除 `panelAuth.pyc`
修改 `panelAuth.py`

修改内容：
添加`result= {'status' : True}`
![5.png](https://i.loli.net/2018/11/27/5bfd58f0cd528.png)

同理操作
删除 `panelPlugin.pyc`
修改 `panelPlugin.py`

修改内容：
删除了不用的东西
为我们的付费页面改个名
![6.png](https://i.loli.net/2018/11/27/5bfd58f0d1fcf.png)

修改完成 我们重启一下我们的宝塔
`service bt restart`
![7.png](https://i.loli.net/2018/11/27/5bfd58ef5ba76.png)

### 修改完成
我们欣赏一下我们的修改结果
![8.png](https://i.loli.net/2018/11/27/5bfd58f0cfab8.png)

ps.**网站防篡改程序** 这个无法使用

