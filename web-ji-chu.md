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
