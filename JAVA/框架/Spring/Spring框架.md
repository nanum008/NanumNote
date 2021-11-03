# Spring基础

## 一、Spring-IOC

### 1.  IOC&DI

IOC(Inversion Of Control)是控制反转的意思，它不是一种技术实现，而是一种设计思想，一个重要的面向对象编程的法则，它能指导我们设计出低耦合的软件系统;

DI(Dependency Injection)是依赖注入的意思，是实现IOC的一种方式；

**问题诞生背景：**

在面向对象设计的软件系统当中，底层都是由无数个对象构成的，每个对象之间相互合作来实现我们的业务需求；

但是随着我们的业务需求的复杂度的提升，我们的软件系统系统也逐渐变得庞大，底层的对象非常多，对象之间的依赖关系异常复杂(耦合度高);`耦合度高`就会导致当我们的需求变动的时候`牵一发而动全身`有可能简单的变动都要花大功夫去改源码，项目的开发与维护变得异常困难,这个时候就需要一种方法(思想)来解耦合；



**对IOC的理解**

<img src="https://img-blog.csdnimg.cn/20200420115748990.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3hpYW9mZW5nMTAzMzAxMTE=,size_16,color_FFFFFF,t_70" style="zoom:50%;" />

既然是`控制反转`，那么我们就应该弄清楚：`谁控制谁,控制了什么？`、`又反转了什么？`、`既然有反转，那么正转又是什么呢？`……

- 谁控制谁，控制什么：在传统Java程序当中，我们是直接在对象内部通过new进行创建对象，是对象主动去获取创建`依赖对象`；而IOC是专门有一个容器来负责创建这些对象，即由IOC容器来控制对象的创建、装配以及外部资源获取（不只是对象包括比如文件等）。
- 为何是反转，反转了什么：有反转就有正转，传统应用程序是由我们自己在对象中主动控制去直接创建依赖对象，也就是正转；而反转则是由IOC容器来帮忙创建及注入依赖对象：由容器帮我们查找及注入依赖对象，对象只是被动的接受依赖对象，所以是反转，`依赖对象的创建方式`被反转了。



**对DI的理解**

- DI是依赖注入的意思，即通过属性的`set`方法结合反射机制给对象的属性赋值；
- 



### 2. Spring-Bean

#### 1）创建Bean

---

Spring的Bean都是在Spring的配置文件里创建的;

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">

    <!--一个bean标签就代表一个spring对象，class属性值为全限定类名，id属性是该bean的全局唯一标识-->
    <bean id="User" class="com.nanum.User"/>
    
</beans>
```

注意：

-  bean 的 id是严格区分大小写的 如果id不存在会报错： NoSuchBeanDefinitionException    

- 如果容器中同一个类型的bean有多个，再根据类型获取的话就会报错： NoUniqueBeanDefinitionException 
- bean一般需要无参构造，spring会调用它来创建对象
- 如果没有无参构造，需要给构造方法的参数赋值：    

<constructor-arg index="参数下标"  value="值"/>
  默认情况下，每个类型的bean在容器中只有一个对象（单例） <bean scope="singleton">                                            多例，每- 用一次，创建一个新的对象, 如果配置多例                  <bean scope="prototype">
  初始化方法 和 销毁方法： <bean init-method="初始化方法名()" destory-method="销毁方法名()" >                                        		单例：单例对象既会调用初始化方法，也会调用销毁方法

​        多例：每使用一个多例对象都会调用初始化方法，但所有的多例对象都不会调用销毁方法







创建方式有三种，分别是：

- 默认的构造方法
- 下标
- 参数类型

#### 2）为Bean的属性赋值

---

- 通过构造参数为属性赋值
  - 参数名
  - 参数下标
- 通过

### 3. Spring&MyBatis整合

---

1）相关依赖坐标如下：

```groovy
 	//logback 日志包
    implementation 'ch.qos.logback:logback-classic:1.2.6'
    // mybatis与spring整合的jar包
    implementation 'org.mybatis:mybatis-spring:2.0.6'
    //spring管理的 jdbc ,以及事务相关的
    implementation 'org.springframework:spring-jdbc:5.3.11'
    //Spring-MVC
    implementation 'org.springframework:spring-webmvc:5.3.11'
    //Servlet
    compileOnly('javax.servlet:javax.servlet-api:4.0.1')
    //MySQL数据库驱动
    implementation 'mysql:mysql-connector-java:8.0.25'
```



2）IoC容器创建Mybatis相关bean：连接池对象、SqlSessionFctory对象、SqlSession对象

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!-- xmlns 是xml的命名空间
    要引入新的 context命名空间
-->
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:context="http://www.springframework.org/schema/context"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
 http://www.springframework.org/schema/beans/spring-beans.xsd
 http://www.springframework.org/schema/context
 http://www.springframework.org/schema/context/spring-context.xsd">
 
    <!--
       读取 jdbc.properties 中的内容
            property-placeholder: 占位符
            location： 属性文件的位置
    -->
    <context:property-placeholder location="classpath:jdbc.properties"/>
 
    <!-- 1) 获得数据库连接池对象，并交由 spring 同一管理 -->
    <bean id="dataSource" class="com.alibaba.druid.pool.DruidDataSource">
 
        <!-- 连接数据库的驱动，连接字符串，用户名和登录密码-->
        <property name="driverClassName" value="${drivername}"/>
        <property name="url" value="${url}"/>
        <property name="username" value="${jdbc.username}"/>
        <property name="password" value="${password}"/>
 
        <!-- 数据池中最大连接数和最小连接数-->
        <property name="maxActive" value="${max}"/>
        <property name="minIdle" value="${min}"/>
    </bean>
 
    <!-- 2) 获取 SqlSessionFactory 对象，并交由 spring 管理-->
    <bean id="sqlSessionFactory" class="org.mybatis.spring.SqlSessionFactoryBean">
        <!-- 注入连接池
         给 sqlsessionFactory 的属性 dataSource 赋值
            ref="引用该 spring容器 中的另一个 bean的id"
        -->
        <property name="dataSource" ref="dataSource"/>
        <!-- 注入 映射文件 mapper
         给 sqlsessionFactory 的属性 mapperLocation 赋值
           value="映射文件 XXXmapper.xml 的相对路径"
          -->
        <property name="mapperLocations" value="classpath:com/chen/mapper/*.xml"/>
    </bean>
 
    <!-- 3) 获取 SqlSession 对象，并交由 spring 管理  用SqlSessionTemplate得到的SqlSession可以不用我们自己操心事务的管理，以及关闭操作-->
    <bean id="sqlSession" class="org.mybatis.spring.SqlSessionTemplate">
        <!-- 给 SqlSessionTemplate 的构造函数赋值-->
        <constructor-arg index="0" ref="sqlSessionFactory" />
    </bean>
</beans>
```



## 三、Spring-AOP

