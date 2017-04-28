# Spring框架参考文档

# 版权相关
[spring.io](https://spring.io)
原文地址:[传送门](http://docs.spring.io/spring/docs/current/spring-framework-reference/htmlsingle/)

4.3.8.RELEASE

Copyright © 2004-2016
Copies of this document may be made for your own use and for distribution to others, provided that you do not charge any fee for such copies and further provided that each copy contains this Copyright Notice, whether distributed in print or electronically.

# 翻译
灰机

----------
#### 目录

# [一、Spring Framework 综述]()
## [1.Spring新手入门]()
## [2.Spring Framework介绍]()
### [2.1 依赖注入和控制反转]()
### [2.2 框架的那些模块]()

---------

# 第一部分. Spring Framework 综述
Spring framework是一个可以帮助你建立企业级应用的**轻量级、一站式解决方案**。并且，Spring是模块化的，所以你可以选择只引用你需要的那部分模块。你可以在任何web framework上使用IoC容器，你也可以只使用[Hibernate集成的代码]()或[JDBC抽象层]()。Spring Framework支持声明式事务管理(declarative transaction management),通过[RMI]()或[](webservice)访问你的服务，还提供多种数据持久化的方案。它还提供了“全功能”的MVC框架，并且允许你透明的集成AOP功能到你的系统中。

Spring被设计成**非侵入式的**(解耦神器),这代表你的域逻辑代码(domain logic code)通常不依赖于spring框架本身。在你的集成层(Integration layer),例如数据访问层，会存在一些数据访问技术依赖包和相关的spring依赖包。但将这些依赖隔离于你自己编写的代码库是非常easy的。

这篇文档是关于Spring framework特性的参考文档。如果你有任何疑问、建议、问题，请直接联系spring官方的联系方式，当然也可以顺便发给我一份。

* [user mailing list](https://groups.google.com/forum/#!forum/spring-framework-contrib)
* [Questions on the Framework]( https://spring.io/questions)
* 灰机的邮箱:[jianbo.fan2016@gmail.com]() 或 [736078227@qq.com]()
* 灰机的个人主页：开发中...真的在开发中，域名都买好啦!!



## 1.Spring新手入门
这段参考指南提供了关于spring framework的细节信息。它为所有特性（all features）和一些Spring包含的底层概念(如依赖注入:Dependency Injection)都提供了综合性的文档.

如果你刚开始接触Spring，你可能希望通过创建一个基于[Spring Boot](http://projects.spring.io/spring-boot/)的应用程序来开始你的Spring之旅。Spring Boot为创建基于Spring的应用(可直接用于生产)提供了非常便捷的方式(真的灰常便捷，类似grails，但个人觉得比grails要方便和强大的多)。它是基与Spring framework的，提倡**“约定大于配置”(convention over configuration)**，并且被设计成让你迅速的构建和运行你的工程(is designed to get you up and running as quickly as possible)。

## 2.Spring Framework介绍
Spring Framework 是一个为开发java应用提供综合性基础设施（infrastructure）支持的java平台（即“框架”）。因为这些基础设施由Spring Framework管理，所以开发者可以专注于应用开发。

Spring让你能通过POJOs(plain old java objects)构建应用、将企业级服务“无侵入式的”应用到POJOs中。此功能适用于Java SE全部和部分Java EE编程模型。

作为一名开发人员，举几个栗子来show一下你能通过Spring平台获得哪些益处：
* 让你在不使用transaction APIs的情况下处理数据库事务
* 不使用传统Servlet API就能方便的将你的服务以http endpoint的形式发布出去
* 无需调用繁琐的JMS API就能通过spring提供的包装后的JMS工具执行JMS动作
* 无需实现麻烦JMX API就能实现java应用管理

### 2.1 依赖注入和控制反转

传统的java应用程序——从 受限制的、嵌入式的应用程序 到 多层的、服务端的企业应用通常由互相之间有协作(耦合)关系的对象组成。因此，应用程序中的对象**彼此具有依赖关系。**

虽然java平台提供了丰富的应用程序开发功能，但它缺乏一些组织基础模块，从而形成一个连贯的整体的思想，并把这些工作留给了架构狮和程序猿。虽然你可能精通设计模式——工厂模式、抽象工厂模式、建造者模式、装饰者模式、服务定位模式(Factory, Abstract Factory, Builder, Decorator, and Service Locator),并且你用他们组成了各种类和方法。这些设计模式仅仅只是：给出一个名字，告诉你它能做什么，通常的最佳实战场景是哪里。但问题是：很多人还是不知道如何使用它们(感觉因为这需要大量的实践经验)。设计模式的最佳实践一定是根据自己正在开发的应用来完成的，所以这些模式仅仅能给出指导和参考。

Spring Framework的Ioc组件(控制反转)通过**提供将不同组件组成为一个完整的应用程序的正式的方式**来解决上面的诸多问题。Spring Framework将形式化的设计模式作为可以集成到你自己的应用程序中的first-class object。许多组织和机构都使用Spring Framework来设计**健壮的、可维护性**高的应用程序。


> **背景**
> “问题是，what aspect of control are [they] inverting？” Martin Fowler针对Ioc提出的一个问题。Fowler建议将Ioc这个名字改为DI(Dependency Injection)依赖注入

### 2.2 框架的那些模块
Spring Framework包含大约20个模块。这些模块被归为下面的几大部分：
* 核心容器（Core Container）
* 数据访问/集成(Data Access/Integration)
* Web （Web服务）
* AOP（切面编程）
* Instrumentation（***这是啥？是监控组件吗？Monitor、JMX的那些东东？***）
* Messaging（消息服务）
* Test（用于测试）

#### 图2.1.Spring Framework总览
![](https://github.com/fanjianbo/picture/blob/master/res/spring-overview.png.pagespeed.ce.XVe1noRCMt.png?raw=true)

下面的章节列出了每个功能的可用模块及其工作组件名称及其包含的主要功能。

#### 2.2.1 核心容器(Core Container)
