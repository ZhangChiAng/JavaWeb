# MySQL

## 安装

## 配置

### 配置环境变量

MYSQL\_HOME 为 mysql的解压目录，并将其 bin 目录加入 PATH 环境变量。

### 测试

```powershell
mysql
```

### 初始化

```powershell
mysqld --initialize-insecure
```

#### 注册MySQL服务

```powershell
mysqld -install
```

### 启动MySQL服务

```powershell
net start mysql    // 启动mysql服务

net stop mysql    // 停止mysql服务
```

### 修改默认账户密码

```powershell
mysqladmin -u root password 密码
```

## 登录

```powershell
mysql [-h数据库服务器IP地址 -P端口号] -u用户名 -p密码    // 方式1

mysql [-h数据库服务器IP地址 -P端口号] -u用户名 -p    // 方式2
```

## SQL语句

### DDL

```sql
-- 查询所有数据库
show databases;

-- 查询当前数据库
select database();

-- 使用/切换数据库
use 数据库名;

-- 创建数据库
create database [if not exists] 数据库名 [default charset utf8mb4];

-- 删除数据库
drop database [if exist] 数据库名;
```

```sql
-- 创建表
create table tablename (
    字段1 字段类型 [约束] [comment 字段1 注释],
    ......
    字段n 字段类型 [约束] [comment 字段n 注释]
) [comment 表注释];
```

|  约束  |            描述            |              关键字              |
| :--: | :----------------------: | :---------------------------: |
| 非空约束 |       限制该字段值不能为null      |            not null           |
| 唯一约束 |    保证字段的所有数据都是唯一、不重复的    |             unique            |
| 主键约束 |   主键是一行数据的唯一标识，要求非空且唯一   | primary key (auto\_increment) |
| 默认约束 |  保存数据时，如果未制定该字段值，则采用默认值  |            default            |
| 外键约束 | 让两张表的数据建立连接，保证数据的一致性和完整性 |          foreign key          |
