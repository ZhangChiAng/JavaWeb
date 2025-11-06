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
    字段1 字段类型 [约束] [comment 字段1注释],
    ......
    字段n 字段类型 [约束] [comment 字段n注释]
) [comment 表注释];
```

|  约束  |            描述            |              关键字              |
| :--: | :----------------------: | :---------------------------: |
| 非空约束 |       限制该字段值不能为null      |            not null           |
| 唯一约束 |    保证字段的所有数据都是唯一、不重复的    |             unique            |
| 主键约束 |   主键是一行数据的唯一标识，要求非空且唯一   | primary key (auto\_increment) |
| 默认约束 |  保存数据时，如果未制定该字段值，则采用默认值  |            default            |
| 外键约束 | 让两张表的数据建立连接，保证数据的一致性和完整性 |          foreign key          |

```sql
show tables;    -- 查询当前数据库的所有表
desc 表名; -- 查询表结构
show create table 表名; -- 查询建表语句

alter table 表名 add 字段名 类型(长度) [coment 注释] [约束]; -- 添加字段
alter table 表名 modify 字段名 新数据类型(长度); -- 修改字段类型
alter table 表名 change 旧字段名 新字段名 类型(长度) [comment 注释] [约束]; -- 修改字段名与字段类型
alter table 表名 drop column 字段名; -- 删除字段
alter table 表名 rename to 新表名; -- 修改表名

drop table [if exists] 表名; -- 删除表
```

### DML

#### DML-insert

```sql
-- 指定字段添加数据
insert into 表名(字段名1, 字段名2) values (值1, 值2);

-- 全部字段添加数据
insert into 表名 values (值1, 值2, ...);

-- 批量添加数据（指定字段）
insert into 表名 (字段名1, 字段名2) values (值1, 值2), (值1, 值2);

-- 批量添加数据（全部字段）
insert into 表名 values (值1, 值2, ...), (值1, 值2, ...);
```

#### DML-update

```sql
-- 修改数据
update 表名 set 字段名1 = 值1, 字段名2 = 值2, .... [where 条件];
-- 如果没有条件，则会修改整张表的所有数据
```

#### DML-delete

```sql
-- 删除数据
delete from 表名 [where 条件];
-- 如果没有条件，则会删除整张表的所有数据
-- 不能删除某一个字段的值，可以使用update将该字段的值设为NULL
```

### DQL

```sql
-- 基本查询
select
    字段列表
from 
    表名列表

-- 条件查询
where
    条件列表

-- 分组查询
group by
    分组字段列表
having
    分组后条件列表

-- 排序查询
order by
    排序字段列表

-- 分页查询
limit
    分页参数
```

#### DQL-基本查询

```sql
-- 查询多个字段
select 字段1, 字段2, 字段3 from 表名;

-- 查询所有字段（通配符）
select * from 表名;

-- 为查询字段设置别名，as关键字可以省略
select 字段1 [as 别名1], 字段2 [as 别名2] from 表名;

-- 去除重复记录
select distinct 字段列表 from 表名;
```

#### DQL-条件查询

```sql
select 字段列表 from 表名 where 条件列表;
```

| 比较运算符               | 功能                      |
| ------------------- | ----------------------- |
| between ... and ... | 在某个范围之内（含最小、最大值）        |
| in(...)             | 在in之后的列表中的值，多选一         |
| like 占位符            | 模糊匹配（\_匹配单个字符，%匹配任意个字符） |

#### DQL-分组查询

```sql
select 字段列表 from 表名 [where 条件列表] group by 分组字段名 [having 分组后过滤条件];
```

* where 与 having 的区别：
  1. 执行时机不同：where 是分组之前进行过滤，不满足 where 条件，不参与分组，而 having 是分组之后对结果进行过滤。
  2. 判断条件不同：where 不能对聚合函数进行判断，而 having 可以。
* 注意：
  1. 分组之后，查询的字段一般为聚合函数和分组字段，查询其他字段无任何意义。
  2. 执行顺序：where > 聚合函数 > having 。

#### DQL-排序查询

{% code fullWidth="false" %}
```sql
select 字段 from 表名 [where 条件] [group by 分组字段 having 过滤条件]
    order by 排序字段 排序方式;
```
{% endcode %}

* 排序方式：升序（asc），降序（desc）；默认为升序。

#### DQL-分页查询

```sql
select 字段 from 表名 [where 条件] [group by 分组字段 having 过滤条件] [order by 排序字段]
    limit 起始索引, 查询记录数 ;
```

* 说明：
  1. 起始索引从0开始。
  2. 分页查询是数据库的方言，不同的数据库有不同的实现，MySQL中是LIMIT。
  3. 如果起始索引为0，起始索引可以省略，直接简写为 limit 10 。
