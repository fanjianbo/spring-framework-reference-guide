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

# [一、Spring Framework 综述](#)
## [1.Spring新手入门](#)
## [2.Spring Framework介绍](#)
### [2.1 依赖注入和控制反转](#)

### [2.2 框架的那些模块](#)
#### [2.2.1 核心容器(Core Container)](#)
#### [2.2.2 AOP和Instrumentation(实在是不知如何翻译....)](#)
#### [2.2.3 消息服务](#)
#### [2.2.4 数据访问/集成(Access/Integration)](#)
#### [2.2.5 Web](#)
#### [2.2.6 测试](#)

### [2.3 应用场景](#)
---------

# 第一部分. Spring Framework 综述
Spring framework是一个可以帮助你建立企业级应用的**轻量级、一站式解决方案**。并且，Spring是模块化的，所以你可以选择只引用你需要的那部分模块。你可以在任何web framework上使用IoC容器，你也可以只使用[Hibernate集成的代码](#)或[JDBC抽象层](#)。Spring Framework支持声明式事务管理(declarative transaction management),通过[RMI](#)或[webservice](#)访问你的服务，还提供多种数据持久化的方案。它还提供了“全功能”的MVC框架，并且允许你透明的集成AOP功能到你的系统中。

Spring被设计成**非侵入式的**(解耦神器),这代表你的域逻辑代码(domain logic code)通常不依赖于spring框架本身。在你的集成层(Integration layer),例如数据访问层，会存在一些数据访问技术依赖包和相关的spring依赖包。但将这些依赖隔离于你自己编写的代码库是非常easy的。

这篇文档是关于Spring framework特性的参考文档。如果你有任何疑问、建议、问题，请直接联系spring官方的联系方式，当然也可以顺便发给我一份。

* [user mailing list](https://groups.google.com/forum/#!forum/spring-framework-contrib)
* [Questions on the Framework]( https://spring.io/questions)
* 灰机的邮箱:[jianbo.fan2016@gmail.com](#) 或 [736078227@qq.com](#)
* 灰机的个人主页：开发中...真的在开发中，域名都买好啦!!



## 1.Spring新手入门
这段参考指南提供了关于spring framework的细节信息。它为所有特性（all features）和一些Spring包含的底层概念(如依赖注入:Dependency Injection)都提供了综合性的文档.

如果你刚开始接触Spring，你可能希望通过创建一个基于[Spring Boot](http://projects.spring.io/spring-boot/)的应用程序来开始你的Spring之旅。Spring Boot为创建基于Spring的应用(可直接用于生产)提供了非常便捷的方式(真的灰常便捷，类似grails，但个人觉得比grails要方便和强大的多)。它是基与Spring framework的，提倡**“约定大于配置”(convention over configuration)**，并且被设计成让你迅速的构建和运行你的工程(is designed to get you up and running as quickly as possible)。

<br/>

## 2.Spring Framework介绍
Spring Framework 是一个为开发java应用提供综合性基础设施（infrastructure）支持的java平台（即“框架”）。因为这些基础设施由Spring Framework管理，所以开发者可以专注于应用开发。

Spring让你能通过POJOs(plain old java objects)构建应用、将企业级服务“无侵入式的”应用到POJOs中。此功能适用于Java SE全部和部分Java EE编程模型。

作为一名开发人员，举几个栗子来show一下你能通过Spring平台获得哪些益处：
* 让你在不使用transaction APIs的情况下处理数据库事务
* 不使用传统Servlet API就能方便的将你的服务以http endpoint的形式发布出去
* 无需调用繁琐的JMS API就能通过spring提供的包装后的JMS工具执行JMS动作
* 无需实现麻烦JMX API就能实现java应用管理

-----

### 2.1 依赖注入和控制反转

传统的java应用程序——从 受限制的、嵌入式的应用程序 到 多层的、服务端的企业应用通常由互相之间有协作(耦合)关系的对象组成。因此，应用程序中的对象**彼此具有依赖关系。**

虽然java平台提供了丰富的应用程序开发功能，但它缺乏一些组织基础模块，从而形成一个连贯的整体的思想，并把这些工作留给了架构狮和程序猿。虽然你可能精通设计模式——工厂模式、抽象工厂模式、建造者模式、装饰者模式、服务定位模式(Factory, Abstract Factory, Builder, Decorator, and Service Locator),并且你用他们组成了各种类和方法。这些设计模式仅仅只是：给出一个名字，告诉你它能做什么，通常的最佳实战场景是哪里。但问题是：很多人还是不知道如何使用它们(感觉因为这需要大量的实践经验)。设计模式的最佳实践一定是根据自己正在开发的应用来完成的，所以这些模式仅仅能给出指导和参考。

Spring Framework的Ioc组件(控制反转)通过**提供将不同组件组成为一个完整的应用程序的正式的方式**来解决上面的诸多问题。Spring Framework将形式化的设计模式作为可以集成到你自己的应用程序中的first-class object。许多组织和机构都使用Spring Framework来设计**健壮的、可维护性**高的应用程序。


> **背景**
> “问题是，what aspect of control are [they] inverting？” Martin Fowler针对Ioc提出的一个问题。Fowler建议将Ioc这个名字改为DI(Dependency Injection)依赖注入

-----

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

<br/>

#### 2.2.1 核心容器(Core Container)
核心容器的组成包括下列模块：```spring-core```、```spring-beans```、```spring-context```、```spring-context-support```、```spring-expression```（Spring表达式语言，常用语AOP编程中定义Aspect(切面/方面)）

```spring-core```和```spring-beans```模块提供了spring Framework的基本组成部分(fundamental parts),包括控制反转和依赖注入两个特性。```BeanFactory```能以工厂模式实现复杂的Bean创建过程。它不需要程序猿编写传统的单例模式类，让你通过从实际的代码逻辑中分离出特定的依赖配置来实现解耦。

[*Context*](#)模块建立在[**Core and Beans**](#)模块提供的坚实基础之上：这意味着能以类似[JNDI 注册](#)那样通过框架风格(framework-style)的方式使用对象。*Context模块*继承了*Beans模块*的特性，并添加了下面的这些功能——国际化支持(i18n,例如使用资源包(resource bundles)),事件传播(event propagation)，资源加载(resource loading，这个不确定怎么翻译)，透明的创建上下文(transparent creation of contexts)——最常见的——例如通过Servlet容器创建。*Context模块*同样也支持Java EE特性，例如:EJB、JMX、远程连接(basic remoting)。*Context模块*的核心是```ApplicationContext```接口，Spring提供了丰富的该接口实现，例如用于Web应用的```WebApplicationContext```，Spring Boot应用中常用的```EmbeddedWebApplicationContext```，桩测试时用到的```StubWebApplicationContext```等等，他们分别为当前应用环境提供最适合的应用上下文环境。```spring-context-support```模块则在Spring Framework集成第三方库到应用上下文中时提供相应的支持，例如在集成：缓存功能(EhCache、Guava、JCache、Redis、MongoDB等等)、邮件(JavaMail)、调度框架(CommonJ,Quartz)、模板引擎(FreeMarker,JasperResports,Velocity)。

```spring-expression```模块提供丰富的*表达式语言*，用于在运行时完成对对象查询、操作。它是统一表达式语言(el表达式)的一个扩展。```spring-expression```支持在Spring Ioc容器中setting和getting属性值、属性分配(property assignment)、方法调用、获取集合内容、逻辑/算法运算、别名的命名、根据对象名称进行检索等。It also supports list projection and selection as well as common list aggregations.

<br/>

#### 2.2.2 AOP和Instrumentation(实在是不知如何翻译....)
```spring-aop```模块提供了一套*面向切面编程的实现*(aspect-oriented programing)，这允许你在不变更原有代码的基础上，实现对批量方法的拦截,并在拦截的前后或异常时定义自己的实现。

```spring-aop```提供的AOP功能主要依赖于JDK动态代理(对接口实现)和cglib动态代理(对无接口的实现)。如果要使用```AspectJ```实现，需要使用```spring-aspects```模块。

```spring-instrument```模块提供了class instrumentation支持和用于特定的应用服务的类加载器实现。```spring-instrymentation-tomcat```模块包含了Spring的Tomcat代理instrumentation

<br/>

#### 2.2.3 消息服务
Spring Framework 4开始，包含了```spring-messaging```模块，这个模块包含了*Spring Integration project*中的关键抽象，例如```Message```,```MessageChannel```,```MessageHandler```,还有其他一些为“基于消息传递的应用”提供服务的关键抽象。这个模块中同样包含了一系列的用于映射消息到方法中的注解(annotations),类似基于Spring MVC注解的编程模型。

<br/>

#### 2.2.4 数据访问/集成(Access/Integration)
*数据访问/集成*层由下列模块组成：
* ```spring-jdbc```
	* 提供了一个JDBC抽象层，让你远离冗长的JDBC编程和解析database供应商特定的错误代码
* ```spring-tx```
	* 提供了*编程式*和*声明式*的事务管理
* ```spring-orm```
	* 提供了一个集成层，用于集成第三方对象关系映射的实现，如[JPA](#),[JDO](#),[Hibernate](#)。在```spring-orm```中，你能在使用所有这些第三方实现的特性的基础上，结合使用Spring提供的所有功能。例如前面提到的简单的声明式事务管理。
* ```spring-oxm```
	* 提供``` Object/XML```关系映射的抽象层支持，如：JAXB、Castor、XMLBeans、JIBX和XStream.
* ```spring-jms```
	* 这个模块涵盖了消息的生产/消费功能支持。自Spring Framework 4.1开始，它也集成了```spring-messaging```模块
	
<br/>

#### 2.2.5 Web
*Web层*由下面几个模块组成：```spring-web```、```spring-webmvc```、```spring-websocket```、```spring-webmvc-portlet```

* ```spring-web```:该模块提供了*面向Web*(Web-oriented)的基础特性支持。例如多文件上传功能，使用Servlet的```Listener```来初始化Ioc容器，并提供了*面向Web*的实现了```ApplicationContext```的上下文环境。 它同样也包含了HTTP clients功能和Web相关的远程调用支持。

* ```spring-webmvc```：也称为*Web-Servlet模块*。这个模块包含Spring模式视图控制器 和 [REST](http://www.redbooks.ibm.com/redbooks/pdfs/sg248357.pdf)风格的web service实现。Spring的MVC框架提供了领域模型代码和Web表单之间的清晰分离，并与Spring Framework的所有其他功能集成。

* ```spring-webmvc-portlet```：也称为*Web-Portlet模块*。提供了再Portlet环境中的MVC实现，并实现了其他在```spring-webmvc```中的功能

<br/>

#### 2.2.6 测试
```spring-test```模块支持使用JUnit或TestNG对Spring组件进行*单元测试*和*集成测试*。它提供了对Spring ```ApplicationContext```上下文的一致性加载，并将它们缓存下来。它同样提供了[mock测试](#)，让你可以对你的代码做不依赖于其他类的隔离测试。

------
### 2.3 应用场景



