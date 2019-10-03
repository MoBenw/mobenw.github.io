---
title: PHP - 03 进阶语法(上)
date: 2018-11-08 21:47:15
categories:
 - PHP学习
tags:
 - PHP
 - basic
description: 是时候给自己来点挑战了
photos: https://i.loli.net/2018/11/27/5bfd47018f9a8.jpg
---

回复一下上次碰到的问题：
>1. PHP有没有类似C语言的`scanf()`,答案是没有,PHP是作用于`服务器端的脚本语言`,所以无法获取用户的键盘输入。
>2. 关于常量的定义，除了`define()函数`还有一个常用的定义方法 `const `
>3. PHP的变量是自动类型转换，指定义变量时不需要指定变量的数据类型，PHP会根据具体引用变量的具体应用环境，将变量转换为合适的数据类型。所以当一个整型与一个数字字符串相加时计算的结果是一个整型的。
>4. 

---

`PHP is the best language` 
[http://php.net/manual/fa/faq.languages.php](http://php.net/manual/fa/faq.languages.php)

## 字符串

### 并置运算符

```php
<?php
$txt1 = 'PHP is ';
$txt2 = 'the best language';
$txt3 = $txt1 . $txt2;
echo $txt3;
//输出结果 PHP is the best language
?>
```
### 常用函数

#### strlen() 函数

```php
<?php 
echo strlen(`PHP is the best language`); 
//输出结果为30
?> 
```

## 数组

### 数组的定义
>在`PHP`中，使用array() 函数创建数组
```php
<?php
$txt=array("PHP","is","the","best","language");
echo $txt[0] . " " . $txt[1] . " " . $txt[2] . " " . $txt[3] . " " . $txt[4];
//输出结果 PHP is the best language
?>
```
### 数组的分类
 - 数值数组 - 带有数字 ID 键的数组
 - 关联数组 - 带有指定的键的数组，即键值对数组
 - 多维数组 - 包含一个或多个数组的数组

### 数组的遍历
1. 循环遍历
2. var_dump() // 用于输出变量的相关信息

## 魔术常量

### 使用方法

直接调用即可
```php
<?php
echo '这是第 " '  . __LINE__ . ' " 行';
?>
//这是第" 2 " 行
```
### 常用魔术常量

PHP中常见的魔术变量

| 名称 | 说明 |
| - | :- |
| `__LINE__` | 文件中的当前行号 |
| `__FILE__` | 文件的完整路径和文件名。如果用在被包含文件中，则返回被包含的文件名。自 PHP 4.0.2 起，`__FILE__` 总是包含一个绝对路径（如果是符号连接，则是解析后的绝对路径），而在此之前的版本有时会包含一个相对路径。|
| `__DIR__` | 文件所在的目录。如果用在被包括文件中，则返回被包括的文件所在的目录。它等价于 dirname(`__FILE__`)。除非是根目录，否则目录中名不包括末尾的斜杠。（PHP 5.3.0中新增） = |
| `__FUNCTION__` | 函数名称（PHP 4.3.0 新加）。自 PHP 5 起本常量返回该函数被定义时的名字（区分大小写）。在 PHP 4 中该值总是小写字母的。 |
| `__CLASS__` | 类的名称（PHP 4.3.0 新加）。自 PHP 5 起本常量返回该类被定义时的名字（区分大小写）。在 PHP 4 中该值总是小写字母的。类名包括其被声明的作用区域（例如 Foo\Bar）。注意自 PHP 5.4 起 `__CLASS__` 对 trait 也起作用。当用在 trait 方法中时，`__CLASS__` 是调用 trait 方法的类的名字。 |
| `__TRAIT__` | Trait 的名字（PHP 5.4.0 新加）。自 PHP 5.4 起此常量返回 trait 被定义时的名字（区分大小写）。Trait 名包括其被声明的作用区域（例如 Foo\Bar）。 |
| `__METHOD__` | 类的方法名（PHP 5.0.0 新加）。返回该方法被定义时的名字（区分大小写）。 |
| `__NAMESPACE__` | 当前命名空间的名称（区分大小写）。此常量是在编译时定义的（PHP 5.3.0 新增）。 |

## 函数

### 函数的定义

使用 `function` 开头表示为一个函数

```php
<?php
function functionName()
{
    // Code...
}
?>
```

### 带参数的函数

```php
<?php
function functionName($value)
{
    // Code...
}
?>
```

### 带返回值的函数

```php
<?php
function functionName()
{
    // Code...
    return 1;
}
?>
```
