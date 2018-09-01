---
title: 将Hexo博客部署至Coding
tags:
  - 记录
  - 教程
  - Hexo博客
reward: true
toc: true
abbrlink: 5827
date: 2018-03-15 13:08:39
---
![zhuyetu](https://wx2.sinaimg.cn/mw690/0068Se8Tgy1fpdg32lfd4j30p70ciq6z.jpg)
## 前言
* <font size=3>之前的Hexo博客部署在Github，但是因为一些墙和政策方面的问题，百度没办法去收录个人网站，所以部署到了Coding平台，并不是说部署到Coding平台，Github平台就不能用了，你可以设置个性化域名，国内网访问Coding平台的页面，外网访问Github平台的页面，可以同时部署，然后说一下Coidng的优点吧：</font>
> * 访问加载网页速度更快
  * 利于爬虫爬取数据，搜索引擎收录
  * 操作及设置更加贴合国内环境

<!-- more --> 

## 一.Coding上创建项目

### 1.注册Coding账号
* <font size=3>[Coding账号注册](https://coding.net/)实在是没有什么难度，都是国内平台，邮箱手机号码填一下就可以了，Coding在Ios Android平台都是有客户端的，每次Push代码也会送平台的代码币可以用来换置礼物。</font>

### 2.项目注册
* <font size=3>打开Coding平台，新建一个项目，名字我建议和你Coding的用户名保持一致，因为如果你的项目名称跟你Coding的用户名一样，比如我的用户是叫`lb948174033`,博客项目名也叫`lb948174033`，那直接访问`lb948174033.coding.me`就能访问博客，否则就要带上项目名：`lb948174033.coding.me/项目名` 才能访问，推荐项目名跟用户名一样，这样就可以省略项目名，并且设置CNAME解析的时候，`lb948174033.coding.me/项目名`这个是没办法解析的，反正我自己是解析失败。</font>
![Coding](https://wx4.sinaimg.cn/mw690/0068Se8Tgy1fpdx4zb69qj30oa09bq34.jpg)

### 3.设置公钥
* <font size=3>之前搭建Hexo博客的时候，我们生成了一个SSH公钥，我们将其复制一下。本地打开`id_rsa.pub`密钥文件，复制其中全部内容。</font>
* <font size=3>进入Coding页面，点击`账户`，打开`SSH公钥`后，点击`新增公钥`，将`id_rsa.pub`密钥文件里面的内容复制进去，`公钥名称`随便。</font>
![SSH](https://wx1.sinaimg.cn/mw690/0068Se8Tgy1fpdxmaeprfj30yf0gsmxw.jpg)

* <font size=3>添加后，在`git bash`命令输入：</font>
``` git
ssh -T git@git.coding.net
```
* <font size=3>如果得到下面提示就表示公钥添加成功了：</font>
``` git
Coding.net Tips : [Hello ! You've conected to Coding.net by SSH successfully! ]
```

### 4.Pages服务方式部署
* <font size=3>Pages服务方式部署有两种，一种是`静态Pages`，我用的就是这种方式，一种是`动态Pages`</font>
* <font size=3>`静态Pages`很简单，先在source/需要创建一个空白文件，至于原因，是因为coding.net需要这个文件来作为以静态文件部署的标志。就是说看到这个`Staticfile`就知道按照静态文件来发布。</font>
![Staticfile](https://wx3.sinaimg.cn/mw690/0068Se8Tgy1fpdy7eqf1nj30ts071jrp.jpg)

* <font size=3>然后Coding里面打开自己的项目，点击`代码`，再点击`Pages服务`，启动`静态Pages`服务，有个性化域名的就设置一下域名，没有的就算了。</font>
![Staticfile2](https://wx1.sinaimg.cn/mw690/0068Se8Tgy1fpdybwfzsfj314n0lpdis.jpg)

## 二.配置_config.yml
* <font size=3>想要同时部署到2个平台，就要修改博客根目录下面的_config.yml文件中的deploy，加一条repo：</font>
``` git
git@git.coding.net:lb948174033/lb948174033.git,master
```
* <font size=3>这样使用部署命令：`hexo d`，就可以同时部署到两个平台了</font>
![git](https://wx1.sinaimg.cn/mw690/0068Se8Tgy1fpdxunx0gpj30tp0cnt9v.jpg)

## 三.个人域名绑定
* <font size=3>要实现国内的走Coding，海外的走Github，只要配置2个CNAME就行</font>
![yuming](https://wx3.sinaimg.cn/mw690/0068Se8Tgy1fpdyftgsewj30w505y0t4.jpg)

* <font size=3>到此，教程就结束了，只要部署一次，Github和Coding两个都会同步。</font>

## 参考
[hexo干货系列：（四）将hexo博客同时托管到github和coding](https://www.cnblogs.com/tengj/p/5352572.html)