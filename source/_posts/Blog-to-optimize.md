---
title: 博客美化记
date: 2018-08-07 21:18:19
categories: Hexo博客搭建
tags: 
 - 安装与配置
 - Hexo
 - NexT
 - JavaScript
description: 当然要把博客打扮的美美的
---

### 不蒜子 浏览记录
```yml
busuanzi_count:
  # count values only if the other configs are false
  enable: true
  # custom uv span for the whole site
  site_uv: true
  site_uv_header: <i class="fa fa-user"></i> 访问人数
  site_uv_footer:
  # custom pv span for the whole site
  site_pv: true
  site_pv_header: <i class="fa fa-street-view"></i> 总访问量
  site_pv_footer: 次
  # custom pv span for one page only
  page_pv: true
  page_pv_header: <i class="fa fa-eye"></i> Visitors
  page_pv_footer: _
```

>因七牛强制过期『dn-lbstatics.qbox.me』域名，与客服沟通无果，只能更换域名到『busuanzi.ibruce.info』！
>修复最新无法显示 修改该文件 `/themes/next/layout/_third-party/analytics/busuanzi-counter.swig` 引用的域名 

### 给网页title添加一些搞怪特效

在`next\source\js\src`文件夹下创建`crash_cheat.js`
```js
<!--崩溃欺骗-->
 var OriginTitle = document.title;
 var titleTime;
 document.addEventListener('visibilitychange', function () {
     if (document.hidden) {
         $('[rel="icon"]').attr('href', "/img/TEP.ico");
         document.title = '╭(°A°`)╮ 页面崩溃啦 ~';
         clearTimeout(titleTime);
     }
     else {
         $('[rel="icon"]').attr('href', "/favicon.ico");
         document.title = '(ฅ>ω<*ฅ) 噫又好了~' + OriginTitle;
         titleTime = setTimeout(function () {
             document.title = OriginTitle;
         }, 2000);
     }
 });
```


在next\layout\_layout.swig文件中，添加引用（注：在swig末尾添加）：
```html
<!--崩溃欺骗-->
<script type="text/javascript" src="/js/src/crash_cheat.js"></script>
```
### 给页面的底部添加小js
在`next\source\js\src`文件夹下创建`chakhsu.js`
```js
var chakhsu = function (r) {
  function t() {
      return b[Math.floor(Math.random() * b.length)]
  }

  function e() {
      return String.fromCharCode(94 * Math.random() + 33)
  }

  function n(r) {
      for (var n = document.createDocumentFragment(), i = 0; r > i; i++) {
          var l = document.createElement("span");
          l.textContent = e(), l.style.color = t(), n.appendChild(l)
      }
      return n
  }

  function i() {
      var t = o[c.skillI];
      c.step ? c.step-- : (c.step = g, c.prefixP < l.length ? (c.prefixP >= 0 && (c.text += l[c.prefixP]), c.prefixP++) :
              "forward" === c.direction ? c.skillP < t.length ? (c.text += t[c.skillP], c.skillP++) : c.delay ?
              c.delay-- : (c.direction = "backward", c.delay = a) : c.skillP > 0 ? (c.text = c.text.slice(0,
                  -1), c.skillP--) : (c.skillI = (c.skillI + 1) % o.length, c.direction = "forward")), r.textContent =
          c.text, r.appendChild(n(c.prefixP < l.length ? Math.min(s, s + c.prefixP) : Math.min(s, t.length -
              c.skillP))), setTimeout(i, d)
  }
  var l = "I work with ",
      o = ["You", "JavaScript", "HTML & CSS", "Node.js", "React", "passion & love"].map(function (r) {
          return r + "."
      }),
      a = 2,
      g = 1,
      s = 5,
      d = 75,
      b = ["rgb(110,64,170)", "rgb(150,61,179)", "rgb(191,60,175)", "rgb(228,65,157)", "rgb(254,75,131)",
          "rgb(255,94,99)", "rgb(255,120,71)", "rgb(251,150,51)", "rgb(226,183,47)", "rgb(198,214,60)",
          "rgb(175,240,91)", "rgb(127,246,88)", "rgb(82,246,103)", "rgb(48,239,130)", "rgb(29,223,163)",
          "rgb(26,199,194)", "rgb(35,171,216)", "rgb(54,140,225)", "rgb(76,110,219)", "rgb(96,84,200)"
      ],
      c = {
          text: "",
          prefixP: -s,
          skillI: 0,
          skillP: 0,
          direction: "forward",
          delay: a,
          step: g
      };
  i()
};
chakhsu(document.getElementById('chakhsu'));

