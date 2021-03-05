---
title: Spring Boot URL 传 Date 类型无法识别和数据库无法准备比较时间问题解决
date: 2020-12-16 02:23:28
tags:
  - idea
  - spring boot
  - java 
categories: spring boot 学习
---

首先检测配置文件 application.yml 的 jackson 的设置

``` xml
    jackson:
      # 全局设置@JsonFormat的格式pattern
      date-format: yyyy-MM-dd HH:mm:ss
      # 当地时区
      locale: zh
      # 设置全局时区
      time-zone: GMT+8
```
<!-- more -->
然后在 Controller 对应 Api 处接收 Date的地方加上@DateTimeFormat

``` java
  @GetMapping("/main")
  public AjaxResponse getMainArticle(@RequestParam Long pageCurrent,
                                     @RequestParam Long pageSize,
                                     @DateTimeFormat(pattern="yyyy-MM-dd HH:mm:ss") Date news_time) {
    //Page<Article> articlePage = new Page<>(1,3,3);
    IPage<Article> articleIPage = articleService.selectArticlePage(new Page<>(pageCurrent, pageSize), news_time);
    return AjaxResponse.success(articleIPage,"获取文章信息成功");
  }
```

此时应该已经可以从前台传 Date 类型,并且后台可以识别了。
可能有些人会有数据库无法准确比较的问题，原因是数据库的时区和项目的不一致，解决方法是去 my.ini 添加默认时区

``` html
  [mysqld]
  default-time_zone = '+8:00'
```
