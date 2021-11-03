# MyBatis笔记

## 一、软件的三层架构 

**三层架构**

- 界面层：和用户交互的，接收用户请求的参数，显示处理结果。(html、jsp、servlet)
- 业务逻辑层：接收界面层传递的参数，处理相关的业务，调用数据库获取数据……
- 数据访问层：访问数据库，对数据进行增、删、改、查等操作。

**三层架构对应的包**

- 界面层：controller包(servlet)
- 业务逻辑层：service包(xxxService类)
- 数据访问层：dao包(xxxxDao类)

**三层对应的处理框架**

界面层：servlet——Springmvc(框架)

业务逻辑层：Service类——Spring(框架)

数据持久层：dao类——MyBatis(框架)



## 二、依赖地址

Gradle坐标：

```groovy
implementation 'org.mybatis:mybatis:3.5.7'
```

Maven坐标：

```xml
```



## 三、Mybatis之核心配置文件

mybatis.xml

```xml
<?xml version="1.0" encoding="utf-8"?>
<!--在这里指定dtd文档约束文件的url，集成开发环境会根据url去获取-->
<!DOCTYPE configuration
        PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-config.dtd">
<configuration>

    <!--配置Mybatis中数据库连接环境，可以配置多个，default属性指定当前使用的是哪个环境-->
    <environments default="mysql">
        
        <environment id="mysql">
            <!--配置Mybatis当中的事务 和JDBC一致-->
            <transactionManager type="JDBC"></transactionManager>
            
            <!--配置连接数据库连接的必要信息，采用数据库连接池-->
            <dataSource type="POOLED">
				<!--JDBC连接四大参数配置-->
                <property name="driver" value="com.mysql.cj.jdbc.Driver"/>
                <property name="url"value="jdbc:mysql://127.0.0.1:3306/mybatis_test?useSSL=false&amp;useUnicode=true&amp;characterEncoding=utf8&amp;serverTimezone=UTC"/>
                <property name="username" value="root"/>
                <property name="password" value="248650"/>
            </dataSource>
        </environment>

    </environments>

    <!--指定要加载的Mapper映射文件-->
    <mappers>
        <mapper resource="UserMapper.xml"/>
    </mappers>
</configuration>
```

### 1）属性文件的支持

---

mybatis支持对属性文件的读取，也就是说datasource元素里面`property元素`的值可以用`properties文件`代替，以达到解耦合的目的；

- 这种方式：

```xml
            <dataSource type="POOLED">
				<!--JDBC连接四大参数配置-->
                <property name="driver" value="com.mysql.cj.jdbc.Driver"/>
                <property name="url"value="jdbc:mysql://127.0.0.1:3306/mybatis_test?useSSL=false&amp;useUnicode=true&amp;characterEncoding=utf8&amp;serverTimezone=UTC"/>
                <property name="username" value="root"/>
                <property name="password" value="248650"/>
            </dataSource>
```



- 可以替换为以下这种方式：

mybaitis配置文件：mybatis.xml

```xml
            <dataSource type="POOLED">
				<!--JDBC连接四大参数配置-->
                <property name="driver" value=""/>
                <property name="url"value=""/>
                <property name="username" value=""/>
                <property name="password" value=""/>
            </dataSource>
```

属性文件：db.properties

```properties
drivername=com.mysql.cj.jdbc.Driver
username=root
password=248650
url=jdbc:mysql://127.0.0.1:3306/mybatis_test?useSSL=false&amp;useUnicode=true&amp;characterEncoding=utf8&amp;serverTimezone=UTC
```





## 四、Mybatis之映射文件
