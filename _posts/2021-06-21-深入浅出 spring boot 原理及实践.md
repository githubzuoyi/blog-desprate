---
layout: post
title: "深入浅出 spring boot 原理及实践"
description: "spring boot starter 概览，自动装配相关原理，及业界实现"
categories: [Spring-Boot]
tags: [Spring-Boot]
redirect_from:
  - /2021/06/21/
---


## 深入浅出 spring boot 原理及实践


* eric table of contents
{:toc .toc}


### 学习要求

* 理解 spring boot 相关原理
  * 自动装配
    * enabled 注解驱动开发
  * 内置Servlet容器
  * 生产级框架
* 实现第三方 spring boot starter
  - [ ] mybatis
  - [ ] redis
  - [ ] spring boot dubbo starter
  - [ ] spring mvc
* 深入理解业界相关实现
  * spring mvc
  * spring boot dubbo starter
  * spring cloud





### 基础概览



#### spring boot 是什么？不是什么？（结合 官方网站 及 自己的理解，从架构方面，软件架构发展方面）



#### spring boot 的核心特性 及 理解

* 起步依赖

* 自动装配
* 内嵌容器
* 生产级可用



#### spring boot 核心组件解析

* org.springframework.boot.context.properties.EnableConfigurationProperties
  * 启动配置组件
  * 关联组件
    * org.springframework.context.annotation.ImportBeanDefinitionRegistrar
      * org.springframework.boot.context.properties.EnableConfigurationPropertiesRegistrar
        * 注入处理器



#### spring boot 起步依赖

##### 起步依赖的使用 及 优劣分析





#### spring boot 自动装配原理解析



##### demo



##### 相关注解含义（表格呈现）

* 条件化注解

| 注解类型                        | 注解生效                                                     | 主要的使用场景 |
| ------------------------------- | ------------------------------------------------------------ | -------------- |
| @ConditionalOnBean              | 配置了某个特定Bean                                           |                |
| @ConditionalOnMissingBean       | 没有配置特定的Bean                                           |                |
| @ConditionalOnClass             | Classpath里有指定的类                                        |                |
| @ConditionalOnMissingClass      | Classpath里缺少指定的类                                      |                |
| @ConditionalOnExpression        | 给定的Spring Expression Language（SpEL）表达式计算结果为true |                |
| @ConditionalOnJava              | Java的版本匹配特定值或者一个范围值                           |                |
| @ConditionalOnJndi              | 参数中给定的JNDI位置必须存在一个，如果没有给参数，则要有JNDI InitialContext |                |
| @ConditionalOnProperty          | 指定的配置属性要有一个明确的值                               |                |
| @ConditionalOnResource          | Classpath里有指定的资源                                      |                |
| @ConditionalOnWebApplication    | 这是一个Web应用程序                                          |                |
| @ConditionalOnNotWebApplication | 这不是一个Web应用程序                                        |                |

* 其他注解

| 注解类型                       | 注解作用       | 使用场景 |
| ------------------------------ | -------------- | -------- |
| @EnableConfigurationProperties | 启动配置？     |          |
| @ConfigurationProperties       | 配置映射？     |          |
| @Configuration                 | 配置点加载？   |          |
| @Import                        | 配置文件导入？ |          |



##### 条件装配

* version > spring 4.0
* 核心注解
  * Conditional
* 核心接口
  * Condition



##### 自动装配启动过程



##### 注解驱动编程

* @EnableConfigurationProperties



##### 疑问点梳理

* @ConfigurationProperties 是如何映射属性的？这些属性又是如何被加载的？
  * A1:
  * A2: 映射的属性通过注解 EnableConfigurationProperties 被组件加载





#### 容器内建



#### 生产级标准







### 相关实践

#### mybatis 根据 spring boot 封装成 starter

概要：

* 包名定义规范
  * spring-boot-starter-XXX.jar
  * spring-boot-autoconfigure-XXX.jar
* 结构分析
  * 梳理与spring集成的核心api及组件
  * 最小化配置【约定大于配置】
    * 核心注解
      * @MapperScan：用于包扫描
    * 核心组件
      * org.apache.ibatis.session.SqlSessionFactory
      * org.mybatis.spring.SqlSessionTemplate
      * org.mybatis.spring.annotation.MapperScannerRegistrar
    * 包路径扫描
      * MapperScannerRegistrar 注册当前的beanfactory所在bean定义下面所有存在@Mapper注解的类



* 设计模式梳理
  * spring boot  -  configurationCustomizer:配置回调
  * org.springframework.beans.factory.ObjectProvider - 组件注入点



#### dubbo 根据 spring boot 封装成 starter

* 自动装配
  * 核心注解
  * 核心bean
* 外部化配置
  * 配置加载
* actuator
  * 运维功能加载
* 兼容性
  * 本次仅集成 2.x 版本的 dubbo



### spring boot starter 开发技巧

#### auto-configuration package

* 梳理集成所需的 最小化配置【约定大于配置】
* 条件配置分析【before，after，onclass，onname，miss。。】

* 启动加载：与spring 集成的配置的组件 转为 自动配置的组件

#### starter package

* 依赖组织

#### spring 

* 尽可能使用spring的组件，将spring boot 最小化







### 相关技术

#### maven项目管理工具

##### 依赖管理



##### 依赖传递

* 最近依赖原则



##### 覆盖/排除依赖

* 排除：Extensions
* 覆盖：最近依赖



##### 可选依赖





### 参考书目

* 《spring boot 实战（第4版）》- Craig Walls

* 《spring boot 编程思想》- 小马哥
* spring.io.com

