---
title: 【java强化】java对list进行指定排序
tags:
  - Java
categories:
  - Java
toc: true
abbrlink: 31020
date: 2021-11-01 19:29:01
---



### 1.java传统表示方式

#### 1.1 对List<Integer>进行排序

<!--more-->

```java
		@Test
    public  void Test1() {
        List<Integer> list = new ArrayList<Integer>();
        list.add(new Integer(5));
        list.add(new Integer(13));
        list.add(new Integer(4));
        list.add(new Integer(9));
        Collections.sort(list);
        System.out.println(list.toString());
    }
```

输出结果

```java
[4, 5, 9, 13]
```

#### 1.2 对对象中指定元素进行排序

```java
 @Test
    public void Test2() {
        List<Student> list = new ArrayList<Student>();
        list.add(new Student("lhh",13));
        list.add(new Student("wcy",10));
        list.add(new Student("tw",25));
        Collections.sort(list);
        System.out.println(list.toString());
    }
    class Student implements Comparable<Student> {

        private String name; //姓名

        private int age; // 年龄

        public Student() {
        }

        public Student(String name, int age) {
            this.name = name;
            this.age = age;
        }

        public String getName() {
            return name;
        }

        public void setName(String name) {
            this.name = name;
        }

        public int getAge() {
            return age;
        }

        public void setAge(int age) {
            this.age = age;
        }

        @Override
        public String toString() {
            return "Student{" +
                    "name='" + name + '\'' +
                    ", age=" + age +
                    '}';
        }
        //重写Comparable接口的compareTo方法，
        // 根据年龄升序排列，降序修改相减顺序即可
        @Override
        public int compareTo(Student o) {
            return this.age-o.getAge();
        }
    }
```

输出结果

```java
[Student{name='wcy', age=10}, Student{name='lhh', age=13}, Student{name='tw', age=25}]
```

#### 1.3 通过匿名内部类的方式进行实现

```java
@Test
    public void Test3() {
        List<Student> list = new ArrayList<Student>();
        list.add(new Student("lhh",13));
        list.add(new Student("wcy",10));
        list.add(new Student("tw",25));
        Collections.sort(list, new Comparator<Student>() {
            @Override
            public int compare(Student o1, Student o2) {
                int diff = o1.getAge() - o2.getAge();
                if (diff > 0) {
                    return 1;
                }else if (diff < 0) {
                    return -1;
                }
                    return 0; //相等为0
                }
        });
        System.out.println(list.toString());
    }
```

输出结果

```java
[Student{name='wcy', age=10}, Student{name='lhh', age=13}, Student{name='tw', age=25}]
```

### 2.使用java8新特性

`demo1`:

```java
@Test
    public void lambdaTest1(){
        List<User> list = new ArrayList<>();
        list.add(new User(1,"张三"));
        list.add(new User(4,"赵六"));
        list.add(new User(2,"李四"));
        list.add(new User(3,"王五"));

        //条件删除
        list.removeIf(user -> user.getUserId() == 3);
        System.out.println("--------------排序前");
        list.forEach(user -> {
            System.out.println(user);
        });
        list.sort((user1,user2)->user1.getUserId() - user2.getUserId());
        System.out.println("_-------------------正序排序后");
        list.forEach(user -> {
            System.out.println(user);
        });

        System.out.println("--------------------倒序排序后：");
        list.sort((((o1, o2) -> o2.getUserId() - o1.getUserId())));
        list.forEach(user -> {
            System.out.println(user);
        });
    }



    class User{
        private Integer userId;
        private String userName;



        public Integer getUserId() {
            return userId;
        }

        public void setUserId(Integer userId) {
            this.userId = userId;
        }

        public String getUserName() {
            return userName;
        }

        public void setUserName(String userName) {
            this.userName = userName;
        }

        public User(Integer userId, String userName) {
            this.userId = userId;
            this.userName = userName;
        }

        public User() {
        }

        @Override
        public String toString() {
            return "User{" +
                    "userId=" + userId +
                    ", userName='" + userName + '\'' +
                    '}';
        }
    }
```

`demo2`

对获取到站点的降雨值进行排序. 这个是重要的排序思想，可以参考下

```java
List<RadarPre> collect = allStationData.stream().map(stationInfo -> {
            String param1 = "";
            String rain = HttpUtils.sendGet("x x x x", param1);
            RadarPre radarPre = new RadarPre();
            radarPre.setRain(Double.valueOf(rain));
            radarPre.setStationId(stationInfo.getStationCode());
            radarPre.setStationName(stationInfo.getStationName());
            radarPre.setLatitude(stationInfo.getLatitude());
            radarPre.setLongitude(stationInfo.getLongitude());
            return radarPre;
        }).sorted(Comparator.comparing(RadarPre::getRain).reversed()).limit(3).collect(Collectors.toList());
```

