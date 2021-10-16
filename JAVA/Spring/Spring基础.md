# Spring基础

## 一、Spring-IOC

### 1.  IOC&DI

IOC(Inversion Of Control)是控制反转的意思，它不是一种技术，只是一种思想，一个重要的面向对象编程的法则，它能指导我们如何设计出低耦合的软件系统;

DI(Dependency Injection)是依赖注入的意思，是实现IOC的一种方式；

**问题诞生背景：**

在面向对象设计的软件系统当中，底层都是由无数个对象构成的，每个对象之间相互合作来实现我们的业务需求；

但是随着我们的业务需求的复杂度的提升，我们的软件系统系统也逐渐变得庞大，底层的对象非常多，对象之间的依赖关系异常复杂(耦合度高);`耦合度高`就会导致当我们的需求变动的时候`牵一发而动全身`有可能简单的变动都要花大功夫去改源码，项目的开发与维护变得异常困难,这个时候就需要一种方法(思想)来解耦合；



**对IOC的理解**

<img src="https://img-blog.csdnimg.cn/20200420115748990.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3hpYW9mZW5nMTAzMzAxMTE=,size_16,color_FFFFFF,t_70" style="zoom:50%;" />

既然是`控制反转`，那么我们就应该弄清楚：`谁控制谁,控制了什么？`、`又反转了什么？`、`既然有反转，那么正转又是什么呢？`……

- 谁控制谁，控制什么：在传统Java程序当中，我们是直接在对象内部通过new进行创建对象，是对象主动去获取创建`依赖对象`；而IOC是专门有一个容器来负责创建这些对象，即由IOC容器来控制对象的创建、装配以及外部资源获取（不只是对象包括比如文件等）。

- 为何是反转，反转了什么：有反转就有正转，传统应用程序是由我们自己在对象中主动控制去直接创建依赖对象，也就是正转；而反转则是由IOC容器来帮忙创建及注入依赖对象：由容器帮我们查找及注入依赖对象，对象只是被动的接受依赖对象，所以是反转，`依赖对象的创建方式`被反转了。
  



## 二、SpringBean的创建方式

Spring的Bean都是在Spring的配置文件里创建的;

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">

    <!--一个bean标签就代表一个spring对象-->
    <bean id="User" class="com.nanum.User"/>
    
</beans>
```



创建方式有三种，分别是：

- 默认的构造方法

- 下标

- 参数类型