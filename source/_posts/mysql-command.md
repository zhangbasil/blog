---
title: mysql相关操作
categories: 
    - DB
tags: 
    - mysql
    - docker
---

### 链接

#### mysql 客户端命令
```bash
mysql -u root -p
```

### Docker
```
docker run \
-p 3306:3306 \
-v $PWD/mysql/conf.d:/etc/mysql/conf.d \
-v $PWD/mysql/data:/var/lib/mysql \
-e MYSQL_ROOT_PASSWORD=root \
--name mysql \
-d mysql:8.0 \
--character-set-server=utf8mb4 --collation-server=utf8mb4_unicode_ci
```