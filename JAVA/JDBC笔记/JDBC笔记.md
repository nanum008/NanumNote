# JDBC学习笔记

## 一、JDBC的本质是什么？

jdbc的本质就是“SUN”公司制定的一套接口，我们JAVA程序员只需要面向这套接口编程即可操作数据库。

## 二、JDBC开发前的准备工作

先从官网下载好对应的驱动(jar包)，然后再将其配置到环境变量“classpath”当中去。

classpath——".;"+jar包路径

以上配置始基于文本编辑器开发，使用集成开发环境不需要此配置。

## 三、JDBC编程六步(需要背会)

- 第一步：注册驱动;(作用：告诉java程序，即将要连接哪个品牌的数据库)
- 第二步：获取连接;(表示JVM的进程和数据库之间的进程打开了，这属于进程之间的通信，重量级的，使用完之后务必关闭通道)
- 第三步：获取数据库操作对象(专门执行SQL语句的对象);
- 第四步：执行SQL语句;(DQL,DML……)
- 第五步：处理查询结果集;(只有第四步执行的是select语句的时候，才有第五步处理查询结果集)
- 第六步：释放资源;(使用完后务必关闭资源)

```java
//JDBC编程六步
imort java.sql.*;

public class Test{
    
    Connection connection = null;
    Statement statement = null;
    
    public static void main(String[] args){
        try{
            //1、注册驱动
            Driver	driver = new com.mysql.jdbc.Driver(); //多态，父类型引用指向子类对象。
            DriverMannager.registerDriver(driver)
                
            //2、获取数据库连接
            String account = "root";
            String password = "123456";
            String url = "jdbc:mysql://127.0.0.1:3306/test";
            connection = DriverMannager.getConnection(account,password,url);
            
            //3、获取数据库操作对象(专门执行SQL语句的对象)
            statement = connection.createStatement();
            
            //4、执行SQL语句
            String sql = "insert into dept(deptno,dname,loc) values(200,'后勤部','上海')";
            //专门执行DML语句的(insert、delet、update),返回值是影响数据库记录的条数。
            int count = statement.executeUpdate(sql);
            System.out.println(count == 1 ? "保存成功" : "保存失败");
            
            //5、处理查询结果集
        }catch(SQLException e){
            e.printStackTrace();
        }finally{
            //6、释放资源
            //为了保证资源一定释放，在finally语句块里关闭资源。(从小到大依次关闭)
            try{
               if(statement != null) 
				statement.close();
            }catch(SQLExcption e){
                e.printStackTrace();
            }
            
            try{
               if(connection != null) 
				connection.close();
            }catch(SQLExcption e){
                e.printStackTrace();
            }
        }
    } 
}
```



## 四、类加载的方式注册驱动

```java
//在加载“conm.mysql.jdbc.Driver”这个类的时候会执行这个类的静态代码块，静态代码块当中有注册驱动的语句。
Class.forName("conm.mysql.jdbc.Driver");
```





