---
title: 【Vue】vue基础知识一（本地数据操作）
tags:
  - Vue
categories:
  - Vue
toc: false
abbrlink: 62539
date: 2021-07-25 12:32:08
---

javaScript  框架

简化Dom的操作

响应式数据驱动

<!--more-->

简单的vue程序：

1.导入开发版本的vue.is

2.创建vue实例对象，设置el属性和data属性

3.使用简介的模版语法把数据渲染到页面上

vue实例可以使用双标签挂载，不能使用HTML和BODy来进行

**v-text .    设置标签的文本值  (覆盖标签中全部的内容el只会替换相应的值)**

```javascript
<div id="app">
        <h1 v-text="message"></h1>
        <h1 v-text="message+'!'"></h1>
        <h1>我的  {{Student.name}}</h1>
    </div>
    <!-- 开发环境版本，包含了有帮助的命令行警告 -->
    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
    <script>
        var app = new Vue({
            el: "#app",
            data:{
                message:"hello world",
                Student:{
                    name:"二狗子",
                    age:12
                },
                score:[12,32,4,32]
            }
        })
    </script>
```



**v-html (1.内容中有html结构会被解析成标签 2.设置元素的innerHTML)**

注：解析文本使用 v-text .   解析hml使用v-html

```javascript
<div id="app">
    <p v-html="context"></p>
    <p v-text="context"></p>
</div>
<!-- 开发环境版本，包含了有帮助的命令行警告 -->
<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
<script>
    var app = new Vue({
        el: "#app",
        data:{
           context:"<a href='http://www.baidu.com'>我的一个小demo<a>"
        }
    })
</script>
```



**v-on(1.为元素绑定事件，2.事件名不需要写on,3.指令可以简写@ 4.绑定的方法定义在methods属性中5.方法内部可以通过this关键字访问定义data中的数据)**

```javascript
<div id="app">
    <input type="button" value="点我" v-on:click="clickIt">
    <input type="button" value="点我2" @click="clickIt">
    <input type="button" value="点我3" @dblclick="clickIt">
    <h2 @click="changeLOve">{{message}}</h2>
</div>
<!-- 开发环境版本，包含了有帮助的命令行警告 -->
<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
<script>
    var app = new Vue({
        el: "#app",
        data: {
            message:"我爱你"
        },
        methods:{
            clickIt:function () {
                alert("王彩云，我爱你！！！");
            },
            changeLOve:function () {
                this.message = "永远";
                console.log(this.message);
            }
        }
    })
</script>
```



**计数器（创建实例v-on事件和方法绑定，实时更改数据）**

```javascript
<div id="app">
    <button @click="sub">-</button>
    <span>{{number}}</span>
    <button @click="add">+</button>
</div>
<!-- 开发环境版本，包含了有帮助的命令行警告 -->
<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
<script>
    var app = new Vue({
        el: "#app",
        data: {
            number:1
        },
        methods:{
            sub:function () {
                if(this.number<0){
                    alert("已经是最小的啦！！");
                }else{
                    this.number--;
                }
            },
            add:function () {
                if(this.number>=10){
                    alert("已经是最大的啦！！");
                }else{
                    this.number++;
                }
            }
        }
    })
</script>
```



**v-show(1.根据元素的真假切换元素的显示状态 2.原理是修改元素的display实现元素的隐藏)**

```javascript
<div id="app">
    <input type="button" value="切换显示" @click="changeIsShow">
    <input type="button" value="年龄增加" @click="addAge">
    <img v-show="isShow" src="IMG_6626.JPG" alt="">
    <img v-show="age>=25" src="IMG_6626.JPG" alt="">
</div>
<!-- 开发环境版本，包含了有帮助的命令行警告 -->
<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
<script>
    var app = new Vue({
        el: "#app",
        data: {
            isShow:false,
            age:20
        },
        methods:{
            changeIsShow:function () {
                this.isShow = !this.isShow;
                console.log(isShow);
            },
            addAge:function () {
                this.age++;
                console.log(this.age);
            }
        }
    })
</script>
```



**v-if(1.根据表达式的真假切换元素的显示状态 2.本质是操作dom 3.表达式的值是true时，元素存在于dom树中，为否是从dom树中移除)**

**注：v-show和v-if的区别：**

**v-show：只是改变了display属性的操作**

**v-if：改变的是dom数**

**实际情况 频繁切换的使用v-show**

```javascript
<div id="app">
    <input type="button" value="切换显示" @click="toggleisShow">
    <p v-if="isShow">我爱你呀</p>
    <p v-show="isShow">我爱你呀 v-show显示</p>
    <h2 v-if="temperature>40">热死算了</h2>
</div>
<!-- 开发环境版本，包含了有帮助的命令行警告 -->
<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
<script>
    var app = new Vue({
        el: "#app",
        data: {
            isShow:false,      xx  
            temperature:39
        },
        methods:{
            toggleisShow:function () {
                this.isShow = !this.isShow;
            }
        }
    })
</script>
```



**v-bind (1.为元素绑定属性 2.完整写法v-bind:属性名 3.简写的话可以只写:属性名)**

