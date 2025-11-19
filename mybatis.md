---
description: Mybatis是一款优秀的持久层框架，用于简化JDBC的开发
---

# Mybatis

## 辅助配置

### 配置SQL提示

### 配置Mybatis的日志输出

默认情况下，在Mybatis中，SQL语句执行时，我们并不能看到SQL语句的执行日志。加入如下配置，即可查看日志：

```yaml
mybatis:
  configuration:
    log-impl: org.apache.ibatis.logging.stdout.StdOutImpl
```

## 数据库连接池

* 是一个容器，负责分配、管理数据库连接（Connection）
* 优势：资源复用、提升系统响应速度
* 接口：DataSource
* 产品：C3P0、DBCP、Druid、Hikari（默认）

## 增删改查

### 删除操作

```java
@Delete("delete from user where id = #{id}")
public Integer deleteById(Integer id);
```

* Mybatis中执行DML语句时，有返回值，int类型，表示DML语句执行影响的记录数。
* Mybatis中 # 是占位符，会替换为 ? 生成预编译SQL（推荐）；$ 是字符串拼接符号，将参数值直接拼接在SQL中。

### 新增操作

{% code fullWidth="true" %}
```java
@Insert("insert into user(username,password,name,age) values(#{username},#{password},#{name},#{age})")
// #{}里填对象属性名
public void insert(User user);
```
{% endcode %}

### 更新操作

{% code fullWidth="true" %}
```java
// 需求：根据id更新用户信息
@Update("update user set username=#{username},password=#{password},name=#{name},age=#{age} where id=#{id}")
public void update(User user);
```
{% endcode %}

### 查询操作

{% code fullWidth="true" %}
```java
// 需求：根据用户名和密码查询用户信息
@Select("select * from user where username=#{username} and password=#{password}")
public User findByUsernameAndPassword(@Param("username") String username, @Param("password") String password);
// @Param注解的作用是为接口的方法形参起名字
// 基于官方骨架创建的springboot项目中，接口编译时会保留方法形参名，@Param注解可以省略
```
{% endcode %}

### XML映射配置
