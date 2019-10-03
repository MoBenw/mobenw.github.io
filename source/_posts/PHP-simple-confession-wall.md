---
title: PHP - 06 简易表白墙
date: 2018-11-14 23:51:50
categories:
 - PHP学习
tags:
 - PHP
 - basic
description: 冲 实践吧
photos: https://i.loli.net/2018/11/27/5bfd461fd09f9.jpg
---

这次，我们直接从一个小应用开始

### 函数解释

`require_once()`
>`require_once()`语句在脚本执行期间包含并运行指定文件(通俗一点，括号内的文件会执行一遍)。此行为和require()语句类似，唯一区别是如果该文件中的代码已经被包含了，则不会再次包含。

`count()`
>计算数组中的单元数目，或对象中的属性个数

`array_key_exists()`
>检查数组里是否有指定的键名或索引

`file_exists()`
>检查文件或目录是否存在

`json_decode()`
>对 JSON 格式的字符串进行解码

`json_last_error()`
>返回最后发生的错误

`JSON_ERROR_NONE`
>常量---没有错误发生

`trim()`
>去除字符串首尾处的空白字符（或者其他字符）

`time()`
>返回当前的 Unix 时间戳

`date()`
>格式化一个本地时间／日期

`json_encode()`
>对变量进行 JSON 编码

### 逻辑

前端进行输入

php进行判断 如果输入成功则显示`写入成功`，如果写入是数据不完整 否则`写入失败`

表白墙历史采用的是一个迭代手段 使用for循环迭代将后端传输过来的数据进行list

read()函数将文件中的数据解码读取出来并以数组的形式保存

write()函数将数据编码加密写入到文件中


### 如何运行

在根目录运行命令：

```bash
php -S localhost:8080
```

打开浏览器，访问：http://localhost:8080/ 即可

### 文件说明

- index.php 项目界面显示
- lib.php 项目数据处理
- data.json 表白数据
- style.css 界面样式

### 更新历史

- v1.2
    - 修正显示
- v1.1 
    - 添加样式
    - 添加背景
- v1.0 
    - 基本功能

[源码下载链接](https://www.lanzous.com/i2e4dzi)