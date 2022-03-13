---
title: SpringBoot 401 Unauthorized问题解决方案
tags:
  - SpringBoot
categories:
  - SpringBoot
toc: false
abbrlink: 5740
date: 2021-07-25 12:48:58
---



**使用浏览器访问接口，自动跳转到的页面**

<!--more-->

```java
@Api("用户信息管理")
@RestController
@RequestMapping("/test")
public class TestController extends BaseController
{
    private final static Map<Integer, UserEntity> users = new LinkedHashMap<Integer, UserEntity>();
    {
        users.put(1, new UserEntity(1, "admin", "admin123", "15888888888"));
    }

    @ApiOperation("获取用户列表")
    @GetMapping("/list")
    public AjaxResult userList()
    {
        List<UserEntity> userList = new ArrayList<UserEntity>(users.values());
        return AjaxResult.success(userList);
    }
}
```

**使用浏览器访问接口，自动跳转到的页面**

```java
{
    "timestamp": "2021-07-19T19:50:05.607+0000",
    "status": 401,
    "error": "Unauthorized",
    "message": "Unauthorized",
    "path": "/test/list"
}
```

**使用浏览器访问接口，自动跳转到的页面**

![image-20210720042117171](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/SpringBoot401%E9%97%AE%E9%A2%98.png)

最终找到问题所在，是导入了`Spring-security`包的问题

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-security</artifactId>
</dependency>
```

当我们使用了Spring-security 之后，Spring Security默认对所有路径进行权限认证，并且提供默认的登陆页面。如果系统最终没有使用到Spring Security，将该依赖移除即可解决问题；如果系统确实需要使用Spring Security，那么可以自定义路径鉴权方式：

```java
@Configuration
@EnableWebSecurity
@EnableGlobalMethodSecurity(prePostEnabled = true, securedEnabled = true)
public class WebSecurityConfig extends WebSecurityConfigurerAdapter {
    @Override
    protected void configure(HttpSecurity httpSecurity) throws Exception {
        httpSecurity.authorizeRequest()              
            // 直接放行
            .antMatchers("/auth/**", "/error/**", "/dev/**").permitAll()
            // 权限认证
            .anyRequest().authenticated();
    }
}

```

**Spring Security默认的configure(HttpSecurity httpSecurity)实际上等同于如下配置：**

```java
    @Override
    protected void configure(HttpSecurity httpSecurity) throws Exception {
        httpSecurity.authorizeRequest()
            // 对所有http请求进行权限认证
            .anyRequest().authenticated().and()
            // 支持基于表单的登陆
            .formLogin().and()
            // 支持基于Basic方式的认证
            .httpBasic();
    }
```

同时，由于没有重载configure(AuthenticationManagerBuilder)，所有系统没有用户存储支撑认证过程，所以系统相当于没有用户，所以没有人可以认证成功。
