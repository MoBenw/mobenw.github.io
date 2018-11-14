---
title: PHP - 05 表单
date: 2018-11-14 22:31:36
categories:
 - PHP学习
tags:
 - PHP
 - basic
 - 安装与配置
description: 表单~~
photos: 2018/11/14/PHP-form/0.jpg
---

我们简单的来讲讲表单


## 全局变量
 - $GLOBALS
 - $_SERVER
 - $_REQUEST
 - $_POST
 - $_GET
 - $_FILES
 - $_ENV
 - $_COOKIE
 - $_SESSION

### $_SERVER

$_SERVER 是一个包含了诸如头信息(header)、路径(path)、以及脚本位置(script locations)等等信息的数组。

### $_POST

预定义的 $_GET 变量用于收集来自 method="post" 的表单中的值。

### $_GET

预定义的 $_GET 变量用于收集来自 method="get" 的表单中的值。

### $_REQUEST

预定义的 $_REQUEST 变量可用来收集通过 GET 和 POST 方法发送的表单数据。

## 表单

### 输入框输入

```php
<html>
<head>
<meta charset="utf-8">
<title>表单</title>
</head>
<body>
 
<form method="post">
名字: <input type="text" name="name">
年龄: <input type="text" name="age">
<input type="submit" value="提交">
</form>
 
</body>
</html>

<?php if (isset($_POST["name"])) echo '欢迎'.$_POST["name"].'!'; ?><br>
<?php if (isset($_POST["age"])) echo '你的年龄是'.$_POST["age"].'岁。'; ?>
```

简单的表单处理就是这样
你获取到了数据
接下来可以进行判断，进行增删改查等操作