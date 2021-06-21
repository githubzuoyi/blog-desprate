---
layout: post
title: "spring boot 自动装配原理详解"
description: "spring boot自动装配原理实践及相关实现"
categories: [Spring-Boot]
tags: [Spring-Boot]
redirect_from:
  - /2021/06/21/
---



# spring boot 自动装配原理详解



>版本信息：
>
>OS : windows 10 （×64）
>
>JDK : 1.8
>
>spring boot : 1.5.19.RELEASE



## 内容概览

* demo展示
* 原理分析
  * 核心组件
  * 自动装配流程
* 自定义自动装配实现
  * mybatis starter 自动装配
  * 开发技巧
  * 扩展点分析
* 业界实现
  * redis 自动装配
  * mvc 自动装配





## demo







## 原理分析

### Enable模块驱动  

#### 核心API

* @Import
* org.springframework.context.annotation.ImportSelector
* org.springframework.context.annotation.ConfigurationClassParser



#### spring 注解驱动编程原理分析

> 在 spring framework 中，如果将组件 component 注入到容器中，需要使用 import 或 componentScan 组件。

* org.springframework.context.annotation.ConfigurationClassParser#processImports()
  * org.springframework.context.annotation.ImportSelector#selectImports(AnnotationMetadata)
    * org.springframework.context.annotation.ConfigurationClassParser#processImports()



#### 时序图





### 自动装配类加载



#### 核心API

* @EnableAutoConfiguration
  * org.springframework.boot.autoconfigure.EnableAutoConfigurationImportSelector
  * spring.factories
* org.springframework.core.io.support.SpringFactoriesLoader
  * spring.factories 的 加载类



* **自动配置类（EnableAutoConfiguration）的加载逻辑**

  * @org.springframework.boot.autoconfigure.EnableAutoConfiguration

    * org.springframework.boot.autoconfigure.AutoConfigurationImportSelector#selectImports(AnnotationMetadata)

      * org.springframework.boot.autoconfigure.AutoConfigurationImportSelector#getCandidateConfigurations()

        > `getCandidateConfigurations()`方法不是最终的自动装配类信息，后面还有去重，排序，黑名单过滤等步骤

        * org.springframework.boot.autoconfigure.AutoConfigurationImportSelector#getSpringFactoriesLoaderFactoryClass() // 加载自动配置类 EnableAutoConfiguration.class 的子类信息
          * org.springframework.core.io.support.SpringFactoriesLoader#loadFactoryNames() // 加载 spring.factories  的自动装配类信息，返回自动装配类 list 列表
            * org.springframework.context.annotation.ConfigurationClassParser#processImports(ConfigurationClass,SourceClass,Collection<SourceClass>,boolean)



加载流程图



#### 自动装配类 生命周期 解析



### 自动装配加载

* XXXAutoConfiguration
* @Conditional 条件装配注解（表格输出）
* @EnableConfigurationProperties
* @ConfigurationProperties



* **自动配置类（XXXAutoConfiguration）的加载逻辑**

  > 以 RedisAutoConfiguration 为例

  * RedisAutoConfiguration 
    * @ConditionalOnClass({ JedisConnection.class, RedisOperations.class, Jedis.class }) // 根据条件化配置判断是否加载自动化配置
      * @EnableConfigurationProperties(RedisProperties.class) // 启用配置属性信息
        * @ConfigurationProperties(prefix = "spring.redis") // 加载配置文件中 spenfix 为 spring.redis 的属性
          * RedisConnectionConfiguration(RedisProperties,ObjectProvider<RedisSentinelConfiguration>,ObjectProvider<RedisClusterConfiguration>) // 加载redis连接池配置类
            * org.springframework.data.redis.connection.jedis.JedisConnectionFactory // 注册 JedisConnectionFactory  bean
              * RedisConfiguration // 加载 redis 配置类
                * RedisTemplate // 条件注册 RedisTemplate bean
                  * StringRedisTemplate // 条件注册 StringRedisTemplate bean





### 相关知识点

#### ConfigurationClassParser -- ImportSelector 加载



#### ObjectProvider 延迟加载



#### SpringFactoriesLoader -- spring.factories 信息加载



#### @EnableConfigurationProperties 与 @ConfigurationProperties 注解处理

* @ConfigurationProperties 是如何将配置文件属性映射到 类属性中的？类型转换是如何做的？
* @EnableConfigurationProperties 是如何启用属性配置的





## 自定义自动装配类



### 开发步骤

* 包名与定义
* 条件装配
* bean加载
* 配置信息加载







### Mybatis 自动装配 starter 实现





### dubbo 自动装配 starter 实现





## spring boot starter 核心起步依赖



### spring-boot-starter-web





### spring-boot-starter-jdbc

