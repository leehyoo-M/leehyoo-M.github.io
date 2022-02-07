---
title: Spring源码解析（一）
date: 2022-01-05 15:33:31
tags: [spring,core,java,IOC]
---

IOC 控制反转 把对象创建和对象之间的调用购过程，交给spring管理
FactoryBean： 所有的bean都是有beanfactory进行管理，一个能生产或者修饰对象生成的工厂bean
BeanFactory： IOC容器或者对象工厂


IOC思想基于IOC容器完成，IOC容器底层就是对象工厂
spring提供ioc容器实现的两种方式
1. beanfactory：ioc容器基本实现，是spring内部接口，不提供开发人员进行使用。加载配置文件时候不会创建对象，在获取对象（使用）采取创建对象（懒汉模式）
2. applicationcontext：beanFactory子接口，提供更多的功能，一般由开发人员进行使用。加载配置文件时就会创建对象 饿汉模式

----
IOC容器初始化过程：cccc
1. resource定位过程
org.springframework.context.support.AbstractApplicationContext#refresh
org.springframework.context.support.AbstractRefreshableApplicationContext#refreshBeanFactory

org.springframework.web.context.support.XmlWebApplicationContext#loadBeanDefinitions(org.springframework.beans.factory.support.DefaultListableBeanFactory)

org.springframework.beans.factory.support.AbstractBeanDefinitionReader#loadBeanDefinitions(java.lang.String, java.util.Set<org.springframework.core.io.Resource>)


2. BeanDefinition的载入

载入的过程就是把定义的beandefinition在ioc容器中转换为一个spring内部表示的数据结构的过程。

IOC容器对bean的管理和依赖注入功能的实现，是通过对其持有的beandefinition进行各种相关操作完成的。这些beandefinition数据在ioc容器中通过一个hashmap来维护，如果需要提高ioc容器的新能和容量，完全可以自己做一些扩展



3. 向IOC容器注册这些BeanDefinition的过程

·crisp