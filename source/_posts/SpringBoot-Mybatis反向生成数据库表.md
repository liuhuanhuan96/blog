---
title: SpringBoot+Mybatis反向生成数据库表
tags:
  - SpringBoot
categories:
  - SpringBoot
toc: false
abbrlink: 45750
date: 2021-11-01 19:31:49
---



废话不多说，直接上源码

config目录下新增

<!--more-->

`MyBatisMapperScannerConfig`

```java
package com.lhh.config;

import org.mybatis.spring.mapper.MapperScannerConfigurer;
import org.springframework.boot.autoconfigure.AutoConfigureAfter;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;

/**
 * @author 刘欢欢
 * @version 1.0
 * @date 2021/10/17 4:44 下午
 */
@Configuration
@AutoConfigureAfter(MybatisTableConfig.class)
public class MyBatisMapperScannerConfig {

    @Bean
    public MapperScannerConfigurer mapperScannerConfigurer() throws Exception{
        MapperScannerConfigurer mapperScannerConfigurer = new MapperScannerConfigurer();
      	// com.lhh.mapper改成自己本地的地址，com.gitee.....不要动
        mapperScannerConfigurer.setBasePackage("com.lhh.mapper.*;com.gitee.sunchenbin.mybatis.actable.dao.*");  
        mapperScannerConfigurer.setSqlSessionFactoryBeanName("sqlSessionFactory");
        return mapperScannerConfigurer;
    }
}

```

`MybatisTableConfig`

```java
package com.lhh.config;

import com.alibaba.druid.pool.DruidDataSource;
import org.mybatis.spring.SqlSessionFactoryBean;
import org.springframework.beans.factory.annotation.Value;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.ComponentScan;
import org.springframework.context.annotation.Configuration;
import org.springframework.core.io.support.PathMatchingResourcePatternResolver;
import org.springframework.jdbc.datasource.DataSourceTransactionManager;


@Configuration
@ComponentScan(basePackages = {"com.gitee.sunchenbin.mybatis.actable.manager.*"})
public class MybatisTableConfig {

    @Value("${spring.datasource.druid.mysql1.driver-class-name}")
    private String driver;

    @Value("${spring.datasource.druid.mysql1.jdbc-url}")
    private String url;

    @Value("${spring.datasource.druid.mysql1.username}")
    private String username;

    @Value("${spring.datasource.druid.mysql1.password}")
    private String password;

    @Bean
    public DruidDataSource dataSource() {
        DruidDataSource dataSource = new DruidDataSource();
        dataSource.setDriverClassName(driver);
        dataSource.setUrl(url);
        dataSource.setUsername(username);
        dataSource.setPassword(password);
        dataSource.setMaxActive(30);
        dataSource.setInitialSize(10);
        dataSource.setValidationQuery("SELECT 1");
        dataSource.setTestOnBorrow(true);
        return dataSource;
    }

    @Bean
    public DataSourceTransactionManager dataSourceTransactionManager() {
        DataSourceTransactionManager dataSourceTransactionManager = new DataSourceTransactionManager();
        dataSourceTransactionManager.setDataSource(dataSource());
        return dataSourceTransactionManager;
    }

    @Bean
    public SqlSessionFactoryBean sqlSessionFactory() throws Exception{
        SqlSessionFactoryBean sqlSessionFactoryBean = new SqlSessionFactoryBean();
        sqlSessionFactoryBean.setDataSource(dataSource());
        PathMatchingResourcePatternResolver resolver = new PathMatchingResourcePatternResolver();
        sqlSessionFactoryBean.setMapperLocations(resolver.getResources("classpath*:com/gitee/sunchenbin/mybatis/actable/mapping/*/*.xml"));
        sqlSessionFactoryBean.setTypeAliasesPackage("com.lhh.bean.*");  //修改成本地地址
        return sqlSessionFactoryBean;
    }

}

```

bean下新增

Test.java