```

在next\layout\_layout.swig文件中，添加引用（注：在swig末尾添加）：
```html
<!--有趣的一段话-->
<script type="text/javascript" src="/js/src/chakhsu.js"></script>
```

在`layout\_partials\footer.swig` 添加
```html
<div>
  <p id="chakhsu">I work with passion<span style="color: rgb(255, 94, 99);">/</span><span style="color: rgb(96, 84, 200);">P</span><span
          style="color: rgb(191, 60, 175);">{</span><span style="color: rgb(198, 214, 60);">W</span><span style="color: rgb(76, 110, 219);">+</span></p>
</div>
```


### 右上角角标

`Blog/themes/next/layout/_layout.swig`
放在`<div class="headband"></div>`下方

```html
<a href="https://your-url" class="github-corner" aria-label="View source on GitHub"><svg width="80" height="80" viewBox="0 0 250 250" style="fill:#151513; color:#fff; position: absolute; top: 0; border: 0; right: 0;" aria-hidden="true"><path d="M0,0 L115,115 L130,115 L142,142 L250,250 L250,0 Z"></path><path d="M128.3,109.0 C113.8,99.7 119.0,89.6 119.0,89.6 C122.0,82.7 120.5,78.6 120.5,78.6 C119.2,72.0 123.4,76.3 123.4,76.3 C127.3,80.9 125.5,87.3 125.5,87.3 C122.9,97.6 130.6,101.9 134.4,103.2" fill="currentColor" style="transform-origin: 130px 106px;" class="octo-arm"></path><path d="M115.0,115.0 C114.9,115.1 118.7,116.5 119.8,115.4 L133.7,101.6 C136.9,99.2 139.9,98.4 142.2,98.6 C133.8,88.0 127.5,74.4 143.8,58.0 C148.5,53.4 154.0,51.2 159.7,51.0 C160.3,49.4 163.2,43.6 171.4,40.1 C171.4,40.1 176.1,42.5 178.8,56.2 C183.1,58.6 187.2,61.8 190.9,65.4 C194.5,69.0 197.7,73.2 200.1,77.6 C213.8,80.2 216.3,84.9 216.3,84.9 C212.7,93.1 206.9,96.0 205.4,96.6 C205.1,102.4 203.0,107.8 198.3,112.5 C181.9,128.9 168.3,122.5 157.7,114.1 C157.9,116.9 156.7,120.9 152.7,124.9 L141.0,136.5 C139.8,137.7 141.6,141.9 141.8,141.8 Z" fill="currentColor" class="octo-body"></path></svg></a><style>.github-corner:hover .octo-arm{animation:octocat-wave 560ms ease-in-out}@keyframes octocat-wave{0%,100%{transform:rotate(0)}20%,60%{transform:rotate(-25deg)}40%,80%{transform:rotate(10deg)}}@media (max-width:500px){.github-corner:hover .octo-arm{animation:none}.github-corner .octo-arm{animation:octocat-wave 560ms ease-in-out}}</style>
```
### 跳动的心

打开`Blog/themes/next/layout/_partials/footer.swig`搜索`with-love`
替换


### 修改超链接颜色
路径
`themes\next\source\css\_common\components\post\post.styl`
一个超级粉嫩的颜色`#ff4081;`
```css
// 文章内链接文本样式
.post-body p a{
  //color: #0593d3; //原始链接颜色
  border-bottom: none;
  border-bottom: 1px solid;// #0593d3; //底部分割线颜色
  &:hover {
    color: #ff4081; //鼠标经过颜色
    border-bottom: none;
    border-bottom: 1px solid #ff4081; //底部分割线颜色
  }
}
```
### 修改代码块颜色
路径
`themes\next\source\css\_custom\custom.styl`
冲
```css
// Custom styles.
code {
    color: #ff4081;
    background: #f3f3f3;
    margin: 2px;
}
```

### gitalk
[学习大佬操作](https://asdfv1929.github.io/2018/01/20/gitalk/)

#### gitalk.swig
新建`/layout/_third-party/comments/gitalk.swig`文件，并添加内容：
```html
{% if page.comments && theme.gitalk.enable %}
  <link rel="stylesheet" href="https://unpkg.com/gitalk/dist/gitalk.css">

  <script src="https://unpkg.com/gitalk/dist/gitalk.min.js"></script>
   <script type="text/javascript">
        var gitalk = new Gitalk({
          clientID: '{{ theme.gitalk.ClientID }}',
          clientSecret: '{{ theme.gitalk.ClientSecret }}',
          repo: '{{ theme.gitalk.repo }}',
          owner: '{{ theme.gitalk.githubID }}',
          admin: ['{{ theme.gitalk.adminUser }}'],
          id: location.pathname,
          distractionFreeMode: '{{ theme.gitalk.distractionFreeMode }}'
        })
        gitalk.render('gitalk-container')           
       </script>
{% endif %}
```

#### comments.swig
修改`/layout/_partials/comments.swig`，添加内容如下，与前面的elseif同一级别上：
```html
{% elseif theme.gitalk.enable %}
 <div id="gitalk-container"></div>
```

#### index.swig
修改`layout/_third-party/comments/index.swig`，在最后一行添加内容：
```html
{% include 'gitalk.swig' %}
```

#### gitalk.styl
新建`/source/css/_common/components/third-party/gitalk.styl`文件，添加内容：
```css
.gt-header a, .gt-comments a, .gt-popup a
  border-bottom: none;
.gt-container .gt-popup .gt-action.is--active:before
  top: 0.7em;
```
#### third-party.styl
修改`/source/css/_common/components/third-party/third-party.styl`，在最后一行上添加内容，引入样式：
```css
@import "gitalk";
```

#### _config.yml
在主题配置文件next/_config.yml中添加如下内容：
```yml
gitalk:
  enable: true
  githubID: github帐号  # 例：mobenw
  repo: 仓库名称   # mobenw.github.io
  ClientID: Client ID
  ClientSecret: Client Secret
  adminUser: github帐号 #指定可初始化评论账户
  distractionFreeMode: true
```


### 修改底部标签样式
修改`Blog\themes\next\layout\_macro\post.swig`中文件
查找`rel="tag">#`
将#替换成`<i class="fa fa-tag"></i>`输入以下命令

### 站内搜索
local_search

`npm install hexo-generator-searchdb --save`

站点配置文件 添加
```yml
# 本地搜索
search:
  path: search.xml
  field: post
  format: html
  limit: 10000
```

主题配置文件 开启 `enable: ture`

### 点击有小爱心
#### 创建一个js文件
在`\themes\next\source\js\src`下新建文件**clicklove.js** 
代码如下：

```JavaScript
! function (e, t, a) {
    function n() {
        c(".heart{width: 10px;height: 10px;position: fixed;background: #f00;transform: rotate(45deg);-webkit-transform: rotate(45deg);-moz-transform: rotate(45deg);}.heart:after,.heart:before{content: '';width: inherit;height: inherit;background: inherit;border-radius: 50%;-webkit-border-radius: 50%;-moz-border-radius: 50%;position: fixed;}.heart:after{top: -5px;}.heart:before{left: -5px;}"), o(), r()
    }
    function r() {
        for (var e = 0; e < d.length; e++) d[e].alpha <= 0 ? (t.body.removeChild(d[e].el), d.splice(e, 1)) : (d[e].y--, d[e].scale += .004, d[e].alpha -= .013, d[e].el.style.cssText = "left:" + d[e].x + "px;top:" + d[e].y + "px;opacity:" + d[e].alpha + ";transform:scale(" + d[e].scale + "," + d[e].scale + ") rotate(45deg);background:" + d[e].color + ";z-index:99999");
        requestAnimationFrame(r)
    }
    function o() {
        var t = "function" == typeof e.onclick && e.onclick;
        e.onclick = function (e) {
            t && t(), i(e)
        }
    }
    function i(e) {
        var a = t.createElement("div");
        a.className = "heart", d.push({
            el: a,
            x: e.clientX - 5,
            y: e.clientY - 5,
            scale: 1,
            alpha: 1,
            color: s()
        }), t.body.appendChild(a)
    }
    function c(e) {
        var a = t.createElement("style");
        a.type = "text/css";
        try {
            a.appendChild(t.createTextNode(e))
        } catch (t) {
            a.styleSheet.cssText = e
        }
        t.getElementsByTagName("head")[0].appendChild(a)
    }
    function s() {
        return "rgb(" + ~~ (255 * Math.random()) + "," + ~~ (255 * Math.random()) + "," + ~~ (255 * Math.random()) + ")"
    }
    var d = [];
    e.requestAnimationFrame = function () {
        return e.requestAnimationFrame || e.webkitRequestAnimationFrame || e.mozRequestAnimationFrame || e.oRequestAnimationFrame || e.msRequestAnimationFrame || function (e) {
            setTimeout(e, 1e3 / 60)
        }
    }(), n()
}(window, document);
```

#### 修改_layout.swig
在`\themes\next\layout\_layout.swig`文件末尾添加以下代码(纳闷了 为啥放哪都行 神奇的script 不过建议放后面 不然有bug)
```JavaScript
<!-- 页面点击小红心 -->
<script type="text/javascript" src="/js/src/clicklove.js"></script>
```

### 点击有爆炸效果
#### 创建一个js文件
同上
**fireworks.js**
```JavaScript
"use strict";
function updateCoords(e) {
    pointerX = (e.clientX || e.touches[0].clientX) - canvasEl.getBoundingClientRect().left,
    pointerY = e.clientY || e.touches[0].clientY - canvasEl.getBoundingClientRect().top
}
function setParticuleDirection(e) {
    var t = anime.random(0, 360) * Math.PI / 180,
    a = anime.random(50, 180),
    n = [ - 1, 1][anime.random(0, 1)] * a;
    return {
        x: e.x + n * Math.cos(t),
        y: e.y + n * Math.sin(t)
    }
}
function createParticule(e, t) {
    var a = {};
    return a.x = e,
    a.y = t,
    a.color = colors[anime.random(0, colors.length - 1)],
    a.radius = anime.random(16, 32),
    a.endPos = setParticuleDirection(a),
    a.draw = function() {
        ctx.beginPath(),
        ctx.arc(a.x, a.y, a.radius, 0, 2 * Math.PI, !0),
        ctx.fillStyle = a.color,
        ctx.fill()
    },
    a
}
function createCircle(e, t) {
    var a = {};
    return a.x = e,
    a.y = t,
    a.color = "#F00",
    a.radius = 0.1,
    a.alpha = 0.5,
    a.lineWidth = 6,
    a.draw = function() {
        ctx.globalAlpha = a.alpha,
        ctx.beginPath(),
        ctx.arc(a.x, a.y, a.radius, 0, 2 * Math.PI, !0),
        ctx.lineWidth = a.lineWidth,
        ctx.strokeStyle = a.color,
        ctx.stroke(),
        ctx.globalAlpha = 1
    },
    a
}
function renderParticule(e) {
    for (var t = 0; t < e.animatables.length; t++) {
        e.animatables[t].target.draw()
    }
}
function animateParticules(e, t) {
    for (var a = createCircle(e, t), n = [], i = 0; i < numberOfParticules; i++) {
        n.push(createParticule(e, t))
    }
    anime.timeline().add({
        targets: n,
        x: function(e) {
            return e.endPos.x
        },
        y: function(e) {
            return e.endPos.y
        },
        radius: 0.1,
        duration: anime.random(1200, 1800),
        easing: "easeOutExpo",
        update: renderParticule
    }).add({
        targets: a,
        radius: anime.random(80, 160),
        lineWidth: 0,
        alpha: {
            value: 0,
            easing: "linear",
            duration: anime.random(600, 800)
        },
        duration: anime.random(1200, 1800),
        easing: "easeOutExpo",
        update: renderParticule,
        offset: 0
    })
}
function debounce(e, t) {
    var a;
    return function() {
        var n = this,
        i = arguments;
        clearTimeout(a),
        a = setTimeout(function() {
            e.apply(n, i)
        },
        t)
    }
}
var canvasEl = document.querySelector(".fireworks");
if (canvasEl) {
    var ctx = canvasEl.getContext("2d"),
    numberOfParticules = 30,
    pointerX = 0,
    pointerY = 0,
    tap = "mousedown",
    colors = ["#FF1461", "#18FF92", "#5A87FF", "#FBF38C"],
    setCanvasSize = debounce(function() {
        canvasEl.width = 2 * window.innerWidth,
        canvasEl.height = 2 * window.innerHeight,
        canvasEl.style.width = window.innerWidth + "px",
        canvasEl.style.height = window.innerHeight + "px",
        canvasEl.getContext("2d").scale(2, 2)
    },
    500),
    render = anime({
        duration: 1 / 0,
        update: function() {
            ctx.clearRect(0, 0, canvasEl.width, canvasEl.height)
        }
    });
    document.addEventListener(tap,
    function(e) {
        "sidebar" !== e.target.id && "toggle-sidebar" !== e.target.id && "A" !== e.target.nodeName && "IMG" !== e.target.nodeName && (render.play(), updateCoords(e), animateParticules(pointerX, pointerY))
    },
    !1),
    setCanvasSize(),
    window.addEventListener("resize", setCanvasSize, !1)
}
"use strict";
function updateCoords(e) {
    pointerX = (e.clientX || e.touches[0].clientX) - canvasEl.getBoundingClientRect().left,
    pointerY = e.clientY || e.touches[0].clientY - canvasEl.getBoundingClientRect().top
}
function setParticuleDirection(e) {
    var t = anime.random(0, 360) * Math.PI / 180,
    a = anime.random(50, 180),
    n = [ - 1, 1][anime.random(0, 1)] * a;
    return {
        x: e.x + n * Math.cos(t),
        y: e.y + n * Math.sin(t)
    }
}
function createParticule(e, t) {
    var a = {};
    return a.x = e,
    a.y = t,
    a.color = colors[anime.random(0, colors.length - 1)],
    a.radius = anime.random(16, 32),
    a.endPos = setParticuleDirection(a),
    a.draw = function() {
        ctx.beginPath(),
        ctx.arc(a.x, a.y, a.radius, 0, 2 * Math.PI, !0),
        ctx.fillStyle = a.color,
        ctx.fill()
    },
    a
}
function createCircle(e, t) {
    var a = {};
    return a.x = e,
    a.y = t,
    a.color = "#F00",
    a.radius = 0.1,
    a.alpha = 0.5,
    a.lineWidth = 6,
    a.draw = function() {
        ctx.globalAlpha = a.alpha,
        ctx.beginPath(),
        ctx.arc(a.x, a.y, a.radius, 0, 2 * Math.PI, !0),
        ctx.lineWidth = a.lineWidth,
        ctx.strokeStyle = a.color,
        ctx.stroke(),
        ctx.globalAlpha = 1
    },
    a
}
function renderParticule(e) {
    for (var t = 0; t < e.animatables.length; t++) {
        e.animatables[t].target.draw()
    }
}
function animateParticules(e, t) {
    for (var a = createCircle(e, t), n = [], i = 0; i < numberOfParticules; i++) {
        n.push(createParticule(e, t))
    }
    anime.timeline().add({
        targets: n,
        x: function(e) {
            return e.endPos.x
        },
        y: function(e) {
            return e.endPos.y
        },
        radius: 0.1,
        duration: anime.random(1200, 1800),
        easing: "easeOutExpo",
        update: renderParticule
    }).add({
        targets: a,
        radius: anime.random(80, 160),
        lineWidth: 0,
        alpha: {
            value: 0,
            easing: "linear",
            duration: anime.random(600, 800)
        },
        duration: anime.random(1200, 1800),
        easing: "easeOutExpo",
        update: renderParticule,
        offset: 0
    })
}
function debounce(e, t) {
    var a;
    return function() {
        var n = this,
        i = arguments;
        clearTimeout(a),
        a = setTimeout(function() {
            e.apply(n, i)
        },
        t)
    }
}
var canvasEl = document.querySelector(".fireworks");
if (canvasEl) {
    var ctx = canvasEl.getContext("2d"),
    numberOfParticules = 30,
    pointerX = 0,
    pointerY = 0,
    tap = "mousedown",
    colors = ["#FF1461", "#18FF92", "#5A87FF", "#FBF38C"],
    setCanvasSize = debounce(function() {
        canvasEl.width = 2 * window.innerWidth,
        canvasEl.height = 2 * window.innerHeight,
        canvasEl.style.width = window.innerWidth + "px",
        canvasEl.style.height = window.innerHeight + "px",
        canvasEl.getContext("2d").scale(2, 2)
    },
    500),
    render = anime({
        duration: 1 / 0,
        update: function() {
            ctx.clearRect(0, 0, canvasEl.width, canvasEl.height)
        }
    });
    document.addEventListener(tap,
    function(e) {
        "sidebar" !== e.target.id && "toggle-sidebar" !== e.target.id && "A" !== e.target.nodeName && "IMG" !== e.target.nodeName && (render.play(), updateCoords(e), animateParticules(pointerX, pointerY))
    },
    !1),
    setCanvasSize(),
    window.addEventListener("resize", setCanvasSize, !1)
};
```
#### 修改_layout.swig
同上
```JavaScript
{% if theme.fireworks %}
   <canvas class="fireworks" style="position: fixed;left: 0;top: 0;z-index: 1; pointer-events: none;" ></canvas> 
   <script type="text/javascript" src="//cdn.bootcss.com/animejs/2.2.0/anime.min.js"></script> 
   <script type="text/javascript" src="/js/src/fireworks.js"></script>
{% endif %}
```
#### 主题配置
路径`\themes\next\_config.yml`
```
# Fireworks
fireworks: true
```

### 新建404界面
在站点根目录下,输入 `hexo new page 404` ,默认在 Hexo 站点下`/source/404/index.md`
打开新建的`404界面`，在顶部插入一行，写上 `permalink: /404` ，这表示指定该页固定链接为 http://"主页"/404.html。
```
---
title: #404 Not Found：该页无法显示
date: 2017-09-06 15:37:18
comments: false
permalink: /404
---
```

如果你不想编辑属于自己的404界面,可以显示腾讯公益404界面,代码如下：
```html
<!DOCTYPE HTML>
<html>
<head>
  <meta http-equiv="content-type" content="text/html;charset=utf-8;"/>
  <meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1" />
  <meta name="robots" content="all" />
  <meta name="robots" content="index,follow"/>
  <link rel="stylesheet" type="text/css" href="https://qzone.qq.com/gy/404/style/404style.css">
</head>
<body>
  <script type="text/plain" src="http://www.qq.com/404/search_children.js"
          charset="utf-8" homePageUrl="/"
          homePageName="回到我的主页">
  </script>
  <script src="https://qzone.qq.com/gy/404/data.js" charset="utf-8"></script>
  <script src="https://qzone.qq.com/gy/404/page.js" charset="utf-8"></script>
</body>
</html>
```
### 内容自适应
>在`Gemini`主题中没有进行配置

```styl
// 修改成你期望的宽度
$content-desktop = 920px

// 当视窗超过 1600px 后的宽度
$content-desktop-large = 920px
```
>700px，当屏幕宽度 < 1600px
>900px，当屏幕宽度 >= 1600px
>移动设备下，宽度自适应



### 提升加载速度
>好像在最新的配置中没用上

主题的配置文件`_config.yml`
```yml
# Internal version: 1.2.1
# See: http://VelocityJS.org
velocity: #//cdn.jsdelivr.net/velocity/1.2.3/velocity.min.js


# Internal version: 4.6.2
# See: http://fontawesome.io/
fontawesome: #//maxcdn.bootstrapcdn.com/font-awesome/4.7.0/css/font-awesome.min.css
```


