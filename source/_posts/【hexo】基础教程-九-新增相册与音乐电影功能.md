---
title: 【hexo】基础教程-九-新增相册与音乐电影功能
copyright_author: 刘先森
copyright_author_href: 'https://novoice.top'
copyright_url: 'https://novoice.top'
copyright_info: 此文章版權歸刘先森所有，如有轉載，請註明來自原作者
abbrlink: 6c2846a4
date: 2022-03-12 10:00:42
tags:
  - Hexo
categories:
  - Hexo
top_img: 'https://cdn.jsdelivr.net/gh/HCLonely/hclonely.github.io/img/Butterfly/029.webp'
copyright: true
cover: 'https://cdn.jsdelivr.net/gh/HCLonely/hclonely.github.io/img/Butterfly/029.webp'
swiper_index: 5
toc: true
---

## 一、新增相册

[首先参考官网新增相册方式](https://butterfly.js.org/posts/4aa8abbe/#Gallery%E7%9B%B8%E5%86%8A%E5%9C%96%E5%BA%AB)

然后我们在hexo项目的根目录下执行如下代码

```shell
hexo new page "gallery"
```

然后会在  `你的博客/source`  下新增一个`gallery/index.md`

此时我们的page 已经生成好了

我们在当前的的index目录中新增如下代码

```markdown
---
title: 相册集
date: 2020-04-21 18:44:23
description:
type: gallery 
top_img: 'https://cdn.jsdelivr.net/gh/HCLonely/hclonely.github.io/img/Butterfly/005.webp'

---

<div class="gallery-group-main">
{% galleryGroup '壁紙' '收藏的一些壁紙' '/gallery/wallpaper' https://i.loli.net/2019/11/10/T7Mu8Aod3egmC4Q.png %}
{% galleryGroup '漫威' '關於漫威的圖片' '/gallery/marvel' https://i.loli.net/2019/12/25/8t97aVlp4hgyBGu.jpg %}
{% galleryGroup 'OH MY GIRL' '關於OH MY GIRL的圖片' '/gallery/ohmygirl' https://i.loli.net/2019/12/25/hOqbQ3BIwa6KWpo.jpg %}
</div>
```

`galleryGroup`代表的是一个相册合集，目录存放地址在/gallery/wallpaper目录下

此时我们在 `你的博客/source/gallery`下新增一个目录`wallpaper`

在`wallpaper`中新增一个`index.md`,然后将我们需要展示的图片放在md文档中，这里借用官方文档的方式来进行描述

```markdown
{% gallery %}
![](https://i.loli.net/2019/12/25/Fze9jchtnyJXMHN.jpg)
![](https://i.loli.net/2019/12/25/ryLVePaqkYm4TEK.jpg)
![](https://i.loli.net/2019/12/25/gEy5Zc1Ai6VuO4N.jpg)
![](https://i.loli.net/2019/12/25/d6QHbytlSYO4FBG.jpg)
![](https://i.loli.net/2019/12/25/6nepIJ1xTgufatZ.jpg)
![](https://i.loli.net/2019/12/25/E7Jvr4eIPwUNmzq.jpg)
![](https://i.loli.net/2019/12/25/mh19anwBSWIkGlH.jpg)
![](https://i.loli.net/2019/12/25/2tu9JC8ewpBFagv.jpg)
{% endgallery %}
```

最后我们查看下效果：

<img src="https://tva1.sinaimg.cn/large/e6c9d24egy1h071b9lg5nj21ck0so0zk.jpg" alt="image-20220312132859702" style="zoom: 25%;" />

<img src="https://tva1.sinaimg.cn/large/e6c9d24egy1h071bscumgj21dm0sigs4.jpg" alt="image-20220312132929960" style="zoom:25%;" />



## 二、新增音乐

我们在hexo项目的根目录下执行如下代码

```shell
hexo new page "music"
```

然后会在  `你的博客/source`  下新增一个`music/index.md`

此时我们的page 已经生成好了

我们在当前的的index目录中新增如下代码

```mar
---
title: Music
date: 2020-04-23 12:58:56
type: 'music'
top_img: https://gitlab.com/valetzx/img/raw/main/img/2022/02/25_22_28_59_%E9%BA%A6%E7%94%B0.png
cover: https://gitlab.com/valetzx/img/raw/main/img/2022/02/25_22_28_59_%E9%BA%A6%E7%94%B0.png
swiper_index: 995
swiper_desc: 歌单推荐
swiper_cover: https://gitlab.com/valetzx/img/raw/main/img/2022/02/25_22_28_59_%E9%BA%A6%E7%94%B0.png

---

# [我的QQ音乐歌单](https://c.y.qq.com/base/fcgi-bin/u?__=8Gjfefjj4DYo)

{% meting "7537308765" "tencent" "playlist" "autoplay" "mutex:false" "listmaxheight:340px" "preload:auto" "theme:#ad7a86"%}   #这里修改meting 为自己的歌单地址即可
```

## 三、新增电影等

此时我们需要用到一个插件

`hexo-butterfly-douban`

在原倉庫基礎上，修改了一些內容，適配 [Butterfly 主題](https://github.com/jerryc127/hexo-theme-butterfly)。可以配置 `meta`, `top_img`, `comments` 和 `aside`

### 3.1 安裝

```she
$ npm install hexo-butterfly-douban --save
```

### 3.2 配置

```shell
douban:
  user: mythsman
  builtin: false
  book:
    title: 'This is my book title'
    quote: 'This is my book quote'
    meta: true
    comments: true
    top_img: https://cccccc.png
    aside: true
    path: books
    limit:
  movie:
    title: 'This is my movie title'
    quote: 'This is my movie quote'
    meta: true
    comments: true
    top_img: https://cccccc.png
    aside: true
    path: movies
    limit:
  game:
    title: 'This is my game title'
    quote: 'This is my game quote'
    meta: true
    comments: true
    top_img: https://cccccc.png
    aside: true
    path: games
    limit:
  timeout: 10000 
```

| 參數     | 解釋                                                         |
| -------- | ------------------------------------------------------------ |
| user     | 你的豆瓣ID.打開豆瓣，登入賬户，然後在右上角點擊 "個人主頁" ，這時候地址欄的URL大概是這樣："https://www.douban.com/people/xxxxxx/" ，其中的"xxxxxx"就是你的個人ID了 |
| builtin  | 是否將生成頁面的功能嵌入`hexo s`和`hexo g`中，默認是`false`,另一可選項為`true`(1.x.x版本新增配置項) |
| title    | 該頁面的標題                                                 |
| quote    | 寫在頁面開頭的一段話,支持 html 語法.                         |
| timeout  | 【可選】爬取數據的超時時間，默認是 10000ms ,如果在使用時發現報了超時的錯(ETIMEOUT)可以把這個數據設置的大一點 |
| meta     | 【可選】插入 `<meta name="referrer" content="no-referrer">` 到頁面，可解決部分瀏覽器無法顯示豆瓣圖片的問題（會導致一些插件出錯，例如 不蒜子計數器。） |
| comments | 【可選】是否顯示評論                                         |
| top_img  | 【可選】是否顯示頂部圖                                       |
| aside    | 【可選】是否顯示側邊欄                                       |
| path     | 【可選】生成的網址 movie 頁面默認為 `//yourblog/movies` book 頁面默認為 `//yourblog/books` game 頁面默認為 ``//yourblog/games` |
| limit    | 【可選】限制爬取的頁數                                       |

**如果只想顯示某一個頁面(比如movie)，那就把其他的配置項註釋掉即可。**

### 3.3 使用

如果設置中 `builtin` 設為 true 的，直接運行 `hexo g` 就會自動生成。

如果設置中 `builtin` 設為 false 的,需要在 `hexo g` 後再運行 `hexo douban`

### 3.4 注意

1. hexo-butterfly-douban 會主動生成頁面，所以不需要自己創建。

2. 如遇到無法抓取問題，顯示 INFO 0 movies have been loaded in xxx ms, because you are offline or your network is bad

   請過段時間再試試，這我也無能為力。
