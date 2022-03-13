---
title: SpringBoot解决跨域的三种方式
tags:
  - SpringBoot
categories:
  - SpringBoot
toc: true
abbrlink: 45037
date: 2021-07-25 13:28:54
---

## 方法一：

<!--more-->

```java
import org.springframework.context.annotation.Configuration;
import org.springframework.web.servlet.config.annotation.CorsRegistry;
import org.springframework.web.servlet.config.annotation.WebMvcConfigurer;
@Configuration
public class CorsConfig implements WebMvcConfigurer {
    @Override
    public void addCorsMappings(CorsRegistry registry) {
        registry.addMapping("/**")
                .allowedOrigins("*")
                .allowedMethods("GET", "HEAD", "POST", "PUT", "DELETE", "OPTIONS")
                .allowCredentials(true)
                .maxAge(3600)
                .allowedHeaders("*");
    }
}
```

这种方式是全局配置的，网上也大都是这种解决办法，但是很多都是基于旧的spring版本，比如：

*https://blog.csdn.net/tiangongkaiwu152368/article/details/81099169*

文中WebMvcConfigurerAdapter在spring5.0已经被标记为Deprecated，点开源码可以看到：

```java
/**
 * An implementation of {@link WebMvcConfigurer} with empty methods allowing
 * subclasses to override only the methods they're interested in.
 *
 * @author Rossen Stoyanchev
 * @since 3.1
 * @deprecated as of 5.0 {@link WebMvcConfigurer} has default methods (made
 * possible by a Java 8 baseline) and can be implemented directly without the
 * need for this adapter
 */
@Deprecated
public abstract class WebMvcConfigurerAdapter implements WebMvcConfigurer {}	
```

spring5最低支持到jdk1.8，所以注释中明确表明，你可以直接实现WebMvcConfigurer接口，无需再用这个适配器，因为jdk1.8支持接口中存在default-method。

## 方法二：

```java
import org.springframework.context.annotation.Configuration;
import javax.servlet.*;
import javax.servlet.annotation.WebFilter;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;
@WebFilter(filterName = "CorsFilter ")
@Configuration
public class CorsFilter implements Filter {
    @Override
    public void doFilter(ServletRequest req, ServletResponse res, FilterChain chain) throws IOException, ServletException {
        HttpServletResponse response = (HttpServletResponse) res;
        response.setHeader("Access-Control-Allow-Origin","*");
        response.setHeader("Access-Control-Allow-Credentials", "true");
        response.setHeader("Access-Control-Allow-Methods", "POST, GET, PATCH, DELETE, PUT");
        response.setHeader("Access-Control-Max-Age", "3600");
        response.setHeader("Access-Control-Allow-Headers", "Origin, X-Requested-With, Content-Type, Accept");
        chain.doFilter(req, res);
    }
}
```

这种办法，是基于过滤器的方式，方式简单明了，就是在response中写入这些响应头，好多文章都是第一种和第二种方式都叫你配置，其实这是没有必要的，只需要一种即可。

## 方法三：

```java
public class GoodsController {
    @CrossOrigin(origins = "http://localhost:4000")
    @GetMapping("goods-url")
    public Response queryGoodsWithGoodsUrl(@RequestParam String goodsUrl) throws Exception {}
}
```

@CrossOrigin 注解

```java
@Target({ ElementType.METHOD, ElementType.TYPE })
@Retention(RetentionPolicy.RUNTIME)
@Documented
public @interface CrossOrigin {}
```

从元注解@Target可以看出，注解可以放在method、class等上面，类似RequestMapping，也就是说，整个controller下面的方法可以都受控制，也可以单个方法受控制。

也可以得知，这个是最小粒度的cors控制办法了，精确到单个请求级别。

以上三种方法都可以解决问题，最常用的应该是第一种、第二种。



参考文章：http://www.telami.cn/2019/springboot-resolve-cors/
