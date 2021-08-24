# JDBC笔记

## 常见问题

- ```java
  Caused by: com.mysql.cj.exceptions.InvalidConnectionAttributeException: The server time zone value   
  ```

此问题为时区问题,在 JDBC 的连接 url 部分加上 serverTimezone=UTC 即可。
如果选择utc会比中国时间早8个小时，如果在中国，可以选择Asia/Shanghai或者Asia/Hongkong

```java
Stirng url = "jdbc:mysql://localhost:3306/mydb01?serverTimezone=UTC";
```



- 
