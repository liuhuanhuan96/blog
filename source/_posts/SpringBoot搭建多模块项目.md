---
title: SpringBoot搭建多模块项目
tags:
  - SpringBoot
categories:
  - SpringBoot
toc: true
abbrlink: 43507
date: 2021-07-25 12:45:53
---

## 一.项目结构

<!--more-->

![image-20210719235053608](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/SpringBoot%E6%90%AD%E5%BB%BA%E5%A4%9A%E6%A8%A1%E5%9D%97%E9%A1%B9%E7%9B%AE01.png)

**本文所有代码源码在本章末尾给出，读者可自取。**

## 二.创建过程

先创建一个`父项目工程`，然后删除多余文件后，在父工程中新增`子模块`

### 1.创建父工程

<img src="https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/SpringBoot%E6%90%AD%E5%BB%BA%E5%A4%9A%E6%A8%A1%E5%9D%97%E9%A1%B9%E7%9B%AE02.png" alt="image-20210719235433951" style="zoom:67%;" />

<img src="https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/SpringBoot%E6%90%AD%E5%BB%BA%E5%A4%9A%E6%A8%A1%E5%9D%97%E9%A1%B9%E7%9B%AE03.png" alt="image-20210719235649050" style="zoom:67%;" />

<img src="https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/SpringBoot%E6%90%AD%E5%BB%BA%E5%A4%9A%E6%A8%A1%E5%9D%97%E9%A1%B9%E7%9B%AE04.png" alt="image-20210719235745691" style="zoom:67%;" />

<img src="https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/SpringBoot%E6%90%AD%E5%BB%BA%E5%A4%9A%E6%A8%A1%E5%9D%97%E9%A1%B9%E7%9B%AE05.png" alt="image-20210719235824925" style="zoom: 67%;" />

完成一个父工程的创建！！！

注意记得删除父项目中pom.xml文件中parent属性 删除如下内容

```java
    <parent>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-parent</artifactId>
        <version>2.5.2</version>
        <relativePath/> <!-- lookup parent from repository -->
    </parent>
```



### 2.创建子模块

删除父工程中的多余信息，只保留对应的(.idea文件夹 , 和项目 pom 文件, 以及一个 *.iml 文件 )

**同时需要修改父工程中的打包方式为`pom`**

<img src="https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/SpringBoot%E6%90%AD%E5%BB%BA%E5%A4%9A%E6%A8%A1%E5%9D%97%E9%A1%B9%E7%9B%AE06.png" alt="image-20210720000251249" style="zoom:67%;" />

选中项目右击新建`module`

<img src="https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/SpringBoot%E6%90%AD%E5%BB%BA%E5%A4%9A%E6%A8%A1%E5%9D%97%E9%A1%B9%E7%9B%AE07.png" alt="image-20210720015005040" style="zoom:67%;" />

<img src="https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/SpringBoot%E6%90%AD%E5%BB%BA%E5%A4%9A%E6%A8%A1%E5%9D%97%E9%A1%B9%E7%9B%AE08.png" alt="image-20210720015041964" style="zoom:67%;" />

![image-20210720015136810](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/SpringBoot%E6%90%AD%E5%BB%BA%E5%A4%9A%E6%A8%A1%E5%9D%97%E9%A1%B9%E7%9B%AE09.png)

![image-20210720015207020](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/SpringBoot%E6%90%AD%E5%BB%BA%E5%A4%9A%E6%A8%A1%E5%9D%97%E9%A1%B9%E7%9B%AE10.png)

此时一个单独的module就创建好啦，删除一些我们不必要的文件，我们去修改当前admin  module中的`pom`文件中的`parent`标签中的内容为

````xml
    <parent>
        <artifactId>demo</artifactId>  //此时的id为父工程pom中的id
        <groupId>com.nuist</groupId>   //父工程中的groupid
        <version>1.0</version>			//父工程中的version
    </parent>
````

新增打包方式为jar

```xml
    <packaging>jar</packaging>
```

