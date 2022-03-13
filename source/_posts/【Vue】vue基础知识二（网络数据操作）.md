---
title: 【Vue】vue基础知识二（网络数据操作）
tags:
  - Vue
categories:
  - Vue
toc: true
abbrlink: 29850
date: 2021-07-25 12:30:57
---



### **axios**

**(1.先导入后使用 2.使用get和post即可发送相应的请求**

**3.then方法中的回调函数会在请求成功和失败时触发**

**4.通过回调函数的形参可以获取响音内容或错误信息)**

<!--more-->

**功能强大的网络请求库**

```javascript
<Script src="https://unpkg.com/axios/dist/axios.min.js"></script>
axios.get(地址).then(function(response){},function(err){})
```



### **axios文档地址：**

**https://github.com/axios/axios**

```javascript
 <input type="button" value="get请求" class="get">
    <input type="button" value="post请求" class="post">
    <!--在线axios地址-->
<!--    <script src="https://cdn.bootcdn.net/ajax/libs/axios/0.1.0/axios.amd.min.js"></script>-->
    <script src="https://unpkg.com/axios@0.20.0/dist/axios.min.js"></script>
    <script>
        /**
         * 接口1：随机笑话
         * 请求地址：https://autumnfish.cn/comment/music?id=186016
         * 请求方法：get
         * 请求参数
         * 相应内容评论
        * */
        document.querySelector(".get").onclick = function () {
            // axios.get("https://autumnfish.cn/comment/music?id=186016&limit=1")
             axios.get("https://autumnfish.cn/api/joke/list?num=3")
            .then(function (response) {
                    console.log(response);
            },function (error) {
                    console.log(error);
            })
        }

        /*
        * 接口2：用户注册
        * 请求地址：https://autumnfish.cn/api/user/reg
        * 请求方法：post
        * 请求参数：user(用户名，密码)
        * 相应内容（注册成功和失败）
        * */
        document.querySelector(".post").onclick = function () {
            axios.post("https://autumnfish.cn/api/user/reg",{username:"刘欢欢"})
            .then(function (response) {
                    console.log(response);
            },function (error) {
                    console.log(error);
            })
        }
    </script>
```



### axios+vue（）

```javascript
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>

<body>

    <div class="wrap">
        <!--播放器主题部分-->
        <div class="play_wrap" id="app">
            <div class="search_bar">
                <!--搜索歌曲-->
                <input type="text" autocomplete="off" v-model="query" placeholder="请输入歌曲"
                @keyup.enter="getMusic">
            </div>
            <div class="center_on">
                <!--搜索歌曲列表-->
                <div class="song_wrapper">
                    <ul class="song_list">
                        <li v-for="item in music">
                            <input type="button" value="播放" @click="playMusic(item.id)">
                            <b>{{item.name}}</b>
                            <span v-if="item.mvid!=0 ">
                                <button @click="playMv(item.mvid)">mv</button>
                            </span>
                        </li>
                    </ul>
<!--                    <button class="switch_btn">播放</button>-->
<!--                    <img src="./7665665492ce4861d66c4b7df2491779.jpeg" class="switch_btn" alt="">-->
                </div>
                <!--歌曲信息容器-->
                <div class="player_con" :class="{playing:isplaying}">
<!--                    <img src="./7665665492ce4861d66c4b7df2491779.jpeg" class="play_bar">-->
                    <!--黑胶图片-->
<!--                    <img src="./7665665492ce4861d66c4b7df2491779.jpeg" class="play_bar">-->
                    <img :src="musicCover" class="cover_autoRotate">
                </div>
                <!--歌曲评论容器-->
                <div class="comment_wrapper">
                    <h5 class="title">热门留言</h5>
                    <div class="comment_list">
                        <dl v-for="item in hotComment">
                            <dt><img :src="item.user.avatarUrl" alt=""></dt>
                            <dd class="name">{{item.nickname}}</dd>
                            <dd class="detail">{{item.content }}</dd>
                        </dl>
                    </div>
                </div>
            </div>
            <div class="audio_con">
                <!--v-bind绑定元素：-->
                <audio ref="audio" @play="play" @pause="pause " :src="musicUrl"  controls autoplay loop class="myaudio"></audio>
            </div>
            <div class="video_con" v-show="isShow" style="display: none;">
                <video :src="mvUrl" controls="controls"></video>
                <div class="mask" @click="hide"></div>
            </div>
        </div>
    </div>

    <!--在线axios地址-->
    <!--<script src="https://cdn.bootcdn.net/ajax/libs/axios/0.1.0/axios.amd.min.js"></script>-->
    <script src="https://unpkg.com/axios@0.20.0/dist/axios.min.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
    <script>
        /*
        * 请求地址：https://autumnfish.cn/search
        * 请求方式：get
        * 请求参数：keywords
        * 返回参数：歌曲名称搜索
        * */
        var app = new Vue({
            el:"#app",
            data:{
                query:"",
                music:[],
                musicUrl:"",
                musicCover:"",
                hotComment:[],
                isplaying:false,
                isShow:false,   //遮罩层显示与否
                mvUrl:""  //mv地址
            },
            methods:{
                <!--获取music-->
                getMusic:function () {
                    var that = this;
                    axios.get("https://autumnfish.cn/search?keywords="+this.query)
                    .then(function (response) {
                        that.music = response.data.result.songs;
                    },function (error) {})
                },
                <!--播放音乐-->
                playMusic:function (id) {
                    var that = this;
                    //获取歌曲地址
                    axios.get("https://autumnfish.cn/song/url?id="+id)
                    .then(function (response) {
                        // console.log(response);
                       that.musicUrl = response.data.data[0].url;
                    },function (error) {
                    })
                    //歌曲详情获取
                    axios.get("https://autumnfish.cn/song/detail?ids="+id)
                    .then(function (response) {
                        that.musicCover = response.data.songs[0].al.picUrl;
                    },function (error) {})
                    //歌曲评论获取
                    axios.get("https://autumnfish.cn/comment/hot?type=0&id="+id)
                        .then(function (response) {
                            that.hotComment = response.data.hotComments;
                        },function (error) {})
                },
                play:function () {
                    this.isplaying=true;
                },
                pause:function () {
                    this.isplaying=false;
                },
                <!--播放mv-->
                playMv:function (id) {
                    var that = this;
                    axios.get("https://autumnfish.cn/mv/url?id="+id)
                    .then(function (response) {
                        console.log(response);
                        that.isShow = true;
                        that.mvUrl = response.data.data.url;
                    },function (error) {})
                },
                hide:function () {
                    this.isShow=false;
                }
            }
        })
    </script>
</body>
</html>
```

