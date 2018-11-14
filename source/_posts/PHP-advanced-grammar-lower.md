---
title: PHP - 04 进阶语法(下)
date: 2018-11-13 09:44:25
categories:
 - PHP学习
tags:
 - PHP
 - basic
 - 安装与配置
description: 继续我们的挑战
photos: 2018/11/13/PHP-advanced-grammar-lower/0.jpg
---

这一节我们来讲类





## 面向对象

### 成员变量

```php
<?php
class Person
{
    public $name = 'tom';
    public $age = '18';
}

$test = new Person();
echo 'My name is ' . $test->name . '我' . $test->age . '岁了';
?>
// 输出结果My name is Tom我18岁了
```
### 成员函数

```php
<?php
class Person
{
    public function talk()
    {
        echo 'PHP is the best language';
    }
}

$test = new Person();
$test->talk();
//输出结果 PHP is the best language
?>
```
### 构造函数

在每次创建新对象时会先调用此方法，一般用于赋初操作
```php
<?php
class Person
{
    public $name;
    public $age;
    function __construct(){
        $this->name = 'Tom';
        $this->age = 18;
    }
    public function talk(){
        echo 'My name is ' . $this->name . '我' . $this->age . '岁了';
    }
}
$test = new Person();
$test->talk();
// 输出结果My name is Tom我18岁了
?>
```
### 析构函数

析构函数会在到某个对象的所有引用都被删除或者当对象被显式销毁时执行
```php
<?php
class Person
{
    public $name;
    public $age;
    function __construct(){
        $this->name = 'Tom';
        $this->age = 18;
    }
    function __destruct(){
        echo 'goodbye';
    }
    public function talk(){
        echo 'My name is ' . $this->name . '我' . $this->age . '岁了';
    }
}
$test = new Person();
$test->talk();
?>
// 输出结果Myname is Tom我18岁了goodbye
```
### 继承
PHP 使用关键字extends来继承一个类 PHP不支持多继承
```php
<?php
class Person
{
    public function talk(){
        echo "hello everybody";
    }
}

class per1 extends Person
{

}

$test = new Per1();
$test->talk();
//输出结果 hello everybody
?>
```

### 方法重写
如果从父类继承的方法不能满足子类的需求，可以对其进行改写，这个过程叫方法的覆盖（override），也称为方法的重写。
```php
<?php
class Person
{
    public function talk(){
        echo "hello everybody";
    }
}

class per1 extends Person
{
    public function talk(){
        echo "ni,hao";
    }
}

$test = new Per1();
$test->talk();
//输出结果 hello everybody
?>
```

### 访问权限

 - public（公有）：公有的类成员可以在任何地方被访问。
 - protected（受保护）：受保护的类成员则可以被其自身以及其子类和父类访问。
 - private（私有）：私有的类成员则只能被其定义所在的类访问。

### 自学部分

#### 接口

使用关键字`interface` 定义
使用关键字`implements`实现
使用接口（interface），可以指定某个类必须实现哪些方法，但不需要定义这些方法的具体内容。 

#### 抽象

使用关键字 `abstract` 定义
使用关键字 `extends` 继承
任何一个类，如果它里面至少有一个方法是被声明为抽象的，那么这个类就必须被声明为抽象的。
>继承一个抽象类的时候，子类必须定义父类中的所有抽象方法

### 关键字

#### Static
声明类属性或方法为静态，就可以不实例化类而直接访问。静态属性不能通过一个类已实例化的对象来访问
>静态属性不可以由对象通过 -> 操作符来访问。

#### Final
如果父类中的方法被声明为 final，则子类无法覆盖该方法。如果一个类被声明为 final，则不能被继承。