在父项目的pom.xml中新增子module,声明子module,相关配置如下：

```java
<modules>
		<module>admin</module>
</modules>
```

修改后的父pom文件如下（我新增了相关依赖包）：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>com.nuist</groupId>
    <artifactId>demo</artifactId>
    <version>1.0</version>

    <name>demo</name>
    <description>Demo project for Spring Boot</description>
    <properties>
        <java.version>1.8</java.version>
    </properties>

    <!-- 依赖声明 -->
    <dependencyManagement>
        <dependencies>

            <!-- SpringBoot的依赖配置-->
            <dependency>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-dependencies</artifactId>
                <version>2.2.13.RELEASE</version>
                <type>pom</type>
                <scope>import</scope>
            </dependency>

            <!--阿里数据库连接池 -->
            <dependency>
                <groupId>com.alibaba</groupId>
                <artifactId>druid-spring-boot-starter</artifactId>
                <version>${druid.version}</version>
            </dependency>

            <!--io常用工具类 -->
            <dependency>
                <groupId>commons-io</groupId>
                <artifactId>commons-io</artifactId>
                <version>${commons.io.version}</version>
            </dependency>

            <!--文件上传工具类 -->
            <dependency>
                <groupId>commons-fileupload</groupId>
                <artifactId>commons-fileupload</artifactId>
                <version>${commons.fileupload.version}</version>
            </dependency>

            <!-- excel工具 -->
            <dependency>
                <groupId>org.apache.poi</groupId>
                <artifactId>poi-ooxml</artifactId>
                <version>${poi.version}</version>
            </dependency>
        </dependencies>
    </dependencyManagement>

    <packaging>pom</packaging>

    <modules>
        <module>admin</module>
    </modules>

    <build>
        <plugins>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-compiler-plugin</artifactId>
                <version>3.1</version>
                <configuration>
                    <source>${java.version}</source>
                    <target>${java.version}</target>
                </configuration>
            </plugin>
        </plugins>
    </build>

</project>

```

修改后的 子模块的 pom 文件大致如下：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>
	<!--此处声明父模块-->
    <parent>
        <artifactId>demo</artifactId>
        <groupId>com.nuist</groupId>
        <version>1.0</version>
    </parent>

    <packaging>jar</packaging>

    <artifactId>admin</artifactId>
    <description>Demo project for Spring Boot</description>


    <properties>
        <java.version>1.8</java.version>
    </properties>
    <dependencies>
        <!-- spring-boot-devtools -->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-devtools</artifactId>
            <optional>true</optional> <!-- 表示依赖不会传递 -->
        </dependency>
    </dependencies>
 
</project>

```

以下创建其他几个相关模块，`common,framework,quartz,system`等相关模块，模块较多，仅演示一个模块的创建操作：

右击新建 common  module:

![image-20210720021056582](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/image-20210720021056582.png)



![image-20210720021450395](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/SpringBoot%E6%90%AD%E5%BB%BA%E5%A4%9A%E6%A8%A1%E5%9D%97%E9%A1%B9%E7%9B%AE11.png)

![](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/SpringBoot%E6%90%AD%E5%BB%BA%E5%A4%9A%E6%A8%A1%E5%9D%97%E9%A1%B9%E7%9B%AE12.png)

之后点击确定，finish即可。此时我们的common 也新建好了。我们可以进行相关配置啦！！！

![image-20210720021707383](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/SpringBoot%E6%90%AD%E5%BB%BA%E5%A4%9A%E6%A8%A1%E5%9D%97%E9%A1%B9%E7%9B%AE13.png)

下面我们依旧删除common module中对应的多余的文件 如下指出的内容，删除这些多余的文件，保留`common.iml`文件

![image-20210720021831706](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/SpringBoot%E6%90%AD%E5%BB%BA%E5%A4%9A%E6%A8%A1%E5%9D%97%E9%A1%B9%E7%9B%AE14.png)

在common模块中进行相关配置，删除pom.xml中的parent,改为如下内容

