---
title: java上传图片至阿里云oss服务器
tags:
  - Java
  - OSS
categories:
  - Java
toc: true
abbrlink: 7937
date: 2021-07-25 13:34:28
---



## 一、阿里云oss设置

在上传图片之前需要简单设置下阿里云oss服务器的相关配置

<!--more-->

进入oss终端页面：

![image-20210529231650235](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/%E9%98%BF%E9%87%8C%E4%BA%91oss01.png)

点击右下角的访问控制新增用户用于获取新增accesskeyid:

![image-20210529233457791](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/%E9%98%BF%E9%87%8C%E4%BA%91oss02.png)

点击左侧的用户新增：

![image-20210529233547705](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/%E9%98%BF%E9%87%8C%E4%BA%91oss03.png)

点击创建用户新增用户：

![image-20210529233701374](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/%E9%98%BF%E9%87%8C%E4%BA%91oss05.png)

点击创建AccessKey即可创建新key，此时会出现用于授权登录的keyecrets

![image-20210529233924094](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/%E9%98%BF%E9%87%8C%E4%BA%91oss06.png)

此时最关键的一步，我们需要创建我们需要的Bucket数据存储仓库，可以自定义显示名称，具体操作步骤详细见官网：

![image-20210529234229356](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/%E9%98%BF%E9%87%8C%E4%BA%91oss07.png)

此后需要给我们当前的用户授权，不然无法正常进行文件上传读写，点击用户，选择刚刚新增的用户，添加权限。

![image-20210529234533175](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/%E9%98%BF%E9%87%8C%E4%BA%91oss08.png)

下面下载官网软件，登录:输入刚刚保存的key与keyecrets选择刚刚新增的bucket实例，选择合适的地址。即可登录成功

![image-20210529234729864](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/%E9%98%BF%E9%87%8C%E4%BA%91oss09.png)

亲测有效，我的已经成功登录啦，前后花了不到1个小时，有兴趣的话可以研究下。

![image-20210529235055855](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/%E9%98%BF%E9%87%8C%E4%BA%91oss10.png)

此页面即为登录成功页面，可以选择本地上传，下面我们教大家一种新方式，使用java实现图片上传

## 二、java上传图片至阿里云oss服务器

下面贴出关键代码：具体修改根据自己实际情况：

**1.引入必须的库**

```java
<!--OSS-->
        <dependency>
            <groupId>com.aliyun.oss</groupId>
            <artifactId>aliyun-sdk-oss</artifactId>
            <version>2.4.0</version>
        </dependency>
        <dependency>
            <groupId>commons-fileupload</groupId>
            <artifactId>commons-fileupload</artifactId>
            <version>1.3.1</version>
        </dependency>
        <dependency>
            <groupId>org.jdom</groupId>
            <artifactId>jdom</artifactId>
            <version>1.1.3</version>
        </dependency>
```

**2.配置文件新增**

```java
aliyun:
  oss:
    file:
      endPoint: "http://oss-cn-beijing.aliyuncs.com"  // 一般不用改，选择自己的地址即可
      keyid: "保存的key"
      keyecrets: "保存的secret"
     #bucket可以在控制台创建，也可以使用java代码创建
      bucketname: "实例名称"
```

**3.java关键代码**

