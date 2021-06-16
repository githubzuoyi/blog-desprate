---
layout: post
title: "A quick demo of Simple Texture theme's code highlighting features"
description: "A quick demo of Simple Texture theme's code highlighting features"
categories: [demo]
tags: [demo, jekyll]
redirect_from:
  - /2017/05/27/
---



## redis如何实现分布式锁

* 应用场景
  * redis为什么适合作为分布式锁使用
    * 分布式锁，是需要在共享存储空间对多个客户端加锁，redis本身就是一个共享存储系统，可以作为分布式锁
    * redis有较好的读写性能，适合作为分布式锁的场景
* 分布式锁需要具备的要素
  * 原子性
  * 可靠性
* redis作为分布式锁如何解决原子性和可靠性问题
  * redis单机模式
    * 使用setnx加锁，命令+lua脚本解锁
    * 怎么应对异常不释放锁的场景
    * 如何避免错误解锁的情况
  * redis集群模式
    * 分布式锁算法
      * redlock
        * 具体原理
        * 使用



* 实践
  * 加锁方式
    * setnx
    * watch
  * 客户端
    * redis-cli
    * jedis
  * redis单机分布式锁实践
  * 秒杀案例