```javascript
<div id="app">
    <img v-bind:src="imgSrc" alt="">
    <br>
    <img :src="imgSrc" alt="" :title="imgTItle">
    <br>
    <img :src="imgSrc" :title="imgTItle" :class="isActive?'active ':''" @click="toggleActive">
    <img :src="imgSrc" :title="imgTItle" :class="{active:isActive}" @click="toggleActive">
</div>
<!-- 开发环境版本，包含了有帮助的命令行警告 -->
<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
<script>
    var app = new Vue({
        el:"#app",
        data:{
            imgSrc:"http://www.itheima.com/images/logo.png",
            imgTItle:"我的哈哈",
            isActive:false
        },
        methods:{
            toggleActive:function () {
                this.isActive = !this.isActive;
            }
        }
    })
</script>
```


**图片切换（1.用数组来存放元素 2.用v-on来绑定事件 3.用v-bing来修改元素的属性）**

```javascript
<div id="app">
    <div class="center">
        <img :src="arrayl[index]" alt="">
        <a href="javaScript:void(0)" v-show="index!=0"
           @click="prev" class="left">
            <img src="左箭头.jpeg">
        </a>
        <a href="javaScript:void(0)" v-show="index<arrayl.length-1"
           @click="back" class="right">
            <img src="右箭头.jpg">
        </a>
    </div>
</div>
<!-- 开发环境版本，包含了有帮助的命令行警告 -->
<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
<script>
    var app = new Vue({
        el:"#app",
        data:{
            arrayl:[
                "IMG_6626.JPG",
                "IMG_20190213_221749.jpg",
                "IMG_20190214_171354.JPG",
                "IMG_20190214_224520.jpg",
                "IMG_20190214_224523.jpg",
                "IMG_20190216_185419.jpg",
            ],
            index:0
        },
        methods:{
            prev:function () {
                this.index--;
            },
            back:function () {
                this.index++;
            }
        }
    })
</script>
```



**v-for(1.根据数据生成列表 2.v-for长和)**

```javascript
<div id="app">    <button @click="add">点我➕</button>    <button @click="del">点我➖</button>    <ul>        <li v-for="item in name">{{item }}</li>    </ul>    <h2 v-for="item2 in score">{{item2}}</h2></div><!-- 开发环境版本，包含了有帮助的命令行警告 --><script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script><script>   var app = new Vue({     el:"#app",     data:{         name:[             "狗子",             "傻狗",             "老婆",             "胖胖"         ],         score:[             21,32,54,743         ]     },       methods:{         add:function () {            this.score.push(100);         },           del:function () {                this.score.shift()           }       }   })</script>
```



**v-on (补充)（1.时间绑定的方法写成函数调用的形式，可以传入自定义参数**

**2.定义方法时定义形参数来接受传入的实参**

**3.通过.修饰符可以对事件进行限制）**

**例如：@keyup.enter**

```javascript
<div id="app">    <input type="button" value="click me" @click="doIt(1,2)">    <input type="text" @keyup.enter="sayHi"></div><!-- 开发环境版本，包含了有帮助的命令行警告 --><script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script><script>    var app = new Vue({        el:"#app",        methods:{            doIt:function (p1,p2) {                console.log(p1);                console.log(p2);            },            sayHi:function () {                alert("我好想你！！！");            }        }    })</script>
```



**v-model(1.便捷的设置和获取表单元素的值**

**2.绑定的数据会和表单元素值相关联**

**3. 表单的 数据=绑定的数据)**

```
<div id="app">    <input type="button" value="click me" @click="changeMessage">    <input type="text" v-model="message" @keyup.enter="getA">    <h2>{{message}}</h2></div><!-- 开发环境版本，包含了有帮助的命令行警告 --><script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script><script>    var app = new Vue({        el:"#app",        data:{            message:"二狗子我好想你啊"        },        methods:{            getA:function () {                alert(this.message);            },            changeMessage:function () {                this.message = "我真的好想你啊"            }        }    })</script>
```



**记事本实战演练(1.增加 2.删除 3.隐藏 4.清空 )**

**注：shift()函数删除的是数组中的第一个元素 使用splice删除指定的某个元素**

```javascript
<!--主题区域--><section id="app">    <!--输入框-->    <header class="header">        <h1>欢欢笔记本</h1>        <input type="text" autocomplete="off" autofocus="autofocus"               placeholder="请输入" class="new-todo" v-model="inputValue"               @keyup.enter="add">        <!--列表区域-->        <section class="main" v-show="list.length!=0">            <ul class="todo-list">                <li class="todo" v-for="(item,index) in list">                    <span class="index">{{index+1}}.</span>                    <label class="item">{{item}}</label>                    <button class="destroy" @click="del(index)">del</button>                </li>            </ul>        </section>        <!--统计和清空-->        <footer class="footer" v-show="list.length!=0">            <span class="todo-count" v-if="list.length!=0">        <strong>{{list.length}}</strong>items left             </span>            <button class="clear-completed" @click="clear">clear</button>        </footer>    </header></section><!--底部文件--><footer class="info"></footer><!-- 开发环境版本，包含了有帮助的命令行警告 --><script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script><script>    var app = new Vue({        el:"#app",        data:{            list:["语文","高数","政治","外语"],            inputValue:"你是我的人了"        },        methods:{            add:function () {                this.list.push(this.inputValue);            },            del:function (index) {                this.list.splice(index,1);            },            clear:function () {                this.list=[];            }        }    })</script>
```



