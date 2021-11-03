# 一、JDK环境搭建



**环境变量的配置**

1. 编辑profile文件：`vi /etc/profile`

2. 在末尾追加以下内容：

export	JAVA_HOME=/usr/local/jdk-17.0.1

export	PATH=$JAVA_HOME/bin:$PATH

export	CLASSPATH=.:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar:$JAVA_HOME/jre/lib/rt.jar



3. profile文件修改完成，执行`source /etc/profile` 让上面的配置生效；

   source命令通常用于重新执行刚修改的初始化文件，使之立即生效，而不必注销并重新登录；
   语法：`source	文件名`

4. 检测环境变量是否成功

   使用`java -version`命令检测是否配置成功；

![image-20211102224848941](C:\Users\nanum008\AppData\Roaming\Typora\typora-user-images\image-20211102224848941.png)

​		出现以上界面这说明配置环境变量成功！



# 二、Tomcat环境搭建

## 1. 文件解压缩

首先将归档文件解压缩到`/usr/local/`，使用命令：`tar -zxvf apache-tomcat-9.0.54.tar.gz -C /usr/local`



## 2. 启动&关闭Tomcat

启动：在tomcat的bin目录下输入`./startup.sh `即可；

关闭：在tomcat的bin目录下输入`./shutdown.sh `即可；



## 3.  打开防火墙,使外部能访问

防火墙运行时可能会导致外部不能访问

未开启防火墙请忽略



# 三、MySQL配置

mysql默认安装目录：/usr/local/mysql

mysql存储数据库文件目录/usr/local/mysql/data

mysql默认占用端口：3306



## 1. 安装前准备工作

1）MySQL安装包下载地址：https://dev.mysql.com/downloads/mysql/

2）查看是否安装过MySQL：

```
rpm -qa | grep mysql
```



## 2. 安装包解压缩

 将安装包解压缩到：/usr/local/

```
tar -zxvf 安装包名路径 -C /usr/local/ 
```

可选项：重命名MySQL安装目录名

```
mv mysql-5.6.23-linux-glibc2.5-x86_64  mysql-5.6.23
```

可选项：删除安装包文件，节省磁盘空间；

```
rm mysql-5.6.23-linux-glibc2.5-x86_64.tar.gz
```



## 3. 创建Mysql用户组并添加Mysql用户

1）创建Mysql用户组

```
groupadd mysql
```

可以看到/etc/gshadow 文件里面增加了mysql用户组



2)添加Mysql用户

```
useradd -r -g mysql mysql
```

可以看到/etc/shadow 文件里面增加了mysql用户



3)修改目录的拥有者

- 进入Mysql安装目录：

```
cd /usr/local/mysql
```

- 修改目录的拥有者:

```
chown -R mysql ./
chgrp -R mysql ./
```

这里的点`./`代表的就是当前目录，选项`-R`表示递归当前目录及其子目录；



## 4. 初始化Mysql安装并启动Mysql服务

1）初始化Mysql安装

```
scripts/mysql_install_db --user=mysql
```

2)启动Mysql服务

```
./support-files/mysql.server start
```

3)查看MySQL服务是否启动

```
ps -ef|grep mysql
```



## 5. 配置环境变量

1）打开profile文件

```
vim /etc/profile
```

2)在末尾追加以下内容

```
 export MYSQL_HOME=/usr/local/这里填Mysql的安装目录名
 export PATH=$PATH:$MYSQL_HOME/bin
```

保存并退出：按esc键退出编辑模式，输入`:wq`保存并退出；

3）执行以下命令使配置生效

```
source /etc/profile
```



## 6. MySQL配置





## 7. 配置MySQL服务远程可访问

1）登录Mysql

```
mysql -uroot -p
```

会提示输入管理员密码。注意，这里输入的密码不会回显。



2)授权root 用户远程连接服务器

```
grant all privileges on *.* to 'root'@'%' identified by "admin" with grant option;
flush privileges;
```

