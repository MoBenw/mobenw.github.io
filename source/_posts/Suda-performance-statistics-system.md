---
title: 记一次suda框架之简单成绩系统
date: 2018-08-10 23:05:13
categories: Suda框架学习
tags: 
 - Suda
description: 正在学习会长的suda框架，努力成为一个优秀的开发狗 
photos: https://i.loli.net/2018/11/27/5bfd54fa49268.png
---
<!-- ![开发狗](Suda-performance-statistics-system/0.png)正在学习会长的suda框架，努力成为一个优秀的开发狗 -->
<!--more-->

----

### 创建一个项目

作为一个萌新 对创建一个新项目后 对项目的结构可能会有所陌生 不知道该有什么

所以这里可以复制之前的项目 简单的说就是复制一个`app`文件夹 然后改名为`statistical`

关于里面的内容
>`./resoure` 目录下
>>`./config/router.json` # 路由文件内容当然要清理
>>`./template/defalut/` # 因为你需要新写入模板 所以该目录下的模板建议删了

>`./share` 目录下
>>`./table/` #库文件 因为你可能不适用这些 所以删了

>`./src` 目录下
>>`./` #响应文件 差不多是与模板对应的 所以删了

>`./module.json` #模板的配置文件 所以内筒清理

关于data文件 data是自动生成的 所以 为了防止之前执行的东东 影响本次 所以 删了

目录结构


