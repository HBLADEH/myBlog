---
title: hexo-next 设置首页和归档页的分页数量
date: 2021-03-05 13:10:31
tags: 
  - hexo 
  - next
  - 插件
categories: hexo 循序渐进
---

首先需要安装下面两个插件 (第一个是首页,第二个是归档页)

``` shell
  npm install --save hexo-generator-index
  npm install --save hexo-generator-archive
```

接着去 hexo 项目目录下的 _config.yml 文件找到并且设置下面配置

``` yml
# 首页分页
index_generator:
  path: ''
  per_page: 5 # 一页 5 篇
  order_by: -date

# 归档页面 分页
archive_generator:
  per_page: 50 # 一页 50 篇
  yearly: true
  monthly: true
```

即设置完成了哈
