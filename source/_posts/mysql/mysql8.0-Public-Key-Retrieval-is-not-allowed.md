---
title: mysql8.0 Public Key Retrieval is not allowed
categories: 
    - 数据库
tags: 
    - mysql
    - UnableToConnectException
---

### 背景&重现

本地开发环境Mysql服务是放在容器docker里面，启动本地项目有时候会发现数据库链接异常如下：

```
Caused by: com.mysql.cj.exceptions.UnableToConnectException: Public Key Retrieval is not allowed
```

经过几次的观察，发现只有在重启mysql服务的时候，第一次启动会有这个问题，其他的时候并没有。

### 解决方案
在连接的后面直接加上如下即可
```
AllowPublicKeyRetrieval=True
```


More info: [connection-options](https://mysqlconnector.net/connection-options/)


