---
title: mybatis-genrator使用
tags:
  - MyBatis
categories:
  - MyBatis
toc: true
abbrlink: 20821
date: 2021-07-25 13:13:06
---

#### 1.mybatis=generator文件新增

在项目路径下新建如下xml文件：名称随便定义

<!--more-->

![image-20210426140410304](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/mybatis-generator01.png)

内容添加如下：具体需要该内容如下

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE generatorConfiguration
        PUBLIC "-//mybatis.org//DTD MyBatis Generator Configuration 1.0//EN"
        "http://mybatis.org/dtd/mybatis-generator-config_1_0.dtd">

<generatorConfiguration>
    <!--mysql 连接数据库jar 这里选择自己本地位置;
    如果不知道maven本地仓库地址，可以使用EveryThing工具全局搜索mysql-connector-java，找到jar包位置；
    也可以手动下载一个jar放在指定位置，进行引用。
    -->
    <classPathEntry location="C:\\Users\\lhh\\.m2\\repository\\mysql\\mysql-connector-java\\8.0.11\\mysql-connector-java-8.0.11.jar"/>

    <context id="testTables" targetRuntime="MyBatis3">
        <commentGenerator>
            <!-- 是否去除自动生成的注释,true：是,false:否 -->
            <property name="suppressAllComments" value="true"/>
        </commentGenerator>

        <!--数据库连接的信息：驱动类、连接地址、用户名、密码 -->
        <jdbcConnection driverClass="com.mysql.cj.jdbc.Driver"
                        connectionURL="jdbc:mysql://localhost:3306/shijiazhuang?serverTimezone=UTC&amp;useSSL=false" userId="root"
                        password="xxxx">
        </jdbcConnection>

        <!-- 默认false，把JDBC DECIMAL 和 NUMERIC 类型解析为 Integer，为 true时把JDBC DECIMAL 和
           NUMERIC 类型解析为java.math.BigDecimal -->
        <javaTypeResolver>
            <property name="forceBigDecimals" value="false"/>
        </javaTypeResolver>

        <!-- 指定javaBean生成的位置
            targetPackage：生成的类要放的包，真实的包受enableSubPackages属性控制；
            targetProject：目标项目，指定一个存在的目录下，生成的内容会放到指定目录中，如果目录不存在，MBG不会自动建目录
         -->
        <javaModelGenerator targetPackage="com.nuist.tw.rainfall.bean" targetProject="src/main/java">
            <!-- 在targetPackage的基础上，根据数据库的schema再生成一层package，最终生成的类放在这个package下，默认为false；如果多个数据库改为true分目录 -->
            <property name="enableSubPackages" value="false"/>
            <!-- 设置是否在getter方法中，对String类型字段调用trim()方法 -->
            <property name="trimStrings" value="true"/>
        </javaModelGenerator>

        <!--  指定mapper映射文件生成的位置
           targetPackage、targetProject同javaModelGenerator中作用一样-->
        <sqlMapGenerator targetPackage="mapper" targetProject="src/main/resources">
            <property name="enableSubPackages" value="false"/>
        </sqlMapGenerator>

        <!-- 指定mapper接口生成的位置
         targetPackage、targetProject同javaModelGenerator中作用一样
         -->
        <javaClientGenerator type="XMLMAPPER" targetPackage="com.nuist.tw.rainfall.mapper" targetProject="src/main/java">
            <property name="enableSubPackages" value="false"/>
        </javaClientGenerator>

        <!-- 指定数据库表
        domainObjectName：生成的domain类的名字,当表名和domain类的名字有差异时一定要设置，如果不设置，直接使用表名作为domain类的名字；
        可以设置为somepck.domainName，那么会自动把domainName类再放到somepck包里面；
        -->
        <table tableName="zone_stat_ref_backup"></table>
    </context>
</generatorConfiguration>
```

需要修改的地方：

**1：**

![image-20210426140756613](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/mybatis-generator02.png)

**2：**
![image-20210426140935628](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/mybatis-generator03.png)

**3：**

![image-20210426141048497](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/mybatis-generator04.png)

**4：**

![image-20210426141149622](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/mybatis-generator05.png)



#### 2.poom.xml新增依赖

```xml
<!-- mybatis代码生成插件 -->
			<plugin>
				<groupId>org.mybatis.generator</groupId>
				<artifactId>mybatis-generator-maven-plugin</artifactId>
				<version>1.3.2</version>
				<configuration>
					<!--配置文件的位置-->
					<configurationFile>src/main/resources/generatorConfig.xml</configurationFile>
					<verbose>true</verbose>
					<overwrite>true</overwrite>
				</configuration>
				<executions>
					<execution>
						<id>Generate MyBatis Artifacts</id>
						<goals>
							<goal>generate</goal>
						</goals>
					</execution>
				</executions>
				<dependencies>
					<dependency>
						<groupId>org.mybatis.generator</groupId>
						<artifactId>mybatis-generator-core</artifactId>
						<version>1.3.2</version>
					</dependency>
				</dependencies>
			</plugin>
```

### **3.idea新增maven执行程序**

#### 3.1: 

![image-20210426142455587](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/mybatis-generator06.png)

#### 3.2 新增maven执行依赖

![image-20210426142610092](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/mybatis-generator07.png)

#### 3.3: 新增maven执行脚本![image-20210426142758300](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/mybatis-generator08.png)

#### 3.4 选择本地maven配置

![image-20210426142849860](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/mybatis-generator09.png)

添加完毕，直接运行即可
