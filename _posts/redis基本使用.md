---
layout: post
title: "A quick demo of Simple Texture theme's code highlighting features"
description: "A quick demo of Simple Texture theme's code highlighting features"
categories: [demo]
tags: [demo, jekyll]
redirect_from:
  - /2017/05/27/
---



# redis基本使用



## redis安装，启动，及基本命令

### docker安装，启动redis

[docker安装redis连接](https://www.runoob.com/docker/docker-install-redis.html)

1. 拉取镜像：$ docker pull redis:latest

2. 运行容器：$ docker run -itd --name redis-test -p 6379:6379 redis

3. 查看镜像：$ docker images

4. 查看运行容器：$ docker ps

5. 进入容器：$ docker exec -it redis-test /bin/bash

   

### redis基本操作

* keys
  * keys pattern 展示符合规则的key
* del 删除key
* exists 
  * exists key 检查是否存在key
* expire 设置key过期时间
  * ttl 查看key过期时间
  * persist key 清除key过期时间
* rename
* type 查看key的数据类型

## redis客户端使用



### redis-cli客户端



### jedis客户端



## redis数据类型及基本使用

> redis可以定义5中数据类型（待定）

* String（字符类型）
* Hash（散列类型）
* List（列表类型）
* Set（集合类型）
* SortedSet（有序集合类型）

> 注意：在 redis 中的命令语句中，命令是忽略大小写的，而 key 是不忽略大小写的。

### string

* 赋值

  * SET KEY

* 取值

  * GET KEY

* 取值并赋值

  * GETSET KEY VALUE

* 数值增减

  * 递增
    * INCR KEY
  * 增加指定值
    * INCRBY KEY INCREMENT
  * 递减
    * DECR KEY
  * 减少指定值
    * DECRBY KEY DECREMENT

* 不存在时赋值

  * SETNX KEY VALUE

    > 分布式锁应用

* 其他命令

  * 尾部追加
    * APPEND KEY VALUE
  * 获取字符串长度
    * STRLEN KEY
  * 同时获取/设置多个键值
    * MSET  KEY1 VALUE1 KEY2 VALUE2 ...
    * MGET  KEY1 KEY2 ...

* 应用场景

  * 自增主键

### hash

* hset 设置一个字段

* hmset 设置多个字段

* hsetnx 当字段不存在即设置

  * > 查看该情况的使用场景

* hget 获取一个字段

* hmget 获取多个字段

* hgetall 获取全部字段

* hdel 删除字段

* hincrby 增加数字

* 应用场景

  * 存储商品信息

### list

* LPUSH/RPUSH 添加列表元素

* LRANGE 返回列表元素

  * > 索引从 0 开始，可以是负数， -1代表最后边的一个元素

* LPOP/RPOP 从两边弹出元素

* LLEN 返回列表元素个数

* 应用场景

  * 商品评论列表

### set

> 集合类型，数据不重复且没有顺序。通过散列表实现，操作复杂度都是O(1)

* SADD/SREM 增加一个集合元素
* SMEMBERS 展示全部集合元素
* SISMEMBER 查看元素是否在集合中
* 集合运算
  * SDIFF 差集
  * SINTER 交集
  * SUNION 并集
* 应用场景

### zset

> 有序集合，通过增加元素分数来实现元素的有序性，和列表相似，但是和列表实现底层不同。
>
> 操作复杂度对比链表较低，尤其是对集合中部的操作。
>
> 但是内存占用相比列表要高。

* ZADD/ZREM 增加元素
* ZRANGE/ZREVRANGE  按分数从小到大返回元素/从大到小
* ZSCORE 显示每个元素的分数
* 应用场景
  * 商品销售排行榜

## redis应用场景

### 消息

#### 消息队列

利用列表操作LPUSH RPOP,RPOP可以使用BRPOP代替，BRPOP为弹出队列时如果没有元素的话就阻塞，等有元素添加时再弹出

#### 发布订阅

redis有单独命令支持发布订阅的消息功能，但是其不如很多专业的消息中间件有更高的可靠性解决方案，redis不支持消息重复读（？），不支持回滚等。

### 分布式锁



### 缓存



## redis事务

待补充



## redis进阶

### redis内存模型

### redis数据结构

### redis缓存淘汰策略

### redis事务

#### 事务典型应用--redis乐观锁

##### 乐观锁实现秒杀



