---
description: Java DataBase Connectivity，使用Java语言操作关系型数据库的一套API
---

# JDBC

## JDBC操作数据库步骤

```java
//1. 注册驱动
Class.forName("com.mysql.cj.jdbc.Driver");
//2. 获取连接
String url = "jdbc:mysql://localhost:3306/web01";
String username = "root";
String password = "1234";
Connection connection = DriverManager.getConnection(url, username, password);
//3. 获取SQL语句执行对象
Statement statement = connection.createStatement();
//4. 执行SQL
int i = statement.executeUpdate("update user set age = 25 where id = 1");
System.out.println("SQL执行完毕，影响的记录数为：" + i);
//5. 释放资源
statement.close();
connection.close();
```

