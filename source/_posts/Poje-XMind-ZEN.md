---
title: 手动破解 XMind ZEN
date: 2018-12-12 14:29:57
categories:
 - pojie
tags:
 - pojie
 - 小配件
 - 安装与配置
description: 别再为水印和弹窗烦恼了
photos: https://i.loli.net/2018/12/12/5c1128dfed59f.png
---

首先说明一下，尊重作者的产品。

本片文章思路来源于[dx老哥的文章](https://dxkite.cn/2018/11/17/xmind-zen-remove-watermark/)，仅加以完善。

>`XMind ZEN` 是一款免费的软件，只是在导出的时候安排上了专属水印

这次的破解 采用绕过式 仅属于娱乐

## 干货

首先我们需要了解一下我们的`XMind ZEN`的安装位置在哪:
`C:\Program Files\XMind ZEN`
![1.png](https://i.loli.net/2018/12/12/5c1128e0927a4.png)

我们采用的方法 不是删除，而是替换

### 导出水印

然后我们需要了解一下

矢量图文件位置：`resources\out\imgs\[类型]-watermark-[语言].svg`
比如：中文的PNG导出的水印：矢量图文件位置：`resources\out\imgs\png-watermark-zh-CN.svg`

#### PNG去水印

因为我们大部分采用的都是中文模式，所以对应的文件应该是：
`resources\out\imgs\png-watermark-zh-CN.svg`

这里拿英文版本的进行对比
![2.png](https://i.loli.net/2018/12/12/5c1128f18f10b.png)

我们将不透明度设置为0，即全透明，不影响导出

#### PDF去水印

pdf背景水印路径：
`resources\app\out\imgs\print-watermark-zh-CN.svg`
![3.png](https://i.loli.net/2018/12/12/5c1128efbbad1.png)
将它设置为透明 `opacity="0"`

pdf 底部水印
`resources\app\out\imgs\pdf-footer-zh-CN.svg`
![4.png](https://i.loli.net/2018/12/12/5c1128f1900c3.png)
我们可以考虑下 添加透明度 `opacity="0"`

到这里 我们其实可以发现
除了手动添加一定内容，也可以考虑把水印内容全部删除，也有同样的奇效

### 订阅弹窗

在保存的时候时常会出现一个窗口，提示你订阅购买该产品
![5.png](https://i.loli.net/2018/12/12/5c1128eadb0d3.png)

这个比较神奇
首先我们找到路径
`resources\app\out\modal-activateAlert.js`
发现这个js文件压缩在一起了

于是

找一个[在线js格式化](http://tool.chinaz.com/tools/jsformat.aspx) `格式化`一下

然后再复制粘贴回来

于是奇效发生了

ps.只适合 `v9.1.3`版本之前，因为在这个版本之后对文件进行了打包
可以考虑到该文件下
`resources\app\locales\new_translations.json`
进行修改取消更新提醒 `"Software Update": false,`

## 附件
[XMind ZEN v9.0.6](https://www.lanzous.com/i2lfoeb)