# Servlet乱码问题

## 一、终极解决方案

终极解决方案：全局使用UTF-8编码

- tomcat：在"service.xml"文件的Connector标签里加入”URIEncoding=UTF-8“

- IntelliJ IDEA：

  - ![image-20210726173609268](C:\Users\null'pointer\AppData\Roaming\Typora\typora-user-images\image-20210726173609268.png)

    追加**-Dfile.encoding=UTF-8**；

    ![image-20210726173914145](C:\Users\null'pointer\AppData\Roaming\Typora\typora-user-images\image-20210726173914145.png)

  - 

## 二、Intellij IDEA控制台乱码问题

- step01：打开"Edit Configurations“；

  <img src="C:\Users\null'pointer\AppData\Roaming\Typora\typora-user-images\image-20210726171712990.png" alt="image-20210726171712990" style="zoom:67%;" />

- stet02：在VM options一栏输入：-Dfile.encoding=UTF-8；

  ![image-20210726172036568](C:\Users\null'pointer\AppData\Roaming\Typora\typora-user-images\image-20210726172036568.png)

- setp03：重启服务器即可。