# 一、B/S架构角色关

![image-20211025205729603](C:\Users\nanum008\AppData\Roaming\Typora\typora-user-images\image-20211025205729603.png)

# 二、Servlet

## 1、Servlet的定义

想要定义一个Servlet需要实现以下两步：

- 实现`Servlet`接口或者继承`HttpServlet`；

- 重写`service()`或者`doGet()`&`doPost()`；



### 1）方式一：实现Servlet接口





### 2）方式二：继承HttpServlet





## 2、Servlet的注册

定义好的Servlet需要在`web.xml`文件里注册才能生效，才能被Tomcat服务器识别；



### 1）方式一：在web.xml里注册

```xml

<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns="https://jakarta.ee/xml/ns/jakartaee"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="https://jakarta.ee/xml/ns/jakartaee https://jakarta.ee/xml/ns/jakartaee/web-app_5_0.xsd"
         version="5.0">
    <!--一个Servlet标签代表一个Servlet-->
    <servlet>
        <!--为Servlet起的别名，便于servlet-mapping标签与当前Servlet进行绑定-->
        <servlet-name>forwardServlet</servlet-name>
        <!--Servlet类的全限定类名-->
        <servlet-class>com.nanum.ForwardServlet</servlet-class>
        <!--可选项1：初始化参数-->
        <!--可以为Servlet配置初始化参数-->
        <init-param>
            <param-name>name</param-name>
            <param-value>value</param-value>
        </init-param>
        <!--可选项2：为servlet设置加载优先级，数值越小，优先级越高，tomcat就会优先创建Servlet实例-->
        <load-on-startup>1</load-on-startup>
    </servlet>
    

    <!--servlet映射标签，用于为Servlet配置访问地址-->
    <!--url-pattern标签里的值就是与之绑定的servlet的访问地址，切记在最前面加上`/`，这表示从当前项目的根路径开始-->
    <servlet-mapping>
        <servlet-name>forwardServlet</servlet-name>
        <url-pattern>/forwardServlet</url-pattern>
    </servlet-mapping>
</web-app>
```





### 2）方式二：使用注解 

```java
//冒号里面的内容就是`url-pattern`的值，也就是当前servlet的访问地址；
//也可以使用数组为当前servlet定义多个访问地址：
//@WebServlet({"/mainServlet","/other"})
@WebServlet("/mainServlet")
public class MainServlet extends HttpServlet {

    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {

    }
}
```





## 3、Servlet的生命周期

1）先调用有参的`init()`方法初始化Servlet；

2）然后调用`service()`方法处理请求并响应；

3）最后调用`destroy()`方法销毁Servlet实例；

​	a）长时间不调用会销毁servlet实例（gc）；

​	b）服务器关闭；



## 4、ServletConfig

ServletConfig的实例封装了与之对应的Servlet的配置信息，也就是将`<servlet>`标签里的内容封装成了ServletConfig；

```xml
<servlet>
    <servlet-name>forwardServlet</servlet-name>
    <servlet-class>com.nanum.ForwardServlet</servlet-class>
    <init-param>
        <param-name>name</param-name>
        <param-value>value</param-value>
    </init-param>
    <load-on-startup>1</load-on-startup>
</servlet>
```



**常用方法说明**

| 方法                          | 说明                                     |
| ----------------------------- | ---------------------------------------- |
| getInitParameter(String name) | 根据参数名获取初始化参数（init-param）； |
| getServletContext()           | 获取ServletContext；                     |
| getServletName()              | 获取Servlet的别名(servlet-name)；        |
| getInitParameterNames()       | 获取所有初始化参数的名字；               |




## 5、HttpServletRequest&HttpServletResponse

ServletRequest和ServletResponse分别对应浏览器发起的一次Http请求和服务器端的一次Http响应；

### 1）HttpServletRequest

HttpServletRequest封装了用户在浏览器发起的一次请求的所有信息；



**常用方法**

| 方法                      | 说明                                   |
| ------------------------- | -------------------------------------- |
| getRequestDispatcher()    | 获取请求调度对象，用作请求转发；       |
| getSession()              | 获取Session对象；                      |
| getCookies()              | 获取所有的Cookie，返回一个Cookie数组； |
| getParameter(String name) | 根据参数名获取请求行参数；             |
| getHeader(String name)    | 根据参数名获取请求头参数             |
| getHeaderNames()              | 获取所有的请求头参数名；                 |
| getRemoteAddr()               | 获取远程ip地址；                         |
| getRemoteHost()               | 获取远程主机的地址；                     |
| getRemotePort()               | 获取远程主机的端口号；                   |
| getProtocol()                 | 获取请求所使用的协议；                   |







# 四、ServletContext

一个ServletContext对应一个项目；



## 1、获取方式

1）从Servlet获取，所有的Servlet共享一个ServletContext；

2）从Servletonfig对象获取；

3）从HttpServletRequest对象获取；



## 2、常用方法说明

| 常用方法              | 说明                               |
| --------------------- | ---------------------------------- |
| getInitParameter()    | 获取整个web环境里的所有配置参数；  |
| getRealPath()         | 获取当前项目的绝对路径；           |
| getContextPath()      | 获取当前项目的根目录；             |
| getResourceAsStream() | 获取当前项目中的某个文件的流对象； |







# 五、转发&重定向

## 1、转发

Servlet转发就是将一次Http请求转发给另一个Servlet处理，浏览器总共还是一次请求；

```java
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        //转发时可以在HttpServletRequest对象当中携带属性(数据)；
        req.setAttribute("user",new User());
        //将请求转发给otherServlet处理；
        req.getRequestDispatcher("otherServlet").forward(req,resp);
    }
```



注意：

转发可能会引起：`405方法不允许`

假设AServlet的的一个post请求转发给BServlet处理，而Bservlet又只重写了`doGet()`方法，只能处理get请求。这时post请求由AServlet转发给BServlet，BServlet又不能处理post请求就会报405错误。所以，对于转发与重定向请合理选择；



## 2、重定向





# 六、拦截器

使用注解`@WEBFilter`的时候，所拦截的路径最前方一定要是是`/`，否者部署工件会报错；
