# MoBenw.github.io
我的博客

## 个人使用

### 本地浏览使用

`hexo g && hexo s`

>hexo g 生成
>hexo s 启动服务预览

### 部署到GitHub

`hexo clean && hexo g && hexo d`

>hexo clean 清理缓存
>hexo g 生成
>hexo d 部署

# 使用到的插件及指令

## 安装Hexo
`npm install -g hexo`

## 自动部署工具

`npm install hexo-deployer-git  --save`

## 文章计数插件
`npm i --save hexo-wordcount`

## 优化工具

```
npm install gulp -g
npm install gulp-minify-css gulp-uglify gulp-htmlmin gulp-htmlclean gulp --save
```

## 上传本地图片插件

`npm install hexo-asset-image --save`

## 站内搜索功能

local_search
`npm install hexo-generator-searchdb --save`