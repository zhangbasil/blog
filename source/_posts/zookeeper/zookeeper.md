---
title: mysql8.0 Public Key Retrieval is not allowed
categories: 
    - 中间件
tags: 
    - zookeeper
---

### 启动
```
./bin/zkServer.sh start
```
### 查看启动日志
启动日志在安装的logs下面
```
cat logs/zookeeper-admin-server-admin.out
```

### 配置文件
* clientPort=2181  端口
* dataDir=/temp/data 存储文件路径

### zkCli 操作

#### 进入客户端
```
./bin/zkCli.sh
```
#### 递归查看节点
```
ls -R /
```