```java
package com.lhh.bean;

import com.gitee.sunchenbin.mybatis.actable.annotation.Column;
import com.gitee.sunchenbin.mybatis.actable.annotation.Table;
import com.gitee.sunchenbin.mybatis.actable.command.BaseModel;
import com.gitee.sunchenbin.mybatis.actable.constants.MySqlTypeConstant;

import java.sql.Date;

/**
 * 第一种定义方式，使用@Table和@Column方式定义
 *
 */
@Table(name = "test")
public class Test extends BaseModel {

	@Column(name = "id",type = MySqlTypeConstant.INT,length = 11,isKey = true,isAutoIncrement = true)
	private Integer	id;

	@Column(name = "name",type = MySqlTypeConstant.VARCHAR, length = 45, defaultValue = "hello")
	private String	name;

	@Column(name = "type",type = MySqlTypeConstant.VARCHAR,length = 45)
	private String	type;

	@Column(name = "description",type = MySqlTypeConstant.TEXT)
	private String	description;

	@Column(name = "create_time",type = MySqlTypeConstant.DATETIME)
	private Date	create_time;

	@Column(name = "update_time",type = MySqlTypeConstant.DATETIME)
	private Date	update_time;

	@Column(name = "number",type = MySqlTypeConstant.BIGINT,length = 5)
	private Long	number;

	@Column(name = "lifecycle",type = MySqlTypeConstant.CHAR,length = 1)
	private String	lifecycle;

	@Column(name = "dekes",type = MySqlTypeConstant.DOUBLE,length = 5,decimalLength = 2)
	private Double	dekes;

	public Integer getId(){
		return id;
	}

	public void setId(Integer id){
		this.id = id;
	}

	public String getName(){
		return name;
	}

	public void setName(String name){
		this.name = name;
	}

	public Date getCreate_time(){
		return create_time;
	}

	public void setCreate_time(Date create_time){
		this.create_time = create_time;
	}

	 public Date getUpdate_time(){
	 return update_time;
	 }
	
	 public void setUpdate_time(Date update_time){
	 this.update_time = update_time;
	 }

	public String getDescription(){
		return description;
	}

	public void setDescription(String description){
		this.description = description;
	}

	public Long getNumber(){
		return number;
	}

	public void setNumber(Long number){
		this.number = number;
	}

	public String getLifecycle(){
		return lifecycle;
	}

	public void setLifecycle(String lifecycle){
		this.lifecycle = lifecycle;
	}

	public Double getDekes(){
		return dekes;
	}

	public void setDekes(Double dekes){
		this.dekes = dekes;
	}

	public String getType() {
		return this.type;
	}

	public void setType(String type) {
		this.type = type;
	}
}

```

或者Test1.java

```java
package com.lhh.bean;


import com.gitee.sunchenbin.mybatis.actable.annotation.Column;
import com.gitee.sunchenbin.mybatis.actable.annotation.ColumnType;
import com.gitee.sunchenbin.mybatis.actable.annotation.IsAutoIncrement;
import com.gitee.sunchenbin.mybatis.actable.annotation.Table;
import com.gitee.sunchenbin.mybatis.actable.command.BaseModel;
import com.gitee.sunchenbin.mybatis.actable.constants.MySqlTypeConstant;

import javax.persistence.Id;
import java.util.Date;

/**
 * 第二种定义方式，使用@Table和@Column定义字段，具体内容用具体注解定义
 * 例如@Id，@IsNotNull，@isAutoIncrement等等
 * 如果没有设置name，会直接把变量名按照驼峰规则转换，如果没有设置类型也会自动转换Java的类型到SQL类型
 *
 */
@Table(name = "test1")
public class Test1 extends BaseModel {

    @Id
    @IsAutoIncrement
    @Column
    private Integer	id;

    @Column
    private Double price;

    @Column
    @ColumnType(value = MySqlTypeConstant.VARCHAR, length = 455)
    private String name;

    @Column
    private Date time;

    public Integer getId() {
        return this.id;
    }

    public void setId(Integer id) {
        this.id = id;
    }

    public Double getPrice() {
        return this.price;
    }

    public void setPrice(Double price) {
        this.price = price;
    }

    public String getName() {
        return this.name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public Date getTime() {
        return this.time;
    }

    public void setTime(Date time) {
        this.time = time;
    }
}

```

此时基本都已经配置好了，然后配置对应的application.yml即可



[参考源码地址](https://gitee.com/liuhuanhuan963019/springboot_mybatis_auto_create_table.git)
