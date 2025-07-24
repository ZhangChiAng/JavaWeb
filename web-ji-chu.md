# Web基础

## SpringBootWeb入门

1. 创建springboot工程，并勾选web开发相关依赖。
2. 定义XxxController类，添加注解`@RestController` ，添加方法及注解`@RequestMapping('/path')` 。

## HTTP协议

### HTTP请求协议

### HTTP响应协议

| 常用状态码 | 描述                          |
| :---: | --------------------------- |
|  200  | 客户端请求成功。                    |
|  404  | 请求资源不存在，URL输入有误，或者网站资源被删除了。 |
|  500  | 服务器发生不可预测的错误。               |

```java
@RequestMapping("/response2")
public ResponseEntity<String> response2() {
    return ResponseEntity
            .status(401)
            .header(...)
            .body(...);
}
```

## SpringBoot案例

1. 创建一个SpringBoot工程，并勾选web依赖、lombok。
2. 将数据文件和前端静态页面放置在`src/main/resources/static/` 。
3. 定义一个实体类，放置在`src/main/java/com/zca/pojo/` ，注解`@Data` `@NoArgsConstructor` `@AllArgsConstructor` 。
4. 开发服务器端程序，放置在`src/main/java/com/zca/controller/`，接收请求，读取数据并响应。

hutool工具包、`this.getClass()/getClassLoader()/getResourceAsStream("file")` 。

## 分层解耦

### 三层架构

* controller：控制层，接收前端发送的请求，对请求进行处理，并响应数据。
* service：业务逻辑层，处理具体的业务逻辑。
* dao：数据访问层（Data Access Object）（持久层），负责数据访问操作，包括数据的增、删、改、查。

每一层一个包，包里是各接口以及一个impl包，impl包里是每个接口对应的实现类。

### 控制反转与依赖注入

* 控制反转：Inversion Of Control，简称IOC。对象的创建控制权由程序自身转移到外部（容器），这种思想成为控制反转。
* 依赖注入：Dependency Injection，简称DI。容器为应用程序提供运行时所依赖的资源，称之为依赖注入。
* Bean对象：IOC容器中创建。管理的对象，称之为Bean。



1. 将Dao及Service层的实现类，交给IOC容器管理，`@Component` 。
2. 为Controller及Service注入运行时所依赖的对象，`@Autowired` 。

### 控制反转

* 声明bean的注解有以下几个：
  * `@Controller` 。
  * `@Service` 。
  * `@Repository` 。
  * `@Component` 。
* 注意事项：
  * 在Springboot集成web开发中，声明控制器bean只能用`@Controller` 。
  * 声明bean的注解要想生效，需要被扫描到，启动类默认扫描当前包及其子包。

### 依赖注入

* 基于`@Autowired` 进行依赖注入的常见方式有如下三种：
  * 属性注入。
  * 构造函数注入。
  * setter注入。
* 依赖注入的详解：
  * `@Autowired` ：默认按照类型自动装配。
  * 如果同类型的bean存在多个：
    * `@Primary` 。
    * `@Autowired` +`@Qualifier` 。
    * `@Resource` 。
* `@Resource` 与`@Autowired` 区别：
  * `@Autowired` 是Spring框架提供的注解，而`@Resource` 是JavaEE规范提供的。
  * `@Autowired` 默认是按照类型注入，而`@Resource` 默认是按照名称注入。
