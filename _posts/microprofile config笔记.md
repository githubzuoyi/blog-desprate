---
layout: post
title: "A quick demo of Simple Texture theme's code highlighting features"
description: "A quick demo of Simple Texture theme's code highlighting features"
categories: [demo]
tags: [demo, jekyll]
redirect_from:
  - /2017/05/27/
---



## microprofile config笔记



### 关键api

* ConfigProvider
  * 是程序化获取configuration的中心点
  * 被 ConfigProviderResolver 代理
* ConfigProviderResolver
* ConfigSource
* converter





### 配置特性

* 多值配置，通过逗号隔开，为string[] 数组

  * ``` java
    myPets=dog,cat,dog\\,cat
    
    String[] myPets = config.getValue("myPets", String[].class);
    //myPets = {"dog", "cat", "dog,cat"}
    ```

* 4种方式获取config实例

  * 通过注解@Inject注入
    * 实现者注意事项
      * 注入config实例，其行为应和ConfigProvider.getConfig()一致
      * 注入config属性值，其行为应和Config.getValue()一致
  * ConfigProvider#getConfig()
  * ConfigProvider#getConfig(ClassLoader forClassLoader)
    *  This can be used if the Thread Context ClassLoader does not represent the correct layer.
  * ConfigProviderResolver#getBuilder() .build();
    * This configuration instance will by default not be shared by the ConfigProvider.
    *  This method is intended be used if an IoC container or any other external Factory can be used to give access to a manually created shared Config. 

* 线程安全性：

  * All methods in the ConfigProvider, ConfigProviderResolver and Config implementations are thread safe and reentrant.

* 序列化

  * The Config instances created via CDI are Serializable.

* 配置元

  * 内建配置元

    * 实现注意点
      * 必须开箱即用得实现一下配置元
        * System Properties
        * Environment variables
        * META-INF/microprofile-config.properties from classpath

  * 定制配置元

    * 通过spi机制加载

    * 实现接口 org.eclipse.microprofile.config.spi.ConfigSource.

    * 动态配置元 **ConfigSourceProvider**

      * spi机制加载

      * 实现org.eclipse.microprofile.config.spi.ConfigSourceProvider.

      * example

        ```java
        public class ExampleYamlConfigSourceProvider
          implements org.eclipse.microprofile.config.spi.ConfigSourceProvider {
          @Override
          public List<ConfigSource> getConfigSources(ClassLoader forClassLoader) {
          List<ConfigSource> configSources = new ArrayList<>();
          Enumeration<URL> yamlFiles
          = forClassLoader.getResources("sampleconfig.yaml");
          while (yamlFiles.hasMoreElements()) {
          configSources.add(new SampleYamlConfigSource(yamlFiles.nextElement()));
          }
          return configSources;
          } }
        ```

* 转换器converter

  

### 设计模式

* 工厂模式
* 建造者模式







### 问题梳理

1. 实现动态配置元，并验证其动态性
2. 完善microprofile config 实现
3. 参考spring 思考，如何更好得设计converter api的非空判断