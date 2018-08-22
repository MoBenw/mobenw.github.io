---
title: STL之Vector函数
date: 2018-08-13 22:15:31
categories: C++学习
tags:
 - C++
 - STL
 - Vector
description: 就让vector函数引领你进入STL的世界吧
photos: 
 - "2018/08/13/STL-vector-function/0.gif"
---

<div hidden="hidden">感谢百度各位大佬的指点
<a href="https://blog.csdn.net/yjunyu/article/details/77728410?locationNum=10&fps=1">https://blog.csdn.net/yjunyu/article/details/77728410?locationNum=10&fps=1</a>
</div>


萌新表示需要百度的指点

~!@#$%^&*()_+

### 介绍

向量 vector 是一种对象实体, 能够容纳许多其他类型相同的元素, 因此又被称为容器。 与string相同, vector 同属于STL(Standard Template Library, 标准模板库)中的一种自定义的数据类型, 可以广义上认为是数组的增强版。

ok 简单说 动态数组

### 定义及使用

#### 头文件

```c++
#include<vector>
using namespace std; //vector属于std命名域
```

#### 定义变量

```c++
// using namespace std;
using std::vector; //将std中的vector 特地指出来
vector<int> v; //一维数组
vector<vector<int> >v; //二维数组 注意有个空格方便区分

//全名定义
std::vector<int> v;
```

### 初始化

#### 一维数组

##### 带参数的构造函数初始化
```c++
//初始化一个size为0的vector
vector<int> v;
```

##### 带参数的构造函数初始化
```c++
//初始化size,但每个元素值为默认值
vector<int> v(10);    //初始化了10个默认值为0的元素
//初始化size,并且设置初始值
vector<int> v(10,1);    //初始化了10个值为1的元素
```
##### 通过数组地址初始化
```c++
int a[5] = {1,2,3,4,5};
//通过数组a的地址初始化，注意地址是从0到5（左闭右开区间）
vector<int> b(a, a+5);
```
##### 通过同类型的vector初始化
```c++
vector<int> a(5,1);
//通过a初始化
vector<int> b(a);
```
##### 通过insert初始化
```c++
//insert初始化方式将同类型的迭代器对应的始末区间（左闭右开区间）内的值插入到vector中
vector<int> a(6,6);
vecot<int> b;
//将a[0]~a[2]插入到b中，b.size()由0变为3
b.insert(b.begin(), a.begin(), a.begin() + 3);

insert也可通过数组地址区间实现插入
int a[6] = {6,6,6,6,6,6};
vector<int> b;
//将a的所有元素插入到b中
b.insert(b.begin(), a, a+7);

此外，insert还可以插入m个值为n的元素
//在b开始位置处插入6个6
b.insert(b.begin(), 6, 6);
```
##### 通过copy函数赋值
```c++
vector<int> a(5,1);
int a1[5] = {2,2,2,2,2};
vector<int> b(10);

/*将a中元素全部拷贝到b开始的位置中,注意拷贝的区间为a.begin() ~ a.end()的左闭右开的区间*/
copy(a.begin(), a.end(), b.begin());

//拷贝区间也可以是数组地址构成的区间
copy(a1, a1+5, b.begin() + 5);
```




#### 二维数组
>首先，需要明确的是，在计算机的世界中，根本不存在二维数组，只是使用者的一个概念罢了。其实我们所谓的二维数组也必须是一段连续的内存,由于计算机的内存是一维的，多维数组的元素应排成线性序列后存入存储器。所以采用顺序存储方法表示数组。

方法一
```c++
vector<vector<int> > array; //这个m一定不能少
//初始化一个m*n的二维数组
for(int i=0;i<m;i++) {
    array.push_back(vector<int>());
}
for (int i=0;i<array.size();i++){
        for (int j=0;j<n;j++){
            array[i].push_back(j);
        }
    }
```
方法二
```c++
vector<vector<int> > array(m); //这个m一定不能少
//初始化一个m*n的二维数组
for(int i=0;i<n;i++) {
    array[i].resize(0);
}
```
方法三
```c++
vector<vector<int> > array(m ,vector<int>(n)); //m*n的二维vector
```
vector 容器与数组相比其优点在于它能够根据需要随时自动调整自身的大小以便容下所要放入的元素。此外, vector 也提供了许多的方法来对自身进行操作。

### Vector常用函数表

|函数|描述|
|-|-|
|v.assign(begin,end) v.assign(n,elem)|将[begin; end)区间中的数据赋值给v 将n个elem的拷贝赋值给v|
|at(index)|传回索引index所指的数据 如果index越界 抛出out_of_range|
|**back()**|传回最后一个数据 不检查这个数据是否存在|
|**begin()**|传回迭代器中的第一个数据地址 数组的首元素地址|
|capacity()|返回容器中数据个数|
|**clear()**|移除容器中所有数据|
|**empty()**|判断容器是否为空 为空时返回真 否则返回假|
|**end()**|指向迭代器中末端元素的下一个 指向一个不存在元素|
|**erase(pos)**|删除pos位置的数据 传回下一个数据的位置|
|erase(begin,end)|删除[begin,end)区间的数据 传回下一个数据的位置|
|**front()**|传回第一个数据|
|get_allocator|使用构造函数返回一个拷贝|
|**insert(pos,elem)**|在pos位置插入一个elem拷贝 传回新数据位置|
|insert(pos,n,elem)|在pos位置插入n个elem数据。无返回值|
|insert(pos,begin,end)|在pos位置插入在[begin,end)区间的数据 无返回值|
|max_size()|返回容器中最大数据的数量|
|**pop_back()**|删除最后一个数据|
|**push_back(elem)**|在尾部加入一个数据|
|rbegin()|传回一个逆向队列的第一个数据|
|rend()|传回一个逆向队列的最后一个数据的下一个位置|
|resize(num)|重新指定队列的长度|
|reserve()|保留适当的容量|
|**size()**|返回容器中实际数据的个数|
|a.swap(b) swap(a,b)|将a和b元素互换|
|operator[]|返回容器中指定位置的一个引用|

