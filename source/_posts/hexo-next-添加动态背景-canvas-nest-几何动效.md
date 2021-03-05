---
title: hexo-next 添加动态背景 (canvas-nest 几何动效)
date: 2021-03-05 23:17:34
tags: 
  - hexo 
  - next
  - 插件
categories: hexo 循序渐进
---

首先需要去 github 上克隆 canvas-nest 项目到 themes/next/source/lib/canvas-nest 目录 (没有 canvas-nest 这个文件夹请自行创建)

[theme-next-canvas-nest](https://github.com/theme-next/theme-next-canvas-nest)

``` shell
 git clone https://github.com/theme-next/theme-next-canvas-nest source/lib/canvas-nest
```
<!-- more -->

然后在 themes/next/_config.yml 文件中添加如下代码:

``` yml
canvas_nest:
  enable: true
  onmobile: true # display on mobile or not
  color: '0,0,255' # RGB values, use ',' to separate
  opacity: 0.5 # the opacity of line: 0~1
  zIndex: -1 # z-index property of the background
  count: 99 # the number of lines
```

接着更新

``` shell
cd themes/next/source/lib/canvas-nest
git pull
```

重新构建一下大功告成!