```xml
  <parent>
        <artifactId>demo</artifactId>
        <groupId>com.nuist</groupId>
        <version>1.0</version>
    </parent>
```

然后在父工程中新增，如下内容

```xml
    <modules>
        <module>admin</module>
        <module>common</module>
    </modules>
```

**之后所有的模块在创建的时候需要修改本模块的parent改为具体的父工程的配置，然后在父工程中加入该模块**



删除common 模块中的`resource`文件夹和`test`文件夹以及`CommonApplication`文件,因为我们整个项目仅需要一个启动类接口，即在`admin` 模块中，删除其他模块的启动类

删除framework模块中的`resource`文件夹和`test`文件夹以及`CommonApplication`文件,因为我们整个项目仅需要一个启动类接口

删除system模块中的`resource`文件夹和`test`文件夹以及`CommonApplication`文件,因为我们整个项目仅需要一个启动类接口

删除quartz模块中的`resource`文件夹和`test`文件夹以及`CommonApplication`文件,因为我们整个项目仅需要一个启动类接口.

具体新增后的目录如下：

![image-20210720023230722](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/SpringBoot%E6%90%AD%E5%BB%BA%E5%A4%9A%E6%A8%A1%E5%9D%97%E9%A1%B9%E7%9B%AE15.png)

​	如果需要在模块中引入其他模块代码，举例如在admin模块中引入其他模块，我们可以通过如下方式，引入：

```xml
 		<!--引入定时任务模块-->
        <dependency>
            <groupId>com.nuist</groupId>
            <artifactId>quartz</artifactId>
            <version>1.0</version>
        </dependency>
        <!--引入公用工具类模块-->
        <dependency>
            <groupId>com.nuist</groupId>
            <artifactId>common</artifactId>
            <version>1.0</version>
        </dependency>
```

此时我们已经搭建好多模块项目，我们来写一个测试案例代码，读取数据库中的文件

### 3.代码测试运行

SysUser.java 实体