```java
package com.lhh.constant;

import org.springframework.beans.factory.InitializingBean;
import org.springframework.beans.factory.annotation.Value;
import org.springframework.stereotype.Component;

/**
 * @version 1.0
 * @date 2021/5/29 21:45
 */
@Component
public class OssConstant implements InitializingBean {
    @Value("${aliyun.oss.file.endPoint}")
    private String oss_file_endpoint;

    @Value("${aliyun.oss.file.keyid}")
    private String oss_file_keyid;

    @Value("${aliyun.oss.file.keysecret}")
    private String oss_file_keysecret;

    @Value("${aliyun.oss.file.bucketname}")
    private String oss_file_bucketname;



    public static String OSS_END_POINT_IM;
    public static String OSS_BUCKET_IM;
    public static String OSS_ACCESS_KEY_ID_IM;
    public static String OSS_ACCESS_KEY_SECRET_IM;

    @Override
    public void afterPropertiesSet() throws Exception {
        OSS_END_POINT_IM = oss_file_endpoint;
        OSS_BUCKET_IM = oss_file_bucketname;
        OSS_ACCESS_KEY_ID_IM = oss_file_keyid;
        OSS_ACCESS_KEY_SECRET_IM = oss_file_keysecret;
    }
}

```

```java
package com.lhh.oss;

import com.aliyun.oss.ClientException;
import com.aliyun.oss.OSSClient;
import com.aliyun.oss.OSSException;
import com.aliyun.oss.model.CannedAccessControlList;
import com.aliyun.oss.model.CreateBucketRequest;
import com.aliyun.oss.model.PutObjectRequest;
import com.aliyun.oss.model.PutObjectResult;
import com.lhh.constant.OssConstant;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

import java.io.File;
import java.text.SimpleDateFormat;
import java.util.Date;

/**
 * @version 1.0
 * @date 2021/5/29 21:48
 */
public class AliyunOSSUtil {
    private static final String accessKeyId= OssConstant.OSS_ACCESS_KEY_ID_IM;
    private static final String accessKeySecret=OssConstant.OSS_ACCESS_KEY_SECRET_IM;
    private static final String endpoint =  OssConstant.OSS_END_POINT_IM;
    private static final String bucket = OssConstant.OSS_BUCKET_IM;

    private static final Logger logger = LoggerFactory.getLogger(AliyunOSSUtil.class);

    public static String OSSUploadFile(String filename){
        SimpleDateFormat format = new SimpleDateFormat("yyyy-MM-dd");
        File file = new File(filename);
        String dateStr = format.format(new Date());
        if(null == file){
            return null;
        }
        OSSClient ossClient = new OSSClient(endpoint,accessKeyId,accessKeySecret);
        try {
            //容器不存在，就创建
            if(! ossClient.doesBucketExist(bucket)){
                ossClient.createBucket(bucket);
                CreateBucketRequest createBucketRequest = new CreateBucketRequest(bucket);
                createBucketRequest.setCannedACL(CannedAccessControlList.Default);
                ossClient.createBucket(createBucketRequest);
            }

            String fileUrl = dateStr + "/" + new Date().getTime()+"-"+file.getName();

            //上传文件
            PutObjectResult result = ossClient.putObject(new PutObjectRequest(bucket, fileUrl, file));
            //设置权限 这里是私有权限读写
            ossClient.setBucketAcl(bucket,CannedAccessControlList.Default);
            if(null != result){
                logger.info("==========>OSS文件上传成功,OSS地址："+fileUrl);
                return bucket+"/"+fileUrl;
            }
        }catch (OSSException oe){
            logger.error(oe.getMessage());
        }catch (ClientException ce){
            logger.error(ce.getMessage());
        }finally {
            //关闭
            ossClient.shutdown();
        }
        return null;
    }
}

```

测试代码：

```java
package com.lhh.controller;

import com.lhh.oss.AliyunOSSUtil;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RequestMethod;
import org.springframework.web.bind.annotation.RequestParam;
import org.springframework.web.bind.annotation.RestController;

/**
 * @version 1.0
 * @date 2021/5/29 21:52
 */
@RestController
@RequestMapping(value = "/oss")
public class OssController {


    @RequestMapping(value = "test",method = RequestMethod.GET)
    public String test(@RequestParam("filename") String filename) {
        String s = AliyunOSSUtil.OSSUploadFile(filename);
        return s;
    }
}
```

成功上传，具体代码依据自己实际情况。

此上为全部代码，感兴趣的朋友可以尝试下。
