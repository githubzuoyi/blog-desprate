---
layout: post
title: "A quick demo of Simple Texture theme's code highlighting features"
description: "A quick demo of Simple Texture theme's code highlighting features"
categories: [demo]
tags: [demo, jekyll]
redirect_from:
  - /2017/05/27/
---



# Spring 容器



## 提问

* spring容器是如何处理bean定义，并且控制bean的生命周期的，梳理出流程图，以及核心api
* spring容器的事件体系是怎样运作的，流程图，以及api和使用，使用了何种设计模式
* spring注入属性是如何自动类型转换的，使用了什么设计模式



## 核心API 及其关系梳理

* BeanDefinition
* BeanFactoryPostProcessor
  * 容器加工 BeanDefinition 对象，使其成为完整的bean定义
  * 加载propertyEditor相关实现类进入属性编辑器注册（PropertyEditorRegistry）
* PropertyEditor
  * 作用：将外部的设置值变为jvm的内在类型表示
    * javabeans规范定义
* BeanInfo
  * PropertyDescripter
    * 每个bean属性对应一个PropertyDescripter
  * 最重要的方法 PropertyDescripter[] getPropertyDescripters()
* BeanWrapper

## 注意点



## 问题汇总

