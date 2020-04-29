---
title: nginx相关操作
categories: 
    - 服务器
tags: 
    - nginx
---

### 链接

#### Nginx 客户端命令
```bash
$ docker run -d -v $PWD/nginx.conf:/etc/nginx/nginx.conf nginx

docker run -p 80:80 -v $PWD/nginx.conf:/etc/nginx/nginx.conf -e TZ=Asia/Shanghai --name nginx -d nginx:stable-alpine
```

### Docker
```
docker run \
-p 80:80 \
-v $PWD/nginx.conf:/etc/nginx/nginx.conf \
-v $PWD/html:/usr/share/nginx/html \
-e TZ=Asia/Shanghai \
--name nginx \
-d nginx:stable-alpine
```
