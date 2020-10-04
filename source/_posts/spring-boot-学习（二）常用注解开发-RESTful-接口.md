---
title: spring boot 学习（二）常用注解开发 RESTful 接口
date: 2020-10-03 11:32:46
tags: 
  - spring-boot
  - java
categories: spring boot 学习
---
## 话不多说直接上代码

<!-- more -->

ArticleController.java

```java
  package com.pjboy.first.controller;

import com.pjboy.first.AjaxResponse;
import com.pjboy.first.model.Article;
import lombok.extern.slf4j.Slf4j;
import org.springframework.web.bind.annotation.*;

import java.util.Date;

/**
 * @program: first
 * @description:
 * @author: BLADE
 * @create: 2020-10-02 19:13
 **/
@Slf4j
@RestController
@RequestMapping("/rest")
public class ArticleController {


  /**
  * @Description: 查询一篇文章
  * @Param: [id]
  * @return: com.pjboy.first.model.Article
  * @Author: BLADE
  * @Date: 2020/10/2
  */
  //@RequestMapping(value = "/articles/{id}", method = RequestMethod.GET)
  @GetMapping("/articles/{id}")
  public AjaxResponse getArticle(@PathVariable("id") Long id) {
    Article article = Article.builder()
            .id(1L)
            .author("blade")
            .content("xixixiix")
            .createTime(new Date())
            .title("tit")
            .build();
    log.info("article:" + article);

    return AjaxResponse.success(article);
  }

  /**
   * @Description: 保存一篇文章
   * @Param: [id]
   * @return: com.pjboy.first.model.Article
   * @Author: BLADE
   * @Date: 2020/10/2
   */
  //@RequestMapping(value = "/articles/", method = RequestMethod.POST)
  @PostMapping("/articles/")
  public AjaxResponse saveArticle(@RequestBody Article article) {

    return AjaxResponse.success();
  }

  /**
   * @Description: 修改一篇文章
   * @Param: [id]
   * @return: com.pjboy.first.model.Article
   * @Author: BLADE
   * @Date: 2020/10/2
   */
  //@RequestMapping(value = "/articles/", method = RequestMethod.PUT)
  @PutMapping("/articles/")
  public AjaxResponse updateArticle(@RequestBody Article article) {

    //if (article.getId() == null) {
      //TODO 抛出一个自定义的异常
    //}

    return AjaxResponse.success();
  }

  /**
   * @Description: 删除一篇文章
   * @Param: [id]
   * @return: com.pjboy.first.model.Article
   * @Author: BLADE
   * @Date: 2020/10/2
   */
  //@RequestMapping(value = "/articles/{id}", method = RequestMethod.DELETE)
  @DeleteMapping("/articles/{id}")
  public AjaxResponse deleteArticle(@PathVariable("id") long id) {
    log.info("deleteArticle:" + id);
    return AjaxResponse.success();
  }

}
```

AjaxResponse.java

```
package com.pjboy.first;

import lombok.Data;

/**
 * @program: first
 * @description:
 * @author: BLADE
 * @create: 2020-10-02 19:19
 **/
@Data
public class AjaxResponse {
  private boolean isok;
  private int code; // 200、400、500
  private String  message;
  private Object data;
  public AjaxResponse() {

  }

  public static AjaxResponse success() {
    AjaxResponse ajaxResponse = new AjaxResponse();
    ajaxResponse.setIsok(true);
    ajaxResponse.setCode(200);
    ajaxResponse.setMessage("请求相应成功!");
    return ajaxResponse;
  }

  public static AjaxResponse success(Object obj) {
    AjaxResponse ajaxResponse = new AjaxResponse();
    ajaxResponse.setIsok(true);
    ajaxResponse.setCode(200);
    ajaxResponse.setMessage("请求相应成功!");
    ajaxResponse.setData(obj);
    return ajaxResponse;
  }
  public static AjaxResponse success(Object obj, String message) {
    AjaxResponse ajaxResponse = new AjaxResponse();
    ajaxResponse.setIsok(true);
    ajaxResponse.setCode(200);
    ajaxResponse.setMessage(message);
    ajaxResponse.setData(obj);
    return ajaxResponse;
  }

}
```
