---
title: Docker相关命令
categories: 
    - 容器
tags: 
    - Docker
---

## 进入

### 进入容器终端
``` bash
docker exec -it 9197d61a519f bash

docker exec -it [container] sh
```

## 启动

### docker 启动容器
```
docker start <CONTAINER ID>
```
### docker 停止容器
```
docker stop <CONTAINER ID>
```

### docker重启容器自动启动
```bash
docker update --restart=always <CONTAINER ID>
```


## 查看

### 查看正在运行的容器
``` bash
docker ps
```
### 查看容器信息
```bash
docker inspect redis 
```
### 查看容器ip地址
```
docker inspect --format='{{.NetworkSettings.IPAddress}}' redis
```
### 查看容器ip地址
```
docker inspect --format '{{.Name}} {{.State.Running}}' redis
```
### 查看日志
```bash
docker logs redis
docker logs -f -t --since="2019-05-31" --tail=100 redis
```
#### 命令分解
docker logs \
-f \ 查看实时日志
-t \ 查看日志产生的日期
--since="2019-05-31" \ 此参数指定了输出日志开始日期，即只输出指定日期之后的日志
--tail=100 \ 查看最后的100条日志。
redis

### 查看进程信息
```bash
docker top redis
```
### 查看端口
```bash
docker port redis
```


## 删除

### 删除所有停止的容器
``` bash
docker container prune
```



