---
title: hexo + next 给博客添加新功能
date: 2020-10-01 10:10:20
tags: 
  - hexo 
  - next
  - 插件
categories: hexo 循序渐进
---
  把用到的一些插件的配置方法记录一下，免得以后忘记了。

## <a id="menu">目录</a>

>* [评论插件 Gitalk](#gitalk)
>* [添加左边菜单栏默认选项](#leftmenu)
>* [添加阅读次数](#reads)
>* [添加相关链接](#links)
>* [添加搜索](#search)

<!--more-->

## <a id="gitalk">评论插件 Gitalk</a>

首先我们需要注册一个[Github Application](https://github.com/settings/applications/new)

![图片](img1.png)

注册完成之后即可获得 Client ID 和 Client Secret

打开 themes/主题/_config.yml 加入如下配置即可

![图片](img2.png)

显示效果就在文章底部哈

[回到顶部👆](#menu)

## <a id="leftmenu">添加左边菜单栏默认选项</a>

这个简单，我用的是 next 主题，直接打开主题的 _config.yml，找到 menu 选项，解除想要使用的页面的注释即可。

![图片](img3.png)

菜单格式为 /路径/ || fontawesome 图标，可自由更换

整点效果图
![图片](img4.png)
![图片](img5.png)

[回到顶部👆](#menu)

## <a id="reads">添加阅读次数</a>

这个我还不懂能不能用，等能用了我再写嘻嘻

## <a id="links">添加相关链接</a>

添加相关链接和上面的左边菜单默认选项差不多，直接打开主题的 _config.yml，找到 social 选项如下图改就完事了

![图片](img6.png)
格式为 地址 || fontawesome 图标，可自由更换

[回到顶部👆](#menu)

## <a id="search">添加搜索</a>

要添加搜索功能就得先下 hexo-generator-searchdb

` npm install hexo-generator-searchdb --save `

接着修改 根目录的 _config.yml,在最底部加上如下配置

```js
  #Local Search
  search:
  path: search.xml
  field: post
  format: html
  limit: 10000
```

再同步修改 themes 里的 _config.yml，搜索 local_search 修改enable为true

```js
  local_search:
    enable: true
```

效果如下
![图片](img7.png)
