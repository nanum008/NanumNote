# Tomcat的安装与配置

## 一、Tomcat的安装

1.1 访问官网下载Tomcat，官网：[https://tomcat.apache.org](https://tomcat.apache.org)；

<img src="C:\Users\null'pointer\AppData\Roaming\Typora\typora-user-images\image-20210726190822709.png" alt="image-20210726190822709" style="zoom: 50%;" />



![image-20210726191120753](C:\Users\null'pointer\AppData\Roaming\Typora\typora-user-images\image-20210726191120753.png)

1.2 下载后解压即可完成Tomcat服务器的安装。



## 二、Tomcat服务器的启动与关闭

- 启动tomcat

  在tomcat的根路径下找到**bin**这个目录，里面的有一个**startup.bat**文件，双击即可启动tomcat服务器；

  

  检测是否正常启动Tomcat服务器：浏览器输入**127.0.0.1:8080**回车，如果出现以下界面就说明Tomcat服务器正常启动。

  ![image-20210726193659968](C:\Users\null'pointer\AppData\Roaming\Typora\typora-user-images\image-20210726193659968.png)

  **PS**：tomcat的运行需要JRE，即JAVA运行环境，如果出现一个黑的窗口”一闪而过“很有可能是该电脑没有配置环境变量

  ​		**JAVA_HOME**导致的；

  ​		在Linux环境下双击**startup.sh**文件即可启动Tomcat服务器；

- 关闭tomcat

  同理，在**bin**目录下找到**shutup.bat**文件，双击即可关闭tomcat服务器。

  ps：关闭tomcat服务器不建议直接点击windows窗口的关闭按钮。

  

- 乱码问题

  如果出现乱码问题在Tomcat根目录下找到**conf**目录，在这个目录下找到**logging.xml**文件，打开该文件找到

  **java.util.logging.ConsoleHandler.encodin**字段，将等号后面值改为**GBK**即可解决乱码问题。

  

## 三、Tomcat服务器的配置

- 快捷打开Tomcat
  1. 配置环境变量CATALINA_HOME，CATALINA_HOME的值就是Tomcat的根路径。然后在path环境变量里添加字符串**%CATALINA_HOME%\bin**，这样在命令行窗口输入**startup**即可快捷启动Tomcat服务器，推荐使用这种方式。
  2. 找到**startup/shutup.bat**文件，右键选择发送到桌面快捷方式即可。
- 