```java
package com.nuist.system.entity;

import com.fasterxml.jackson.annotation.JsonIgnore;
import com.fasterxml.jackson.annotation.JsonProperty;
import com.nuist.common.BaseEntity;
import com.nuist.common.annotation.Excel;
import com.nuist.common.annotation.Excels;

import org.apache.commons.lang3.builder.ToStringBuilder;
import org.apache.commons.lang3.builder.ToStringStyle;

import javax.validation.constraints.Email;
import javax.validation.constraints.NotBlank;
import javax.validation.constraints.Size;
import java.util.Date;
import java.util.List;

/**
 * @author liuhuanhuan
 * @version 2.0
 * @date 2021/7/16
 * @description 用户对象 sys_user
 */
public class SysUser extends BaseEntity
{
    private static final long serialVersionUID = 1L;

    /** 用户ID */
    @Excel(name = "用户序号", cellType = Excel.ColumnType.NUMERIC, prompt = "用户编号")
    private Long userId;

    /** 部门ID */
    @Excel(name = "部门编号", type = Excel.Type.IMPORT)
    private Long deptId;

    /** 用户账号 */
    @Excel(name = "登录名称")
    private String userName;

    /** 用户昵称 */
    @Excel(name = "用户名称")
    private String nickName;

    /** 用户邮箱 */
    @Excel(name = "用户邮箱")
    private String email;

    /** 手机号码 */
    @Excel(name = "手机号码")
    private String phonenumber;

    /** 用户性别 */
    @Excel(name = "用户性别", readConverterExp = "0=男,1=女,2=未知")
    private String sex;

    /** 用户头像 */
    private String avatar;

    /** 密码 */
    private String password;

    /** 盐加密 */
    private String salt;

    /** 帐号状态（0正常 1停用） */
    @Excel(name = "帐号状态", readConverterExp = "0=正常,1=停用")
    private String status;

    /** 删除标志（0代表存在 2代表删除） */
    private String delFlag;

    /** 最后登录IP */
    @Excel(name = "最后登录IP", type = Excel.Type.EXPORT)
    private String loginIp;

    /** 最后登录时间 */
    @Excel(name = "最后登录时间", width = 30, dateFormat = "yyyy-MM-dd HH:mm:ss", type = Excel.Type.EXPORT)
    private Date loginDate;

    /** 部门对象 */
    @Excels({
        @Excel(name = "部门名称", targetAttr = "deptName", type = Excel.Type.EXPORT),
        @Excel(name = "部门负责人", targetAttr = "leader", type = Excel.Type.EXPORT)
    })
    private SysDept dept;

    /** 角色对象 */
    private List<SysRole> roles;

    /** 角色组 */
    private Long[] roleIds;

    /** 岗位组 */
    private Long[] postIds;

    public SysUser()
    {

    }

    public SysUser(Long userId)
    {
        this.userId = userId;
    }

    public Long getUserId()
    {
        return userId;
    }

    public void setUserId(Long userId)
    {
        this.userId = userId;
    }

    public boolean isAdmin()
    {
        return isAdmin(this.userId);
    }

    public static boolean isAdmin(Long userId)
    {
        return userId != null && 1L == userId;
    }

    public Long getDeptId()
    {
        return deptId;
    }

    public void setDeptId(Long deptId)
    {
        this.deptId = deptId;
    }

    @Size(min = 0, max = 30, message = "用户昵称长度不能超过30个字符")
    public String getNickName()
    {
        return nickName;
    }

    public void setNickName(String nickName)
    {
        this.nickName = nickName;
    }

    @NotBlank(message = "用户账号不能为空")
    @Size(min = 0, max = 30, message = "用户账号长度不能超过30个字符")
    public String getUserName()
    {
        return userName;
    }

    public void setUserName(String userName)
    {
        this.userName = userName;
    }

    @Email(message = "邮箱格式不正确")
    @Size(min = 0, max = 50, message = "邮箱长度不能超过50个字符")
    public String getEmail()
    {
        return email;
    }

    public void setEmail(String email)
    {
        this.email = email;
    }

    @Size(min = 0, max = 11, message = "手机号码长度不能超过11个字符")
    public String getPhonenumber()
    {
        return phonenumber;
    }

    public void setPhonenumber(String phonenumber)
    {
        this.phonenumber = phonenumber;
    }

    public String getSex()
    {
        return sex;
    }

    public void setSex(String sex)
    {
        this.sex = sex;
    }

    public String getAvatar()
    {
        return avatar;
    }

    public void setAvatar(String avatar)
    {
        this.avatar = avatar;
    }

	@JsonIgnore
    @JsonProperty
    public String getPassword()
    {
        return password;
    }

    public void setPassword(String password)
    {
        this.password = password;
    }

    public String getSalt()
    {
        return salt;
    }

    public void setSalt(String salt)
    {
        this.salt = salt;
    }

    public String getStatus()
    {
        return status;
    }

    public void setStatus(String status)
    {
        this.status = status;
    }

    public String getDelFlag()
    {
        return delFlag;
    }

    public void setDelFlag(String delFlag)
    {
        this.delFlag = delFlag;
    }

    public String getLoginIp()
    {
        return loginIp;
    }

    public void setLoginIp(String loginIp)
    {
        this.loginIp = loginIp;
    }

    public Date getLoginDate()
    {
        return loginDate;
    }

    public void setLoginDate(Date loginDate)
    {
        this.loginDate = loginDate;
    }

    public SysDept getDept()
    {
        return dept;
    }

    public void setDept(SysDept dept)
    {
        this.dept = dept;
    }

    public List<SysRole> getRoles()
    {
        return roles;
    }

    public void setRoles(List<SysRole> roles)
    {
        this.roles = roles;
    }

    public Long[] getRoleIds()
    {
        return roleIds;
    }

    public void setRoleIds(Long[] roleIds)
    {
        this.roleIds = roleIds;
    }

    public Long[] getPostIds()
    {
        return postIds;
    }

    public void setPostIds(Long[] postIds)
    {
        this.postIds = postIds;
    }

    @Override
    public String toString() {
        return new ToStringBuilder(this,ToStringStyle.MULTI_LINE_STYLE)
            .append("userId", getUserId())
            .append("deptId", getDeptId())
            .append("userName", getUserName())
            .append("nickName", getNickName())
            .append("email", getEmail())
            .append("phonenumber", getPhonenumber())
            .append("sex", getSex())
            .append("avatar", getAvatar())
            .append("password", getPassword())
            .append("salt", getSalt())
            .append("status", getStatus())
            .append("delFlag", getDelFlag())
            .append("loginIp", getLoginIp())
            .append("loginDate", getLoginDate())
            .append("createBy", getCreateBy())
            .append("createTime", getCreateTime())
            .append("updateBy", getUpdateBy())
            .append("updateTime", getUpdateTime())
            .append("remark", getRemark())
            .append("dept", getDept())
            .toString();
    }
}

```

