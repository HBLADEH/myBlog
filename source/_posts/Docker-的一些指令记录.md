---
title: Docker 的一些指令记录
date: 2021-05-18 23:37:31
tags: 
  - Docker
  - 指令
---

有些指令啊，经常忘记哈哈哈哈。干脆直接记在这里吧！！！

## 启动 nginx 和挂载

``` shell
  docker run -d -p 80:80 --name nginx-web -v ~/nginx/www:/usr/share/nginx/html -v ~/nginx/conf/nginx.conf:/etc/nginx/nginx.conf -v ~/nginx/logs:/var/log/nginx nginx
```

## nginx 配置代理

``` shell
  location / {
           proxy_ignore_client_abort on;
            root   /usr/share/nginx/html;
            index  index.html;
        }
    location ^~ /api/ {
        proxy_pass http://121.4.162.86:8081;
        proxy_set_header Host $host:$server_port;
    }

```
