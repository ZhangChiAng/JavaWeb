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
