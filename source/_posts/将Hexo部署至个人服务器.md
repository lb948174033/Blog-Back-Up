---
title: 将Hexo部署至个人服务器
tags:
  - 记录
  - 教程
  - Hexo博客
reward: true
toc: true
abbrlink: 51893
date: 2018-09-02 21:21:29
---
![zhuyetu](http://wx4.sinaimg.cn/mw690/0068Se8Tgy1furl0jdw8hj31hc0u0tcy.jpg)
## 前言
* <font size=3>在开始文章之前，我先感慨一句：“一入前端深似海,从此再无安宁日。”，好像总是有填不完的坑和看了总想改的界面...</font>

<!-- more --> 
* <font size=3>在有了自己的站点以后，虽然互联网给我们提供了许多托管代码的地方，但是这种“人在屋檐下”的feel，我相信是每一个小强迫症所不能容忍的，嘻嘻。其实有个自己的服务器部署站点，还有着:1.访问加载网页速度更快，不用通过第三方平台再转一下，你可以选择高性能服务器。2.利于备案等操作，使站点更具有可信度。3.有着自己独立的隐私空间，存储数据等这些优点</font>

## 一.选择服务器及安装Hexo

### 1.选择服务器
* <font size=3>服务器的选择总结起来一句话：因需而选。像部署hexo这种个人博客站，就尽量选择性能最小的，这样也最便宜，像我目前使用的就是腾讯云学生机，相当于阿里的服务器来说，老马在价格方面还是良心一些呀。</font>

### 2.安装Hexo
* <font size=3>Hexo的安装及部署，我觉得没必要再重复多叙述了，详情可以参考这篇文章：[GitHub+Hexo 搭建个人网站详细教程](https://zhuanlan.zhihu.com/p/26625249)，这是我目前看过最详细的一篇文了。</font>

## 二.配置服务器远程 Git

### 1.git环境搭建
* <font size=3>首先下好并安装好Git，这个直接百度就有资源下载了，可以参考这个Git资料：[Git教程](https://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000)</font>

### 2.生成ssh认证
* <font size=3>在你的Hexo博客根目录下执行如下命令：</font>
``` Bash
git config --global user.name "yourname"
git config --global user.email youremail@example.com
ssh-keygen -t rsa -C "youremail@example.com"
git config --global core.autocrlf false  // 禁用自动转换
```
* <font size=3>最后获取到的ssh认证在`C:\Users\yourname\.ssh`中，名字叫`id_rsa.pub`</font>

### 3.搭建远程Git私库
* <font size=3>登录到远程服务器，可以使用`Xshell 6`或者`Xftp 6`，我这里使用的是`Xshell 6`</font>
* <font size=3>安装 git，执行如下命令：</font>
``` Bash
yum install curl-devel expat-devel gettext-devel openssl-devel zlib-devel perl-devel
yum install -y git
```
* <font size=3>给服务器安装Centeros，以上和以下命令是针对Centos</font>
* <font size=3>创建用户并配置其仓库，执行如下命令：</font>
``` Bash
useradd git
passwd git // 设置密码
su git // 这步很重要，不切换用户后面会很麻烦
cd /home/git/
mkdir -p projects/blog // 项目存在的真实目录
mkdir repos && cd repos
git init --bare blog.git // 创建一个裸露的仓库
cd blog.git/hooks
vi post-receive // 创建hook钩子函数

然后输入内容如下：
#!/bin/sh
git --work-tree=/home/git/projects/blog --git-dir=/home/git/repos/blog.git checkout -f

编辑命令：
键盘上ins键  //进行编辑
退出保存 先键盘上Esc键 然后：键（冒号键} 最后输入wq 保存并退出
```
* <font size=3>添加完毕后修改权限，执行如下命令</font>
``` Bash
chmod +x post-receive
exit // 退出到 root 登录
chown -R git:git /home/git/repos/blog.git // 添加权限
```
* <font size=3>测试git仓库是否可用，电脑上另找空白文件夹，如果能将空文件夹拉下来，则成功，执行如下命令：</font>
``` Bash
git clone git@server_ip:/home/git/repos/blog.git
```
* <font size=3>建立ssh信任关系，在本地电脑，执行如下命令：</font>
``` Bash
ssh-copy-id -i C:/Users/yourname/.ssh/id_rsa.pub git@server_ip
ssh git@server_ip // 测试能否登录
此时的ssh登录git用户不需要密码，则建立成功
```
* <font size=3>打开`Xshell 6`并连接到服务器，为了安全起见禁用git用户的shell登录权限，从而只能用`git clone`,`git push`等登录，执行如下命令：</font>
``` Bash
cat /etc/shells // 查看`git-shell`是否在登录方式里面，有则跳过
which git-shell // 查看是否安装
vi /etc/shells
添加上2步显示出来的路劲，通常在 /usr/bin/git-shell

vi /etc/passwd
将：
git:x:1000:1000::/home/git:/bin/bash
改为：
git:x:1000:1000:,,,:/home/git:/usr/bin/git-shell
```

### 3.搭建nginx服务器
* <font size=3>下载并安装nginx，执行如下命令：</font>
``` Bash
cd /usr/local/src
wget http://nginx.org/download/nginx-1.15.2.tar.gz
tar xzvf nginx-1.15.2.tar.gz
cd nginx-1.15.2
./configure // 如果后面还想要配置 SSL 协议，就执行后面一句！
./configure --prefix=/usr/local/nginx --with-http_stub_status_module --with-http_ssl_module --with-file-aio --with-http_realip_module
make && make install
alias nginx='/usr/local/nginx/sbin/nginx' // 为nginx取别名，后面可直接用

nginx // 输入完这句后，浏览器输入服务器ip，查看是否有nginx页面，有则成功安装

继续执行：
nginx -s stop // 先停止nginx
cd /usr/local/nginx/conf
vi nginx.conf
修改 root 解析路径，如下图
同时将 user 改为 root 如下图，不然nginx无法访问 /home/git/project/blog
nginx -s reload
```
![root](http://wx3.sinaimg.cn/mw690/0068Se8Tgy1fuvl04kz8oj30l30eq75s.jpg)

![user](http://wx2.sinaimg.cn/mw690/0068Se8Tgy1fuvl00yxuqj30qx0gtac6.jpg)

## 三.本地配置
* <font size=3>配置Hexo根目录的`_config.yml`文件，搜索`deploy`，将其并修改为：</font>
``` code
deploy:
  type: git
  repo: git@yourip:/home/git/repos/blog.git
  branch: master
```
![deploy](http://wx1.sinaimg.cn/mw690/0068Se8Tgy1fuvjzn0cprj30ip04qmxm.jpg)

* <font size=3>`yourip`为你的服务器ip或者是你的域名，然后执行`hexo clean`、`hexo g`和`hexo d`查看效果。发布完成以后，也可以下一个`Xftp 6`软件，连接到你的服务器，到`/home/git/projects/blog`目录下查看你的hexo站点文件，`Xftp 6`是Gui图形画界面</font>
![Xftp](http://wx4.sinaimg.cn/mw690/0068Se8Tgy1fuvjxtm0ldj30id0cl3zh.jpg)

## 参考
* <font size=3>下面这第一篇文章写的真的很详细，只是有点杂乱，本文大部分代码均复制于第一篇</font>

[带你跳过各种坑，一次性把 Hexo 博客部署到自己的服务器](https://blog.csdn.net/qq_35561857/article/details/81590953?tdsourcetag=s_pctim_aiomsg)
[使用 Git Hook 自动部署 Hexo 到个人 VPS](http://www.swiftyper.com/2016/04/17/deploy-hexo-with-git-hook/)