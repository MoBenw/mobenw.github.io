---
title: 使用GitHub和Hexo搭建自己的博客
date: 2018-08-06 16:31:21
categories: 博客搭建
tags:
 - 安装与配置
 - Hexo
 - NexT
description: 博客是个好东西啊 第一次来体验一番由自己搭建的一个博客 有点简陋别笑 关于没有图片 是因为还没有还找到合适的图床
---


我这里选用的是GitHub.io以及Hexo来搭建自己的博客的

### 配置必备

> [git](https://git-scm.com/downloads)
>[node.js](http://nodejs.cn/download/)

#### git的安装
>Git是一个开源的分布式版本控制系统，用于敏捷高效地处理任何或小或大的项目。
>Git 是 Linus Torvalds 为了帮助管理 Linux 内核开发而开发的一个开放源码的版本控制软件。
>Git 与常用的版本控制工具 CVS, Subversion 等不同，它采用了分布式版本库的方式，不必服务器端软件支持

无需多讲，一路默认 

#### node.js的安装
>简单的说 Node.js 就是运行在服务端的 JavaScript。
>Node.js 是一个基于Chrome JavaScript 运行时建立的一个平台。
>Node.js是一个事件驱动I/O服务端JavaScript环境，基于Google的V8引擎，V8引擎执行Javascript的速度非常快，性能非常好。

操作空间不大，一路默认

### 正式开始

#### 安装 Hexo
进入命令行 输入命令

    npm install -g hexo

顺便把这个也安装一下 自动部署发布工具

      npm install hexo-deployer-git  --save

#### 初始化 Hexo
选择你博客存放的位置 (建议创建一个新的文件夹_初始化需要一个空的文件夹)
然后命令行输入命令

    hexo init

#### git主题
本身自带主题 可以暂时跳过该操作 若需要更换主题时再进行操作
>此处以我使用的主题为例
>进入你的 **themes**目录 命令行输入命令

    git clone https://github.com/iissnan/hexo-theme-next.git

>主题下载后需要进行以下操作才能更换
>根目录下的 **_config.yml**
>修改 xxxxx为你的主题名 ps.注意有空格
>themes: XXXXX

#### 本地浏览博客
命令行输入命令

```
hexo g
hexo s
```

>hexo g 生成
>hexo s 启动服务预览




> 在浏览器输入：**localhost:4000** 就可以进行访问
>Ctrl+C 即可退出

#### 写文章
根目录下命令行 输入命令
```
hexo new '文章名字'
```

>在source目下的 **_posts**目录下 会出现 **.md**文件以下为一般完整内容

```\---
title: postName #文章页面上的显示名称，一般是中文
date: 2013-12-02 15:30:16 #文章生成时间，一般不改，当然也可以任意修改
categories: 默认分类 #分类
tags: [tag1,tag2,tag3] #文章标签，可空，多标签请用格式，注意:后面有个空格
description: 附加一段文章摘要，字数最好在140字以内，会出现在meta的description里面
---
以下文章是正文
```


#### 上传到GitHub上
>首先你得有GitHub账号
>然后你创建了一个仓库为 **用户名.gitHub.io**
>ssh密钥自己配好

>根目录下 **_config.yml**文件内
>把你的git写进去 现在写的是我的 替换一下就ok了

```
deploy:
  type: git
  repo: git@github.com:MoBenw/MoBenw.github.io.git
```

满足以上条件
命令行 输入命令

    hexo clean && hexo g && hexo d

>hexo clean 清理缓存
>hexo g 生成
>hexo d 部署

#### 使用你的GitHub.io访问
到这里你就基本上会基本的GitHub上Hexo的博客搭建了 (感觉语句不通 不管了)


### 有关于README.md
>在 **source**目录下 创建一个 **README.md** 文件 里面是你要写的内容
>进入根目录 打开配置文件 **_config.yml** 
>修改 跳过渲染内容
>skip_render: README.md
