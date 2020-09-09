# 对于Java开发中时间的处理

### 方法一：yml配置

```
spring：
  jackson:
    date-format: yyyy-MM-dd HH:mm:ss
    time-zone: GMT+
```

### 方法二：实体类加注解

```
public class User {
    private Integer id;
    private String name;
    private String password;
    @DateTimeFormat(pattern = "yyyy-MM-dd HH:mm:ss")
    @JsonFormat(pattern = "yyyy-MM-dd HH:mm:ss"，timezone="GMT+8")
    private LocalDateTime time;
}
```

**@DateTimeFormat**是入参格式化

**@JsonFormat**是出参格式化

对于jackson在序列化时间时是按照国际化标准时间GMT进行格式化的，而在国内默认时区使用的是CST时区，两者相差8个小时。所以要GMT+8

### 方法三：时间转换工具类