![1](https://i.loli.net/2018/11/27/5bfd551fb784f.png)

ps.为啥这里我不适用那个高逼格的制表符 是因为没用过 不会用...

**大佬语录**
>template 下的是模板文件
>src的文件是页面响应文件
>share的文件是库文件


### 设置配置文件
#### 模板配置 **module.json**

```json
{
    "name": "dxkite/statistical",
    "namespace": "dxkite/statistical",
    "authors": [{
        "name": "dxkite",
        "email": "dxkite@qq.com"
    }],
    "import": {
        "share": {
            "dxkite\\statistical": "share"
        },
        "src": {
            "dxkite\\statistical\\response": "src"
        }
    },
    "discription": "DXkite的成绩统计模块",
    "require": {},
    "version": "1.0.0"
}
```

#### 启用模块 **manifast.json**

```json
{
    "name": "dxkite-statistical-app",
    "namespace": "dxkite\\statistical",
    "version": "1.0-dev",
    "application": "suda\\core\\Application",
    "modules": ["suda", "statistical"],
    "reachable": ["statistical"],
    "language": "zh-CN",
    "url": {
        "mode": 0,
        "beautify": true,
        "rewrite": true
    }
}
```

#### 表单配置 **statistic.json** 

```json
{
    "table_id_1": {
        "name": "学生XXX统计表",
        "fields": {
            "math": {
                "name": "数学成绩",
                "type": "number"
            },
            "english": {
                "name": "英语成绩",
                "type": "number"
            }
        }
    },
    "table_id_2": {
        "name": "学生XXX统计表-2",
        "fields": {
            "math": {
                "name": "数学成绩",
                "type": "number"
            },
            "english": {
                "name": "英语成绩",
                "type": "number"
            }
        }
    }
}
```

#### 路由配置 **router.json**

```json
{
    "index": {
        "url": "\/",
        "class": "dxkite\\statistical\\response\\IndexResponse"
    },
    "table": {
        "url": "\/{table_id:string}",
        "class": "dxkite\\statistical\\response\\TableResponse"
    },
    "download": {
        "url": "\/{table_id:string}\/download",
        "class": "dxkite\\statistical\\response\\DownloadResponse"
    }
}
```

案例分析请移步 会长文章

### 模板及响应文件
#### **StatisticTable.php**
这是放在 `./share/table` 目录下的 相当于库文件吧

```php
<?php
namespace dxkite\statistical\table;
class StatisticTable extends \suda\archive\Table {

    public function  __construct(){
        // 数据表名
        parent::__construct('statistic');
    }

    protected function onBuildCreator($table){
        $table->fields(
            $table->field('id','bigint',20)->primary()->auto()->comment('自动增长ID'),
            $table->field('student_id','varchar',80)->key()->comment('学号'),
            $table->field('table_id','varchar',80)->key()->comment('姓名'),
            $table->field('name','varchar',80),
            $table->field('data','text')
        );
        return $table;
    }

    protected function _inputDataField($data){
        return serialize($data);
    }

    protected function _outputDataField($data){
        return unserialize($data);
    }
}
```

#### **index.tpl.html**
你可能需要一个index 
![2](https://i.loli.net/2018/11/27/5bfd5536b2fdb.png)

这个界面可以自己制作
一个`<table>`
需要注意的地方就是 url的生成方式

![3](https://i.loli.net/2018/11/27/5bfd554589279.png)

也可以参考我的

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Index - 备选表单</title>
</head>
<body>

    <table>
        <tr>
            <th>
                ID
            </th>
            <th>
                名称
            </th>
            <th>
                操作
            </th>
        </tr>
        <tr>
            <td>
                table_id_1
            </td>
            <td>
                学生XXX统计表
            </td>
            <td>
                <a href="@u('table', 'table_id_1' )">填写</a>
                <a href="@u('download','table_id_1')">下载</a>
            </td>
        </tr>
        <tr>
            <td>
                table_id_2
            </td>
            <td>
                学生XXX统计表-2
            </td>
            <td>
                <a href="@u('table', 'table_id_2' )">填写</a>
                <a href="@u('download','table_id_2')">下载</a>
            </td>
        </tr>
    </table>

</body>
</html>
```

#### **TableResponse.php && table.tpl.html**

下面的这个代码 的作用是 你在url里输入什么 他就会返回什么 纯属好玩 给你玩玩的 

应该放在 index之前的 因为index弄好后会有连接 难免会手痒点两下

##### **TableResponse.php**
```php
<?php
namespace dxkite\statistical\response;

use suda\core\Request;

class TableResponse extends \suda\core\Response
{
    public function onRequest(Request $request)
    {
        echo $request->get('table_id');  
    }
}
```

##### **table.tpl.html**
table的模板设计
```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>{{$:name}} - 填写表单</title>
</head>

<body>
    <h3>{{$:name}}</h3>
    <form action="@u" method="post">
    <table>
        <tr>
            <th>姓名</th>
            <td>
                <input type="text" name="name" />
            </td>
        </tr>
        <tr>
            <th>学号</th>
            <td>
                <input type="text" name="number" />
            </td>
        </tr>
        @foreach ($:fields as $id => $field) 
        <tr>
            <th>{{$field['name']}}</th>
            <td>
                @if ($field['type'] == 'text')
                    <textarea name="data[{{$id}}]" cols="30" rows="10" required></textarea>
                @elseif ($field['type'] == 'number')
                    <input type="number" name="data[{{$id}}]" required> 
                @else
                    <input type="text" name="data[{{$id}}]" required> 
                @endif
            </td>
         @endforeach
        </tr>
        
    </table>
    <button>提交</button>
</form>
</body>

</html>
```

##### **TableResponse.php**
完善过后一次的响应文件
```php
<?php
namespace dxkite\statistical\response;

use suda\core\Request;

class TableResponse extends \suda\core\Response
{
    public function onRequest(Request $request)
    {
        
        $tables = app()->getModuleConfig(app()->getFileModule(__FILE__), 'statistic');
        $tableId = $request->get('table_id');
        // 判断是否存在ID
        if (isset($tables[$tableId])) {
            $view = $this->page('table');
            $view->set('fields',$tables[$tableId]['fields']);
            $view->set('name',$tables[$tableId]['name']);
            $view->render();
        } else {
            // 显示404界面
            hook()->exec('system:404');
        }
    }
}
```

##### **TableResponse.php**
再次升级 新增写入数据
你可能需要一个`state.tpl.html`后面有

```php
<?php
namespace dxkite\statistical\response;

use suda\core\Request;

class TableResponse extends \suda\core\Response
{
    public function onRequest(Request $request)
    {
        $tables = app()->getModuleConfig(app()->getFileModule(__FILE__), 'statistic');
        $tableId = $request->get('table_id');
        // 判断是否存在ID
        if (isset($tables[$tableId])) {
            if ($request->hasPost()) {
                // 显示结果页面
                $view = $this->page('state');
                if ($type = $this->insertData($tableId, $request)) {
                    if ($type == 1) {
                        $view->set('message','写入成功');
                    } else {
                        $view->set('message','数据未更新');
                    }
                } else {
                    $view->set('message','写入失败');
                }
                $view->render();
            } else {
                $view = $this->page('table');
                $view->set('fields', $tables[$tableId]['fields']);
                $view->set('name', $tables[$tableId]['name']);
                $view->render();
            }
        } else {
            // 显示404界面
            hook()->exec('system:404');
        }
    }

    public function insertData(string $tableId, Request $request): int
    {
        $table = new \dxkite\statistical\table\StatisticTable;
        if ($request->post('name', null) && $request->post('number', null) && $request->post('data', null)) {
            // 查询条件
            $where = [
                'table_id' => $tableId,
                'student_id' => $request->post('number')
            ];
            // 如果存在学号相同，则更新记录
            // 根据ID更新会更快
            if ($data = $table->select(['id'],$where)->fetch()) {
                if ($table->updateByPrimaryKey($data['id'], [
                    'name' => $request->post('name'),
                    'data' => $request->post('data')
                ])) {
                    // 更新成功
                    return 1;
                } else {
                    // 未跟新
                    return 2;
                }
            } else {
                // 插入新记录
                $id = $table->insert([
                    'table_id' => $tableId,
                    'student_id' => $request->post('number'),
                    'name' => $request->post('name'),
                    'data' => $request->post('data'),
                ]);
                if ($id > 0) {
                    return 1;
                }
            }
        }
        return 0;
    }
}
```

#### **DownloadResponse.php**
下载有两个版本

##### 非密码版本

```php
<?php
namespace dxkite\statistical\response;

use suda\core\Request;

class DownloadResponse extends \suda\core\Response
{
    public function onRequest(Request $request)
    {
        $tables = app()->getModuleConfig(app()->getFileModule(__FILE__), 'statistic');
        $tableId = $request->get('table_id');
        // 判断是否存在ID
        if (isset($tables[$tableId])) {
            $data = $this->exportData($tableId, $tables[$tableId]['fields']);
            // 暂存文件
            $path = RUNTIME_DIR .'/'. $tableId .'.csv';
            storage()->put($path,$data);
            // 生成文件下载
            $this->file($path);
        } else {
            // 显示404界面
            hook()->exec('system:404');
        }
    }

    public function exportData(string $tableId, array $fields): string
    {
        $table = new \dxkite\statistical\table\StatisticTable;
        // 列出同一个表格
        $datas =  $table->listWhere(['table_id' => $tableId]);
        // 生成表头
        $csv = [];
        $csv[0] = [ 0 =>'学号', 1 => '姓名'];
        // 表头ID
        $header = [0,1];
        foreach ($fields as $id  => $value) {
            $csv[0][$id] = $value['name'];
            $header[] = $id;
        }
        // 生成数据
        foreach ($datas as $data) {
            $id = count($csv);
            $csv[$id][0]= $data['student_id'];
            $csv[$id][1]= $data['name'];
            foreach ($data['data'] as $index => $value) {
                $csv[$id][$index]=$value;
            }
        }
        $text = '';
        foreach ($csv as $data) {
            $row = [];
            foreach ($header as $id) {
                $row[] = $data[$id];
            }
            $text .= implode(',', $row) . "\r\n";
        }
        return $text;
    }
}
```

##### 密码验证版本

```php
<?php
namespace dxkite\statistical\response;

use suda\core\Request;

class DownloadResponse extends \suda\core\Response
{
    public function onRequest(Request $request)
    {
        $tables = app()->getModuleConfig(app()->getFileModule(__FILE__), 'statistic');
        $tableId = $request->get('table_id');
        // 判断是否存在ID
        if (isset($tables[$tableId])) {
            if (isset($tables[$tableId]['password'])) {
                if ($request->get('password') == $tables[$tableId]['password']) {
                    $this->download($tableId, $tables[$tableId]['fields']);
                } else {
                    echo '密码错误';
                }
            } else {
                $this->download($tableId, $tables[$tableId]['fields']);
            }
        } else {
            // 显示404界面
            hook()->exec('system:404');
        }
    }

    public function download(string $tableId, array $fields)
    {
        $data = $this->exportData($tableId, $fields);
        // 暂存文件
        $path = RUNTIME_DIR .'/'. $tableId .'.csv';
        storage()->put($path, $data);
        // 生成文件下载
        $this->file($path);
    }

    public function exportData(string $tableId, array $fields): string
    {
        $table = new \dxkite\statistical\table\StatisticTable;
        // 列出同一个表格
        $datas =  $table->listWhere(['table_id' => $tableId]);
        // 生成表头
        $csv = [];
        $csv[0] = [ 0 =>'学号', 1 => '姓名'];
        // 表头ID
        $header = [0,1];
        foreach ($fields as $id  => $value) {
            $csv[0][$id] = $value['name'];
            $header[] = $id;
        }
        // 生成数据
        foreach ($datas as $data) {
            $id = count($csv);
            $csv[$id][0]= $data['student_id'];
            $csv[$id][1]= $data['name'];
            foreach ($data['data'] as $index => $value) {
                $csv[$id][$index]=$value;
            }
        }
        $text = '';
        foreach ($csv as $data) {
            $row = [];
            foreach ($header as $id) {
                $row[] = $data[$id];
            }
            $text .= implode(',', $row) . "\r\n";
        }
        return $text;
    }
}
```

使用密码验证时需要设置密码

![4](https://i.loli.net/2018/11/27/5bfd55581794c.png)

你所需要的下载姿势是
`./dev.php/table_id_1/download?password=密码`

#### **state.tpl.html**
该页面是为了显示 数据写入信息的
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Action PAGE</title>
</head>
<body>
    <P>{{ $:message }}</P>
</body>
</html>
```

### 个人姿势
为了方便在url传值 我对`download.tpl.html`、`DownloadResponse.php`进行了修改
新增了：
- 输入框输入
- 密码提示
- 当前输入密码

![5](https://i.loli.net/2018/11/27/5bfd5565a4b11.png)
#### **download.tpl.html**

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Action PAGE</title>
</head>
<body>
    <form action="@u" method="GET">
        Password:<input type="password" name="password">
        <input type="submit" value="Submit">
    </form>
    <div>
        <div>下载密码: {{ $:pwd }} </div>
        <div>你的输入的密码: {{ $:ypwd }}</div>
        <div>当前情况: {{ $:response }} </div>
    </div>
</body>
</html>
```


#### **DownloadResponse.php**

```php
<?php
namespace mobenw\statistical\response;

use suda\core\Request;

class DownloadResponse extends \suda\core\Response
{
    public function onRequest(Request $request)
    {
        $tables = app()->getModuleConfig(app()->getFileModule(__FILE__), 'statistic');
        $tableId = $request->get('table_id');
        // 判断是否存在ID
        if (isset($tables[$tableId])) {
            if (isset($tables[$tableId]['password'])) {
                // 显示密码填写界面
                $view = $this->page('download');

                //设置页面变量
                $view->set('pwd',$tables[$tableId]['password']);
                $view->set('ypwd',$request->get('password'));

                if ($request->get('password') == $tables[$tableId]['password']) {
                    $view->set('response','密码正确，请下载');
                    $this->download($tableId, $tables[$tableId]['fields']);
                } else {
                    $view->set('response','密码错误');
                }

                // 渲染模板显示出来
                $view->render();
            } else {
                $this->download($tableId, $tables[$tableId]['fields']);
            }
        } else {
            // 显示404界面
            hook()->exec('system:404');
        }
    }

    public function download(string $tableId, array $fields)
    {
        $data = $this->exportData($tableId, $fields);
        // 暂存文件
        $path = RUNTIME_DIR .'/'. $tableId .'.csv';
        storage()->put($path, $data);
        // 生成文件下载
        $this->file($path);
    }

    public function exportData(string $tableId, array $fields): string
    {
        $table = new \mobenw\statistical\table\StatisticTable;
        // 列出同一个表格
        $datas =  $table->listWhere(['table_id' => $tableId]);
        // 生成表头
        $csv = [];
        $csv[0] = [ 0 =>'学号', 1 => '姓名'];
        // 表头ID
        $header = [0,1];
        foreach ($fields as $id  => $value) {
            $csv[0][$id] = $value['name'];
            $header[] = $id;
        }
        // 生成数据
        foreach ($datas as $data) {
            $id = count($csv);
            $csv[$id][0]= $data['student_id'];
            $csv[$id][1]= $data['name'];
            foreach ($data['data'] as $index => $value) {
                $csv[$id][$index]=$value;
            }
        }
        $text = '';
        foreach ($csv as $data) {
            $row = [];
            foreach ($header as $id) {
                $row[] = $data[$id];
            }
            $text .= implode(',', $row) . "\r\n";
        }
        return $text;
    }
}
```
### 后记
基本教程应该就是这样了 不对 是心酸历程就是这样了
这里附上会长大佬的链接
[https://dxkite.cn/2018/08/05/suda-results-statistical-design/](https://dxkite.cn/2018/08/05/suda-results-statistical-design/)
[https://dxkite.cn/2018/08/06/suda-results-statistical-router/](https://dxkite.cn/2018/08/06/suda-results-statistical-router/)
[https://dxkite.cn/2018/08/07/suda-results-statistical-data/](https://dxkite.cn/2018/08/07/suda-results-statistical-data/)
