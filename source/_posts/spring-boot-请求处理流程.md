---
title: spring boot 请求处理流程
date: 2020-10-03 18:32:36
tags: 
  - spring-boot
  - java
categories: spring boot 学习
---
## 流程图在此

{% mermaid graph TD %}
  A[请求发送者] -->|1.发送请求| B[DispatchServlet]
  B -->|2.查找匹配Handler| C[HandlerMapping]
  B -->|3.调用适配器| D[HandlerAdapter]
  D -->|4.处理业务请求| E(Handler controller)
  D --> F(ModelAndView)
  F -->|5.返回处理结果| B
{% endmermaid %}
