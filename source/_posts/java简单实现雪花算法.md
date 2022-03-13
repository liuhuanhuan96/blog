---
title: java简单实现雪花算法
tags:
  - Java
  - 算法
categories:
  - Java
  - 算法
toc: true
abbrlink: 37664
date: 2021-11-01 19:32:45
---



## 一、介绍

`SnowFlake `算法，是 Twitter 开源的分布式 id 生成算法.其核心思想就是：使用一个 64 bit 的 long 型的数字作为全局唯一 id。在分布式系统中的应用十分广泛，且 ID 引入了时间戳，基本上保持自增。

<!--more-->

这 64 个 bit 中，其中 第一个表示符位号，然后用其中的 41 bit 作为毫秒数，用 10 bit 作为工作机器 id，12 bit 作为序列号。

例如：

![image-20211024232225798](https://img-blog.csdnimg.cn/img_convert/9e68b8126240ed4baf241de66346f3e0.png)

- 第一个部分，是 1 个 bit：0，这个是符号位。
  因为二进制里第一个 bit 如果是 1，那么都是负数，但是我们生成的 id 都是正数，所以第一个 bit 统一都是 0

- 第二个部分是 41 个 bit：表示的是时间戳

  41 bit 可以表示的数字多达 2 41 − 1 2^{41} - 12  41−1，也就是可以标识 2 41 − 1 2^{41}-12 41
   −1 个毫秒值，换算成年就是表示 69 年的时间

- 第三个部分是 5 个 bit：表示的是机房 id，10001代表的是这个服务最多可以部署在 2 5 2^{5}2 5个机房（32个机房）

- 第四个部分是 5 个 bit：表示的是机器 id，11001代表的是这个每个机房最多可以部署 2 5 2^{5}2 5个机器（32个机器）

- 第五个部分是 12 个 bit：表示的序号，就是某个机房某台机器上这一毫秒内同时生成的 id 的序号，0000 00000000 12 bit 可以代表的最大正整数是 2 12 − 1 = 4096 2 ^ {12} - 1 = 40962 12 −1=4096，也就是说可以用这个 12 bit 代表的数字来区分同一个毫秒内的 4096 个不同的 id

简单来说，你的某个服务假设要生成一个全局唯一 id，那么就可以发送一个请求给部署了 SnowFlake 算法的系统，由这个 SnowFlake 算法系统来生成唯一 id。

这个 SnowFlake 算法系统首先肯定是知道自己所在的机房和机器的，比如机房 id = 17，机器 id = 12。

接着 SnowFlake 算法系统接收到这个请求之后，首先就会用二进制位运算的方式生成一个 64 bit 的 long 型 id，64 个 bit 中的第一个 bit 是无意义的。

接着 41 个 bit，就可以用当前时间戳（单位到毫秒），然后接着 5 个 bit 设置上这个机房 id，还有 5 个 bit 设置上机器 id。

最后再判断一下，当前这台机房的这台机器上这一毫秒内，这是第几个请求，给这次生成 id 的请求累加一个序号，作为最后的 12 个 bit。

最终一个 64 个 bit 的 id 就出来了

这个算法可以保证说，一个机房的一台机器上，在同一毫秒内，生成了一个唯一的 id。可能一个毫秒内会生成多个 id，但是有最后 12 个 bit 的序号来区分开来。

## 二、特点

SnowFlake算法的优点：

- 高性能高可用：生成时不依赖于数据库，完全在内存中生成
- 容量大：每秒中能生成数百万的自增 ID
- ID自增：存入数据库中，索引效率高

SnowFlake算法的缺点：

- 依赖与系统时间的一致性，如果系统时间被回调，或者改变，可能会造成id冲突或者重复



## 三、算法实现

```java
public class SnowFlake {
    // 起始的时间戳
    private final static long START_STMP = 1577808000000L; //2020-01-01
    // 每一部分占用的位数，就三个
    private final static long SEQUENCE_BIT = 12; //序列号占用的位数private final static long MACHINE_BIT = 5; //机器标识占用的位数private final static long DATACENTER_BIT = 5; //数据中心占用的位数
    // 每一部分最大值
    private final static long MAX_DATACENTER_NUM = -1L ^ (-1L << DATACENTER_BIT);
    private final static long MAX_MACHINE_NUM = -1L ^ (-1L << MACHINE_BIT); private final static long MAX_SEQUENCE = -1L ^ (-1L << SEQUENCE_BIT);
    // 每一部分向左的位移
    private final static long MACHINE_LEFT = SEQUENCE_BIT;
    private final static long DATACENTER_LEFT = SEQUENCE_BIT + MACHINE_BIT;
    private final static long TIMESTMP_LEFT = DATACENTER_LEFT + DATACENTER_BIT; private long datacenterId; //数据中心
    private long machineId; //机器标识
    private long sequence = 0L; //序列号private long lastStmp = -1L; //上一次时间戳

    public SnowFlake(long datacenterId, long machineId) {
        if (datacenterId > MAX_DATACENTER_NUM || datacenterId < 0) {
            throw new IllegalArgumentException("datacenterId can't be greater than MAX_DATACENTER_NUM or less than 0");
        }
        if (machineId > MAX_MACHINE_NUM || machineId < 0) {
            throw new IllegalArgumentException("machineId can't be greater than MAX_MACHINE_NUM or less than 0");
        }
        this.datacenterId = datacenterId; this.machineId = machineId;
    }

    //产生下一个ID
    public synchronized long nextId() {
        long currStmp = timeGen(); if (currStmp < lastStmp) {
            throw new RuntimeException("Clock moved backwards. Refusing to generate id");
        }

        if (currStmp == lastStmp) {
//if条件里表示当前调用和上一次调用落在了相同毫秒内，只能通过第三部分，序列号自增来判断为唯一，所以+1. sequence = (sequence + 1) & MAX_SEQUENCE;
//同一毫秒的序列数已经达到最大，只能等待下一个毫秒     if (sequence == 0L) {
            currStmp = getNextMill();
        }
    } else {
//不同毫秒内，序列号置为0
//执行到这个分支的前提是currTimestamp > lastTimestamp，说明本次调用跟上次调用对比，已经不再同一个毫秒内了，这个时候序号可以重新回置0了。
        sequence = 0L;
    }

    lastStmp = currStmp;
//就是用相对毫秒数、机器ID和自增序号拼接
return (currStmp - START_STMP) << TIMESTMP_LEFT //时间戳部分
| datacenterId << DATACENTER_LEFT //数据中心部分
| machineId << MACHINE_LEFT //机器标识部分
| sequence;	//序列号部分
}

    private long getNextMill() { long mill = timeGen(); while (mill <= lastStmp) { mill = timeGen();
    }
        return mill;
    }

    private long timeGen() {
        return System.currentTimeMillis();
    }
}
```

生成配置

```java
Configuration
public class WebMvcConfig implements WebMvcConfigurer {

@Autowired
public void configureMessageConverters(List<HttpMessageConverter<?>> converters) { converters.add(toStringConverter());
}

/**
*	BigDecimal Long 转化为String
*
*	@return
*/ @Bean
public MappingJackson2HttpMessageConverter toStringConverter() { MappingJackson2HttpMessageConverter converter = new MappingJackson2HttpMessageConverter(); ObjectMapper mapper = new ObjectMapper();
SimpleModule simpleModule = new SimpleModule(); simpleModule.addSerializer(BigDecimal.class, BigDecimalToStringSerializer.instance); simpleModule.addSerializer(Long.class, ToStringSerializer.instance); simpleModule.addSerializer(Long.TYPE, ToStringSerializer.instance); simpleModule.addSerializer(long.class, ToStringSerializer.instance); mapper.registerModule(simpleModule);
// Include.Include.ALWAYS 默认
// Include.NON_DEFAULT 属性为默认值不序列化
// Include.NON_EMPTY 属性为 空（""） 或者为 NULL 都不序列化，则返回的json是没有这个字段的。这样对移动端会更省流量
// Include.NON_NULL 属性为NULL 不序列化
mapper.setSerializationInclusion(JsonInclude.Include.NON_NULL);
mapper.configure(DeserializationFeature.FAIL_ON_UNKNOWN_PROPERTIES, false); mapper.configure(JsonParser.Feature.ALLOW_UNQUOTED_CONTROL_CHARS, true);// 允许出现特殊字符和转义符mapper.configure(JsonParser.Feature.ALLOW_SINGLE_QUOTES, true); // 允许出现单引号

converter.setObjectMapper(mapper);

return converter;
}

@JacksonStdImpl
static class BigDecimalToStringSerializer extends ToStringSerializer {
public final static BigDecimalToStringSerializer instance = new BigDecimalToStringSerializer();

public BigDecimalToStringSerializer() { super(Object.class);
}

public BigDecimalToStringSerializer(Class<?> handledType) { super(handledType);
}

@Override
public boolean isEmpty(SerializerProvider prov, Object value) { if (value == null) {
return true;
}
String str = ((BigDecimal) value).stripTrailingZeros().toPlainString(); return str.isEmpty();
}

@Override
public void serialize(Object value, JsonGenerator gen, SerializerProvider provider) throws IOException {
gen.writeString(((BigDecimal) value).stripTrailingZeros().toPlainString());
}

@Override
public JsonNode getSchema(SerializerProvider provider, Type typeHint) throws JsonMappingException { return createSchemaNode("string", true);
}

@Override
public void serializeWithType(Object value, JsonGenerator gen, SerializerProvider provider, TypeSerializer typeSer)
throws IOException {
// no type info, just regular serialization serialize(value, gen, provider);
}
}
}

```



参考文章：https://blog.csdn.net/dreaming_coder/article/details/116542633?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522163508968716780366545515%2522%252C%2522scm%2522%253A%252220140713.130102334.pc%255Fblog.%2522%257D&request_id=163508968716780366545515&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~blog~first_rank_v2~rank_v29-1-116542633.pc_v2_rank_blog_default&utm_term=%E9%9B%AA%E8%8A%B1&spm=1018.2226.3001.4450
