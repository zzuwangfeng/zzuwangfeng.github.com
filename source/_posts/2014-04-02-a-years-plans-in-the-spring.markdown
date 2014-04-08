---
layout: post
title: "A year's plans in the spring"
date: 2014-04-02 16:52:54 +0800
comments: true
categories: Octopress
---
### 大家好，我是JackWong！欢迎大家来到我的小站！

一直想弄个bolg,由于时间问题,今天终于弄成了.由于git和[markdown](http://en.wikipedia.org/wiki/Markdown)对我来说就是小白，所以搭建的时间断断续续持续了约一周。其实网上已经有很好的参考资料了，只要照着弄，很容易就能搭建好的。

这篇文章是第一篇，我用的[markdown](http://en.wikipedia.org/wiki/Markdown)编辑器是[mou](http://www.mouapp.com)，感觉不错。
下面是一些在mac机器上用octopress写博文需要用到的操作(持续更新)

**目录**

* 发表并部署博文

* 添加多说评论功能

* 起草文章 暂不公开

* 域名解析

* 添加百度统计和google analytics

###发表并部署博文###
```
$ rake new_post["New Post"]
$ rake generate
$ git add .
$ git commit -am "Some comment here." 
$ git push origin source
$ rake deploy
```
###添加多说评论功能###

**A 获取** ``short_name``

去多说网注册账号，获取站点的short_name

**B 在** ``_config.yml`` **文件中添加如下内容**

```
#duoshuo comments
duoshuo_comments: true
duoshuo_short_name: yourname
```
**C 在** ``source/_layouts/post.html`` **中添加多说评论模块**

```
｛% if site.duoshuo_short_name and site.duoshuo_comments == true and page.comments == true %｝
  <section>
    <h1>Comments</h1>
    <div id="comments" aria-live="polite">｛% include post/duoshuo1.html %｝</div>
  </section>
｛% endif %｝
```
**D 发布到站点**

```
$ rake generate
$ git add .
$ git commit -am "添加多说评论" 
$ git push origin source
$ rake deploy
```

###起草文章暂不公开###

在文章头部添加 ``published: false`` ，就能起到暂时不公开文章了(即使已经部署到了github中)，要公开文章只需要将false修改true即可。

###域名解析###

我们可以给GitHub上的page指定一个域名，具体做法如下2个步骤

**1、给repo配置域名**

在 ``source`` 根目录下新建一个名为``CNAME``的文件，并把你的域名填写进去，例如``iluckly.com``。这样做的目的是告诉GitHub服务器开始将repo中的page(例如``zzuwangfeng.github.io``)指向到某个域名中。

**2、配置DNS(我的域名是在godaddy上购买的)**
添加一条A记录： ``@ 204.232.175.78`` 在CNAME中添加一条记录:``zzuwangfeng.github.com``

###添加百度统计和google analytics###
从百度统计获取脚本，然后添加到文件s``ource/_includes/after_footer.html``文件中 从google analytics获取跟踪ID，然后将这个ID添加到``_config.yml``文件的``google_analytics_tracking_id``后面即可。





