---
title: 用亚马逊服务器免费搭建SS
tags:
  - 记录
  - 教程
  - 科学上网
reward: true
toc: true
abbrlink: 28110
date: 2018-03-12 18:11:46
---
![zhuyetu](https://wx3.sinaimg.cn/mw690/0068Se8Tgy1fpa7gerzu8j30jw08974n.jpg)

## 一.前言
> 因为大天朝的一些限制，所以科学上网是很多人都需要的，像我之前在Android平台时可以用许多科学上网的软件（网速是硬伤），但是换到了IOS平台显然这些开源化的福利就享受不到了（越狱不说），这时购买VPS搭建自己的海外服务器就比较靠谱，从经济的角度考虑，购买VPS尽量从免费的入手，首推AWS（Amazon Web Services），只要注册成功会送12个月的免费服务器。

<!-- more --> 

## 二.注册AWS
* <font size=3>打开[亚马逊服务器](https://amazonaws-china.com/cn/)的官方网站，点击创建免费账户，这些注册过程倒也没什么好说的，其中注册的时候要用到信用卡，直接到淘宝买一张信用卡账号就行（卡号16位，价格大概8.8元左右吧），持卡人姓名是可以匿名的，也就是随便填姓名。</font>

* <font size=3>这个信用卡验证是有几率失败的，我在淘宝上分别买了两张信用卡，第一张失败了，左改信息右改信息都没用，然后重新购买第二张信用卡就通过审核了。如果审核失败，重新购买信用卡，建议账号也重新注册一下，这样过审成功率高一些。出现下面这个图或者注册的时候提示支付信息错误，基本上等于失败了，他给你发邮件要你提供什么单子，这些信息淘宝买的虚拟信用卡都是没有提供的。</font>

![yanzheng](https://wx2.sinaimg.cn/mw690/0068Se8Tgy1fpa9n3zu1gj30pf0aqq2y.jpg)

## 三.创建亚马逊服务器
* <font size=3>创建好后账号后，打开AWS管理控制台，点击EC2，并创建启动实例，如图</font>

![EC2](https://wx2.sinaimg.cn/mw690/0068Se8Tgy1fpa9vts2eij316y0m7q5q.jpg)

![实例](https://wx1.sinaimg.cn/mw690/0068Se8Tgy1fpa9yqqi9fj30l904dweh.jpg)

* <font size=3>接着选择Ubuntu系统映像，如图</font>

![ubuntu](https://wx3.sinaimg.cn/mw690/0068Se8Tgy1fpaa0nov52j31a70k5gom.jpg)

* <font size=3>然后一直下一步，一直到第五步的`添加标签`</font>

![ami](https://wx3.sinaimg.cn/mw690/0068Se8Tgy1fpaa3sr2sjj31700kpgnj.jpg)

![biaoqian](https://wx1.sinaimg.cn/mw690/0068Se8Tgy1fpaa5np8nnj316t0kfmxy.jpg)

* <font size=3>密钥填你的Name随便你改不改，后面的值填一下你的密码，然后继续下一步，到`配置安全组`，点击添加规则，配置所有流量和端口开放，然后下一步，启动</font>

![anquanzu](https://wx3.sinaimg.cn/mw690/0068Se8Tgy1fpaa9t6ppkj316q0f475c.jpg)

* <font size=3>创建新的密钥，下载下来，然后设置，并连接实例</font>

![miyao](https://wx2.sinaimg.cn/mw690/0068Se8Tgy1fpaafnhym7j30zt0icwg5.jpg)

![tongzhi](https://wx3.sinaimg.cn/mw690/0068Se8Tgy1fpaahwwmc3j30xw07q3z3.jpg)

![tongzhi2](https://wx2.sinaimg.cn/mw690/0068Se8Tgy1fpaahwfzbzj30xs0c3tae.jpg)

![lianjie](https://wx1.sinaimg.cn/mw690/0068Se8Tgy1fpaal348c4j311q0bp3z0.jpg)

## 四.XShell登录亚马逊EC2云服务器
* <font size=3>百度下载一个Xshell工具，随便安到哪里，路径不一定c盘</font>
* <font size=3>打开XShell，选择`工具`菜单项，选择`用户密码管理者`，打开`用户密钥`界面，选择`导入`，导入之前下载好的PEM密钥文件</font>

![XShell](https://wx3.sinaimg.cn/mw690/0068Se8Tgy1fpaasal1bdj30hz0hadgg.jpg)

* <font size=3>选择`文件`菜单下的`新建`项，我们开始新建一个到云服务器的会话连接，在左侧列表框中选择`连接`，在右侧界面中输入会话名称和主机IP，端口可以不用改，名称随意</font>

![XShell2](https://wx2.sinaimg.cn/mw690/0068Se8Tgy1fpaaw1w7rsj30hp0hcjs7.jpg)

* <font size=3>在左侧列表框中选择`用户身份验证`，修改右侧界面：`方法`项的值改成`Public Key`，`用户名`那里填写ubuntu，否则会出现 所选的用户密钥未在远程主机上注册 请再试一次，`用户密钥`项的值是下拉框中选择前面说的导入的PEM文件，点击`确定`按钮，完成设置。</font>

![XShell3](https://wx4.sinaimg.cn/mw690/0068Se8Tgy1fpab06cakij30h50h60tj.jpg)

* <font size=3>最后打开并连接就可以了</font>

![XShell4](https://wx3.sinaimg.cn/mw690/0068Se8Tgy1fpab1vqkojj30gp0aomxd.jpg)

## 五.安装并配置Shadowsocks
* <font size=3>安装Shadowsocks</font>
``` html
// 获取root权限
sudo -s

// 更新apt-get
apt-get update

// 安装python包管理工具
apt-get install python-setuptools
apt-get install python-pip

// 安装shadowsocks
pip install shadowsocks
```
* <font size=3>配置Shadowsocks</font>
```
mkdir /etc/shadowsocks
vim /etc/shadowsocks/ss.json
```
* <font size=3>配置文件内容，退出按键盘的`esc`键退出，`shift`键，然后再输入wq，保存并退出</font>
```
{
    "server":"0.0.0.0",
    "server_port":443,
    "local_address":"127.0.0.1",
    "local_port":1080,
    "password":"密码",
    "timeout":300,
    "method":"aes-256-cfb",
    "fast_open":false,
    "workers": 1
}
```

| 配置字段        | 说明           |
| ------------- |:-------------:|
| server      | 服务端监听地址(IPv4或IPv6) |
| server_port      | 服务端端口，一般为443      |
| local_address | 本地监听地址，缺省为127.0.0.1      |
| local_port      | 本地监听端口，一般为1080 |
| password      | 用以加密的密匙      |
| timeout | 超时时间（秒）      |
| method      | 加密方法，默认为aes-256-cfb，更多请查阅[Encryption](https://github.com/shadowsocks/shadowsocks/wiki/Encryption) |
| fast_open      | 是否启用[TCP-Fast-Open](https://github.com/shadowsocks/shadowsocks/wiki/TCP-Fast-Open)，true或者false      |
| workers | [worker数量](https://github.com/shadowsocks/shadowsocks/wiki/Workers)      |

* <font size=3>启动Shadowsocks</font>
```
// 启动
ssserver -c /etc/shadowsocks/ss.json -d start 
// 停止
ssserver -c /etc/shadowsocks/ss.json -d stop 
// 重启
ssserver -c /etc/shadowsocks/ss.json -d restart
```
* <font size=3>设置SS为开机自启动</font>
```
// 编辑rc.local
vi /etc/rc.local
// 加入
sudo ssserver -c /etc/shadowsocks/ss.json -d start
```
* <font size=3>到这里就结束了，最后只要你用手机或者电脑连接SS就可以啦，</font>