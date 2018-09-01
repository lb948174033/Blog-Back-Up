---
title: Hexo博客Yilia主题修改记录
tags:
  - 记录
  - 教程
  - Hexo博客
reward: true
toc: true
abbrlink: 20223
date: 2017-12-05 15:06:52
---
![zhuyetu](https://wx3.sinaimg.cn/mw690/0068Se8Tly1fnt0tk8f7ag30fa03m0sm.gif)
## 说明
* <font size=3>在搭建完自己的博客以后，自然就想着丰富里面的功能，于是这篇文章就记录一下我的博客修改的内容：</font>
> * 文章下面添加livere评论
  * 添加顶部加载条
  * 实现点击出现桃心效果
  * 添加修改相册
  * 在右上角或者左上角实现fork me on github
  * 在每篇文章末尾统一添加“本文结束”标记
  * 在网站底部加上访问量
***
<!-- more --> 

## 一.文章下面添加livere评论

### 1.关于
* <font size=3>因为liyia主题里面只提供的评论有：1、多说；2、网易云跟帖；3、畅言；4、Disqus；5、Gitment；且里面的一些评论已经停止服务，所以我在参考了next主题所使用的评论插件livere以后，插到了liyia主题里面</font>
* <font size=3>效果图：</font>
![liever](https://wx1.sinaimg.cn/mw690/0068Se8Tly1fnt28e9aaqj30yb0dnglt.jpg)

### 2.实现
* <font size=3>首先去[来必力官网](https://livere.com/)注册账号，现在国内很多都要实名制认证了，这个不用，很方便，唯一的遗憾这个是韩网，可能会遇到墙的问题</font>
* <font size=3>打开`yourblog\themes\yilia\layout\_partial`文件夹，并编辑`article.ejs`文件。</font>
* <font size=3>并在这段代码：</font>
``` html
</article>
<% if (!index){ %>
  <%- partial('post/nav') %>
<% } %>
<%- partial('_partial/aside') %>
```
* <font size=3>下面添加：</font>
``` html
<!-- 来必力City版安装代码 -->
<div id="lv-container" data-id="city" data-uid="####################">
<script type="text/javascript">
   (function(d, s) {
       var j, e = d.getElementsByTagName(s)[0];

       if (typeof LivereTower === 'function') { return; }

       j = d.createElement(s);
       j.src = 'https://cdn-city.livere.com/js/embed.dist.js';
       j.async = true;

       e.parentNode.insertBefore(j, e);
   })(document, 'script');
</script>
<noscript>为正常使用来必力评论功能请激活JavaScript</noscript>
</div>
<!-- City版安装代码已完成 -->
```
* <font size=3>其中“##...##”是代码的uid，这段代码可以在来必力官网的控制台直接复制，最后执行`hexo clean` `hexo g` `hexo d`三条命令即可。</font>

## 二.添加顶部加载条

### 1.关于
* <font size=3>参考资料：[hexo的next主题个性化教程:打造炫酷网站](https://www.jianshu.com/p/f054333ac9e6)</font>
* <font size=3>效果图：</font>
![加载条](https://wx1.sinaimg.cn/mw690/0068Se8Tly1fnt1dh1apzj316o049glx.jpg)
=======

### 2.实现
* <font size=3>打开`yourblog\themes\yilia\layout\_partial`文件夹，并编辑`head.ejs`文件。</font>
* <font size=3>并在这段代码：</font>
``` html
  <meta name="renderer" content="webkit">
  <meta http-equiv="X-UA-Compatible" content="IE=edge" >
  <link rel="dns-prefetch" href="<%= config.url %>">
  <title><% if (title){ %><%= title %> | <% } %><%= config.title %></title>
  <meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=1">
```
* <font size=3>下面添加：</font>
``` html
<script src="//cdn.bootcss.com/pace/1.0.2/pace.min.js"></script>
  <link href="//cdn.bootcss.com/pace/1.0.2/themes/pink/pace-theme-flash.css" rel="stylesheet">
    <style>
    .pace .pace-progress {
        background: #6d6d6d; /*进度条颜色*/
        height: 2px;
    }
    .pace .pace-progress-inner {
         box-shadow: 0 0 10px #1E92FB, 0 0 5px     #6d6d6d; /*阴影颜色*/
    }
    .pace .pace-activity {
        border-top-color: #6d6d6d;    /*上边框颜色*/
        border-left-color: #6d6d6d;    /*左边框颜色*/
    }
  </style>
```
* <font size=3>最后执行`hexo clean` `hexo g` `hexo d`三条命令即可。</font>

## 三.实现点击出现桃心效果

### 1.关于
* <font size=3>参考资料：[hexo的next主题个性化教程:打造炫酷网站](https://www.jianshu.com/p/f054333ac9e6)</font>
* <font size=3>效果图：</font>
![桃心](https://wx4.sinaimg.cn/mw690/0068Se8Tly1fnt1fezdnej30lz06jt91.jpg)
=======

### 2.实现
* <font size=3>打开`yourblog\themes\yilia\source\js\src`文件夹，如果找不到，就新建对应的文件夹。在里面新建一个文本文档，并命名为`love.js`文件。打开并编辑，添加以下代码，并保存。</font>
````
!function(e,t,a){function n(){c(".heart{width: 10px;height: 10px;position: fixed;background: #f00;transform: rotate(45deg);-webkit-transform: rotate(45deg);-moz-transform: rotate(45deg);}.heart:after,.heart:before{content: '';width: inherit;height: inherit;background: inherit;border-radius: 50%;-webkit-border-radius: 50%;-moz-border-radius: 50%;position: fixed;}.heart:after{top: -5px;}.heart:before{left: -5px;}"),o(),r()}function r(){for(var e=0;e<d.length;e++)d[e].alpha<=0?(t.body.removeChild(d[e].el),d.splice(e,1)):(d[e].y--,d[e].scale+=.004,d[e].alpha-=.013,d[e].el.style.cssText="left:"+d[e].x+"px;top:"+d[e].y+"px;opacity:"+d[e].alpha+";transform:scale("+d[e].scale+","+d[e].scale+") rotate(45deg);background:"+d[e].color+";z-index:99999");requestAnimationFrame(r)}function o(){var t="function"==typeof e.onclick&&e.onclick;e.onclick=function(e){t&&t(),i(e)}}function i(e){var a=t.createElement("div");a.className="heart",d.push({el:a,x:e.clientX-5,y:e.clientY-5,scale:1,alpha:1,color:s()}),t.body.appendChild(a)}function c(e){var a=t.createElement("style");a.type="text/css";try{a.appendChild(t.createTextNode(e))}catch(t){a.styleSheet.cssText=e}t.getElementsByTagName("head")[0].appendChild(a)}function s(){return"rgb("+~~(255*Math.random())+","+~~(255*Math.random())+","+~~(255*Math.random())+")"}var d=[];e.requestAnimationFrame=function(){return e.requestAnimationFrame||e.webkitRequestAnimationFrame||e.mozRequestAnimationFrame||e.oRequestAnimationFrame||e.msRequestAnimationFrame||function(e){setTimeout(e,1e3/60)}}(),n()}(window,document);
````
* <font size=3>打开`yourblog\themes\yilia\layout`文件夹，并编辑`layout.ejs`文件,最末尾添加：</font>
``` html
<script type="text/javascript" src="/js/src/love.js"></script>
```
* <font size=3>最后执行`hexo clean` `hexo g` `hexo d`三条命令即可。</font>

## 四.添加修改相册

### 1.关于
* <font size=3>参考资料：[hexo Yilia 主题如何添加相册功能](https://maker997.com/2017/07/01/hexo-Yilia-%E4%B8%BB%E9%A2%98%E5%A6%82%E4%BD%95%E6%B7%BB%E5%8A%A0%E7%9B%B8%E5%86%8C%E5%8A%9F%E8%83%BD/#more)、[Hexo+Github实现相册功能](https://lawlite.me/2017/04/13/Hexo-Github%E5%AE%9E%E7%8E%B0%E7%9B%B8%E5%86%8C%E5%8A%9F%E8%83%BD/)</font>
* <font size=3>效果图：</font>
![相册](https://wx3.sinaimg.cn/small/0068Se8Tly1fnt1ip9skaj30wh0idqk0.jpg)
=======

### 2.Github新建相册同步项目
* <font size=3>在Github上面新建一个项目，我这里新建的是一个名为`Blog-Back-Up`的项目</font>
![Blog-Back-Up](https://wx3.sinaimg.cn/mw690/0068Se8Tly1fnt1lga4e5j30mu05874b.jpg)
=======
* <font size=3>然后打开你的blog，你要将你的blog跟新建这个项目git，如果你这里不完成，后面使用脚本操作就会报错或者出现同步不上Github等问题，但是你如果对这些并不是很了解，可以先不git，接着操作`2.博客添加相册布局及样式`，后面脚本出现报错，我会在`5.执行脚本出现的错误`里面细说怎么Git和解决报错问题</font>

### 3.博客添加相册布局及样式
* <font size=3>打开`yourblog\source`文件夹，里面新建一个`photos`文件夹，打开[Blog-Back-Up/source/photos/](https://github.com/lb948174033/Blog-Back-Up/tree/master/source/photos)网站，将里面的五个样式文件下载并复制到你刚刚新建的文件夹内。</font>
* <font size=3>打开并编辑五个样式文件里面的`ins.js`文件，找到`render`函数：</font>
``` js
    var render = function render(res) {
      var ulTmpl = "";
      for (var j = 0, len2 = res.list.length; j < len2; j++) {
        var data = res.list[j].arr;
        var liTmpl = "";
        for (var i = 0, len = data.link.length; i < len; i++) {
          var minSrc = 'https://raw.githubusercontent.com/lb948174033/blog-back-up/master/min_photos/' + data.link[i];
          var src = 'https://raw.githubusercontent.com/lb948174033/blog-back-up/master/photos/' + data.link[i];
          var type = data.type[i];
          var target = src + (type === 'video' ? '.mp4' : '.jpg');
          src += '';

          liTmpl += '<figure class="thumb" itemprop="associatedMedia" itemscope="" itemtype="https://schema.org/ImageObject">\
                <a href="' + src + '" itemprop="contentUrl" data-size="1080x1080" data-type="' + type + '" data-target="' + src + '">\
                  <img class="reward-img" data-type="' + type + '" data-src="' + minSrc + '" src="/assets/img/empty.png" itemprop="thumbnail" onload="lzld(this)">\
                </a>\
                <figcaption style="display:none" itemprop="caption description">' + data.text[i] + '</figcaption>\
            </figure>';
        }
        ulTmpl = ulTmpl + '<section class="archives album"><h1 class="year">' + data.year + '年<em>' + data.month + '月</em></h1>\
        <ul class="img-box-ul">' + liTmpl + '</ul>\
        </section>';
      }
      document.querySelector('.instagram').innerHTML = '<div class="photos" itemscope="" itemtype="https://schema.org/ImageGallery">' + ulTmpl + '</div>';
      createVideoIncon();
      _view2.default.init();
    };
```
* <font size=3>其中`minSrc = `和`src =`后面的url链接就是对应你相册照片地址了，`raw.githubusercontent.com`是个解析网站的意思，其实你就把`/lb948174033/blog-back-up/`给修改一下就行了，`lb948174033`是我的Github用户名，`blog-back-up`是你前面在Github上面创建的项目名称</font>

### 4.脚本对图片进行处理和同步
* <font size=3>打开`yourblog`文件夹，里面再新建一个`photos`文件夹和`min_photos`文件夹，打开[lb948174033/Blog-Back-Up](https://github.com/lb948174033/Blog-Back-Up)网站，将里面的`ImageProcess.py`、`ImageProcess.pyc`、`tool.py`脚本下载并复制到`yourblog`文件夹内，每次要上传博客相册的图片也放在`yourblog\photos`文件夹。</font>
![Blog](https://wx4.sinaimg.cn/mw690/0068Se8Tly1fnt1o5468yj30xv0aemyk.jpg)
=======
* <font size=3>在`yourblog`文件夹内执行`python tool.py`命令就会执行脚本，最后再执行`hexo clean` `hexo g` `hexo d`三条命令即可。</font>

### 5.执行脚本可能会出现的错误
* <font size=3>如果出现`no module named PIL`报错，出现这错误的原因是: PIL 模块找不到,PIL 模块已经过时了，解决方案: 输入`pip install pillow`即可</font>
* <font size=3>如果出现执行完脚本，你的Github上面并没有同步项目，那就是说明你的blog文件夹并没有push到github上面，这个时候你可以输入这些指令：`git int`、`git add --all`、`git commit -m "add photos"`、`git push origin master`，详细可以百度查git资料</font>

## 五.博客边角实现fork me on github

### 1.关于
* <font size=3>参考资料：[hexo的next主题个性化教程:打造炫酷网站](https://www.jianshu.com/p/f054333ac9e6)</font>
* <font size=3>效果图：</font>
![fork me on github](https://wx2.sinaimg.cn/small/0068Se8Tly1fnt1aqv7jvj30aq0aiwet.jpg)

### 2.实现
* <font size=3>打开[GitHub Corners](https://tholman.com/github-corners/)或[GitHub Ribbons](https://github.com/blog/273-github-ribbons)网站，从里面选择一个你喜欢的样式，并复制其代码</font>
![1](https://wx3.sinaimg.cn/mw690/0068Se8Tly1fnt1hf4bqdj30gq05f3z3.jpg)
* <font size=3>打开`yourblog\themes\yilia\layout`文件夹，并编辑`layout.ejs`文件。</font>
* <font size=3>并在这段代码：</font>
``` html
<%- partial('_partial/head') %>
<body>
  <div id="container" q-class="show:isCtnShow">
    <canvas id="anm-canvas" class="anm-canvas"></canvas>
    <div class="left-col" q-class="show:isShow">
      <%- partial('_partial/left-col', null, {cache: !config.relative_link}) %>
```
* <font size=3>下面添加：</font>
``` html
<a href="https://github.com/lb948174033"><img style="position: absolute; top: 0; left: 0; border: 0;" src="https://camo.githubusercontent.com/c6625ac1f3ee0a12250227cf83ce904423abf351/68747470733a2f2f73332e616d617a6f6e6177732e636f6d2f6769746875622f726962626f6e732f666f726b6d655f6c6566745f677261795f3664366436642e706e67" alt="Fork me on GitHub" data-canonical-src="https://s3.amazonaws.com/github/ribbons/forkme_left_gray_6d6d6d.png"></a>
```
* <font size=3>其中`href=`后面的链接是你Github主页对应的链接，`style`是风格，也就是位置和颜色这些款式，alt是显示的文字.最后执行`hexo clean` `hexo g` `hexo d`三条命令即可。</font>

## 六.在每篇文章末尾统一添加“本文结束”标记

### 1.关于
* <font size=3>效果图：</font>
![文本结束](https://wx1.sinaimg.cn/mw690/0068Se8Tly1fnt19h99c7j30gq01ka9v.jpg)
=======

### 2.实现
* <font size=3>打开`yourblog\themes\yilia\layout\_partial`文件夹，并编辑`article.ejs`文件。</font>
* <font size=3>并在这段代码：</font>
``` html
      <% if (!index && theme.share_jia){ %>
        <%- partial('post/share') %>
      <% } %>
      <div class="clearfix"></div>
    </div>
```
* <font size=3>下面添加：</font>
``` html
  </div>
  	<div>
      <div style="text-align:center;color: #ccc;font-size:14px;">-------------本文结束<i class="fa fa-paw"></i>感谢您的阅读-------------</div>
	</div>
```
* <font size=3>最后执行`hexo clean` `hexo g` `hexo d`三条命令即可。</font>

## 七.在网站底部加上访问量

### 1.关于
* <font size=3>参考资料：[hexo的next主题个性化教程:打造炫酷网站](https://www.jianshu.com/p/f054333ac9e6)</font>
* <font size=3>效果图：</font>
![访问量](https://wx2.sinaimg.cn/mw690/0068Se8Tly1fnt1qb7rh9j307602jwe9.jpg)
=======

### 2.实现
* <font size=3>打开`yourblog\themes\yilia\layout\_partial`文件夹，并编辑`footer.ejs`文件。</font>
* <font size=3>并在这段代码：</font>
``` html
    	<div class="footer-left">
    		&copy; <%= date(new Date(), 'YYYY') %> <%= config.author || config.title %>
        <script async src="https://dn-lbstatics.qbox.me/busuanzi/2.3/busuanzi.pure.mini.js"></script>
```
* <font size=3>下面添加：</font>
``` html
<div class="powered-by">
<i class="fa fa-user-md"></i><span id="busuanzi_container_site_uv">
  本站访客数:<span id="busuanzi_value_site_uv"></span>
</span>
</div>
```
* <font size=3>其实具体在页脚哪里添加，哪怕不添加在页脚也行，看个人喜好了。最后执行`hexo clean` `hexo g` `hexo d`三条命令即可。</font>