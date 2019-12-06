---
title: Docker中相关Redis操作
categories: 
    - Redis
tags: 
    - Redis
---

### 链接

#### Redis 客户端命令
```bash
redis-cli -h host -p port -a password

-h 服务器地址 -p 端口号 -a 密码
```

### Docker

#### 创建并运行一个名为 `redis` 的容器
```bash
docker run \
-p 6379:6379 \
-v $PWD/data:/data \
-v $PWD/conf/redis.conf:/etc/redis/redis.conf \
--name redis \
-d redis redis-server /etc/redis/redis.conf
```
##### 命令分解
docker run \
-p 6379:6379 \ # 端口映射 宿主机:容器
-v $PWD/data:/data:rw \ # 映射数据目录 rw 为读写
-v $PWD/conf/redis.conf:/etc/redis/redis.conf:ro \ # 挂载配置文件 ro 为readonly
--privileged=true \ # 给与一些权限
--name redis \ # 给容器起个名字
-d redis:3.2 redis-server /etc/redis/redis.conf # daemon 运行容器 并使用配置文件启动容器内的 redis-server `3.2` redis的版本


#### 链接Redis客户端
```bash
docker exec -it 3a64d9068558(container_id) redis-cli
```