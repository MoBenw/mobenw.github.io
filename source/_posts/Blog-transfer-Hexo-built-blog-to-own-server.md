---
title: 转移Hexo搭建的博客到自己的阿里云服务器
date: 2018-10-20 18:43:07
categories: Hexo博客搭建
tags:
 - 安装与配置
 - Hexo
 - NexT
description: 这速度 你能满意 代码不背锅 绝对是服务器背锅
photos:
---

上一篇文章介绍了如何配置`Hexo`，但是在使用的时候发现`Github`的速度并不能让人满意，于是开始转战我的阿里云

### 创建一个 `git` 用户 专门运行 `git` 服务

```Bash
$ sudo adduser git
```
为了安全

### ssh 连接配对

```Bash
$ ssh-keygen
```
创建公钥私钥对
```Bash
$ ssh-copy-id -i .ssh/id_rsa.pub  用户名字@192.168.x.xxx
```
将公钥复制到远程机器中


我的ssh好像翻车了 但是问题不大 手动输入密码
这里的作用就是方便连接

>`ssh-keygen`  产生公钥与私钥对. 
>`ssh-copy-id` 将本机的公钥复制到远程机器的
>创建证书登录，把自己电脑的公钥，也就是 `~/.ssh/id_rsa.pub` 文件里的内容添加到服务器的 `/home/git/.ssh/authorized_keys` 文件中，添加公钥之后可以防止每次 push 都输入密码。

### 在服务器上弄个 Git 仓库

```
$ mkdir hexo.git
$ cd hexo.git
$ git init --bare
```
使用 --bare 参数，Git 就会创建一个裸仓库，为共享而存在

### 编写脚本
```Bash
`$ cd /home/git/hexo.git/hooks`
```

```Bash
`$ vim post-receive`
```

```Bash
#!/bin/sh
git --work-tree=/www/wwwroot/www.mobenw.cn --git-dir=/home/git/hexo.git checkout -f
```
>`/www/wwwroot/www.mobenw.cn` 网站目录
>`/home/git/hexo.git` 仓库

以上操作实现了自动部署的功能

### 提权
```Bash
$ chmod +x post-receive
为这个文件提权
```
```Bash
$ sudo chown -R git:git hexo.git
```
使`hexo.blog`该目录的拥有者为 `git`

`$ chmod 777 -R /www/wwwroot/www.mobenw.cn`
至少这里有写的权限

### 本地配置
本地`hexo`目录下的
**`_config.yml`**
```yml
deploy:
  type: git
  repo: 
    aliyun: git@192.168.x.xxx:/home/git/hexo.git
```

### 收工

接下来就是正常的 hexo 的操作...