SysUserMapper   

```java
package com.nuist.system.mapper;

import com.nuist.system.entity.SysUser;
import org.apache.ibatis.annotations.Mapper;
import org.apache.ibatis.annotations.Param;

import java.util.List;


/**
 * @author liuhuanhuan
 * @version 2.0
 * @date 2021/7/16
 * @description 用户表 数据层
 */
@Mapper
public interface SysUserMapper
{
    /**
     * 根据条件分页查询用户列表
     * 
     * @param sysUser 用户信息
     * @return 用户信息集合信息
     */
    public List<SysUser> selectUserList(SysUser sysUser);   
}
```

SysUserRoleService

```java
package com.nuist.system.service;

import com.nuist.system.entity.SysUser;

import java.util.List;


/**
 * @author liuhuanhuan
 * @version 2.0
 * @date 2021/7/16
 * @description 用户 业务层
 */
public interface ISysUserService
{
    /**
     * 根据条件分页查询用户列表
     * 
     * @param user 用户信息
     * @return 用户信息集合信息
     */
    public List<SysUser> selectUserList(SysUser user);
}

```

SysUserRoleServiceImpl

```java
package com.nuist.system.service.impl;

import com.nuist.common.annotation.DataScope;
import com.nuist.system.entity.SysUser;
import com.nuist.system.mapper.SysUserMapper;
import com.nuist.system.service.ISysUserService;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;


import java.util.List;
@Service
public class SysUserServiceImpl implements ISysUserService {

    private static final Logger log = LoggerFactory.getLogger(SysUserServiceImpl.class);

    @Autowired
    private SysUserMapper userMapper;

    /**
     * 根据条件分页查询用户列表
     *
     * @param user 用户信息
     * @return 用户信息集合信息
     */
    @Override
    @DataScope(deptAlias = "d", userAlias = "u")
    public List<SysUser> selectUserList(SysUser user)
    {
        return userMapper.selectUserList(user);
    }
}
```

TestContoller

```java
package com.nuist.test;

import com.nuist.common.controller.BaseController;
import com.nuist.common.core.TableDataInfo;
import com.nuist.system.entity.SysUser;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.security.access.prepost.PreAuthorize;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;
import com.nuist.system.service.ISysUserService;

import java.util.List;

@RestController
@RequestMapping("test")
public class TestController extends BaseController {

    @Autowired
    private ISysUserService sysUserService;

    /**
     * 获取用户列表
     */
    @PreAuthorize("@ss.hasPermi('system:user:list')")
    @GetMapping("/list")
    public TableDataInfo list(SysUser user)
    {
        startPage();
        List<SysUser> list = sysUserService.selectUserList(user);
        return getDataTable(list);
    }
}
```

![image-20210720040958130](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/SpringBoot%E6%90%AD%E5%BB%BA%E5%A4%9A%E6%A8%A1%E5%9D%97%E9%A1%B9%E7%9B%AE16.png)

即可测试成功！！！！



源代码地址：https://gitee.com/liuhuanhuan963019/spring-boot-module-demo.git

