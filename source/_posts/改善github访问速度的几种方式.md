---
title: 改善github访问速度的几种方式
tags:
  - GitHub
categories:
  - GitHub
toc: true
abbrlink: 38968
date: 2021-07-25 13:11:18
---



改善github访问速度的几种方式：

<!--more-->

## **1. GitHub 镜像访问**

这里提供两个最常用的镜像地址：

* [https://github.com.cnpmjs.org](https://link.zhihu.com/?target=https%3A//github.com.cnpmjs.org)
* [https://hub.fastgit.org](https://link.zhihu.com/?target=https%3A//hub.fastgit.org)

也就是说上面的镜像就是一个克隆版的 GitHub，你可以访问上面的镜像网站，网站的内容跟 GitHub 是完整同步的镜像，然后在这个网站里面进行下载克隆等操作。



## **2. GitHub 文件加速**

利用 Cloudflare Workers 对 github release 、archive 以及项目文件进行加速，部署无需服务器且自带CDN.

* [https://gh.api.99988866.xyz](https://link.zhihu.com/?target=https%3A//gh.api.99988866.xyz)
* [https://g.ioiox.com](https://link.zhihu.com/?target=https%3A//g.ioiox.com)

以上网站为演示站点，如无法打开可以查看开源项目：gh-proxy-GitHub([https://hunsh.net/archives/23/](https://link.zhihu.com/?target=https%3A//hunsh.net/archives/23/)) 文件加速自行部署。

## **3. Github 加速下载**

只需要复制当前 GitHub 地址粘贴到输入框中就可以代理加速下载！

地址：[http://toolwa.com/github/](https://link.zhihu.com/?target=http%3A//toolwa.com/github/)

![image-20210427044306625](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/github%E5%8A%A0%E9%80%9F%E8%AE%BF%E9%97%AE%E7%9A%84%E5%87%A0%E7%A7%8D%E6%96%B9%E5%BC%8F01.png)

## **4. 加速你的 Github**

[https://github.zhlh6.cn](https://link.zhihu.com/?target=https%3A//github.zhlh6.cn)

输入 Github 仓库地址，使用生成的地址进行 git ssh 等操作

## **5. 谷歌浏览器 GitHub 加速插件(推荐)**

![image-20210427044539819](https://cdn.jsdelivr.net/gh/liuhuanhuan963019/blogPicture/md_photos/github%E8%AE%BF%E9%97%AE%E5%8A%A0%E9%80%9F%E7%9A%84%E5%87%A0%E7%A7%8D%E6%96%B9%E5%BC%8F02.png)

## **6. GitHub raw 加速**

GitHub raw 域名并非 [http://github.com](https://link.zhihu.com/?target=http%3A//github.com) 而是 [http://raw.githubusercontent.com](https://link.zhihu.com/?target=http%3A//raw.githubusercontent.com)，上方的 GitHub 加速如果不能加速这个域名，那么可以使用 Static CDN 提供的反代服务。

将 [http://raw.githubusercontent.com](https://link.zhihu.com/?target=http%3A//raw.githubusercontent.com) 替换为 [http://raw.staticdn.net](https://link.zhihu.com/?target=http%3A//raw.staticdn.net) 即可加速。

## **7. GitHub + Jsdelivr**

jsdelivr 唯一美中不足的就是它不能获取 exe 文件以及 Release 处附加的 exe 和 dmg 文件。

也就是说如果 exe 文件是附加在 Release 处但是没有在 code 里面的话是无法获取的。所以只能当作静态文件 cdn 用途，而不能作为 Release 加速下载的用途。

## **8. 通过 Gitee 中转 fork 仓库下载**

网上有很多相关的教程，这里简要的说明下操作。

访问 gitee 网站：[https://gitee.com/](https://link.zhihu.com/?target=https%3A//gitee.com/) 并登录，在顶部选择“从 GitHub/GitLab 导入仓库” 如下：

等待导入操作完成，然后在导入的仓库中下载浏览对应的该 GitHub 仓库代码，你也可以点击仓库顶部的“刷新”按钮进行 Github 代码仓库的同步。

## **9. 通过修改 HOSTS 文件进行加速**

手动把cdn和ip地址绑定。

[【github】提升github访问速度_最爱吃大米的博客-CSDN博客_github hosts加速](https://blog.csdn.net/qq_38140292/article/details/114104854)
