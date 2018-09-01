---
title: Windows系统的优化
tags:
  - 记录
  - 教程
  - Windows
reward: true
toc: true
abbrlink: 23934
date: 2018-01-28 16:37:35
---
![zhuyetu](https://wx1.sinaimg.cn/mw690/0068Se8Tly1fnweucfauaj31hc0u0465.jpg)
## 前言
> 本篇文章记录一下Windows系统的优化，其中很多都是在各个论坛的技术贴上所Get到的，这些对电脑优化的技术教程都是我自己亲自实践有用所收藏的精华，点滴记录汇成此博。至今也不记得这些优化教程的具体出处了，所以也就不列举了，只能说前人栽树后人乘凉吧...

* <font size=3>整理如下：</font>

<!-- more --> 

> * Windows系统的精简
  * 禁用多余服务及关闭磁盘碎片整理计划
  * 设置windows启动参数软件自启动
  * 取消不必要的计划任务及磁盘清理
  * 显卡优化windows设置
  * CPU优化winodws设置
  * 网速优化windows设置
  * 其他设置

***
## 一.Windows系统的精简
* <font size=3>Windows的精简很重要，当一台计算机没有那些冗余的软件跟插件的时候，自然也就能最大程度发挥它的实力。</font>
* <font size=3>如果当你还没有装好系统的时候，这个时候你可以不用考虑那些msdn或者微软的官网的镜像去装系统，你可以到网上找一个精简好的Windows镜像文件去安装就可以了，这里有整理好的几套镜像，大部分都是在吾爱论坛淘到的，具体作者是谁也不记得了</font>
> * [Windows10（1703）精简版：](https://pan.baidu.com/s/1bq5TQUV) 密码: t2ku
  * [俄罗斯大神精简的Windows7版：](https://pan.baidu.com/s/1dHdFJ8H) 密码: n82r
  * [Windows7 SP1旗舰精简版：](https://pan.baidu.com/s/1kW8vyuj) 密码: h9hy
  * [Windows7（64位）其他精简版：](https://pan.baidu.com/s/1jJRur8i) 密码: n7sa

* <font size=3>如果你已经装好系统，那么你所需要的肯定已经不再是精简镜像了，而是需要精简掉那些你不需要的软件的方法，我这里不会去具体强调哪些Windows软件卸载，对于强迫症来说无疑全部卸载才是王道，因为这始终是一个使用习惯问题，所以授之于鱼不如授之于渔，精简哪些还是让大家自己决定吧。
管理员权限打开`windows powershell`</font>
``` html
//卸载命令
Get-AppxPackage *ZuneMusic* | Remove-AppxPackage

//加载所有app
Get-AppxPackage -AllUsers

//得到所有的PackageFullName，可卸载PackageFullName
get-appxpackage -alluser | findstr "PackageFullName"
```
![windows powershell](https://wx3.sinaimg.cn/mw690/0068Se8Tly1fnxbab3idnj30kp0hjgm4.jpg)

## 二.禁用多余服务及关闭磁盘碎片整理计划

### 1.禁用多余服务
* <font size=3>电脑计算机之所以有的时候越用越卡就是因为那些多余服务占用了你电脑的使用，这些服务有些是微软自带的，有些是安装第三方软件产生的，软件千千万，是不可能讲的完的，所以这里就以微软自带的服务举例子。</font>
* <font size=3>打开`控制面板–管理工具–服务`</font>
``` html
//微软搜索
Windows Search 禁用

//微软家庭组
HomeGroup Listener和HomeGroup Provider 设置禁用

//安全中心
SecurityCenter 设置禁用

//微软升级
Windows Update 设置禁用

//内存管理机制
Superfetch -启动类型–自动（延迟启动）
```
![Superfetch](https://wx4.sinaimg.cn/mw690/0068Se8Tly1fnxbn2q3dzj30d30gmgm2.jpg)

### 2.关闭磁盘碎片整理计划
* <font size=3>如果不是固态硬盘，那么是没必要关闭磁盘碎片整理计划的，因为磁盘碎片整理，就是通过系统软件或者专业的磁盘碎片整理软件对电脑磁盘在长期使用过程中产生的碎片和凌乱文件重新整理，可提高电脑的整体性能和运行速度。但是如果是固态硬盘，固态硬盘的闪存存储特性决定了其擦写次数是有限的，一旦超过擦写限额，磁盘将无法写入成为废盘。固态硬盘进行磁盘碎片整理是加速硬盘报废。</font>
* <font size=3>打开`我的电脑`，右键`磁盘C`-`属性`–`工具`–`对驱动器进行优化和碎片整理`–`优化`–`更改设置`–`取消选择按计划`运行</font>
![磁盘碎片整理计划](https://wx3.sinaimg.cn/mw690/0068Se8Tly1fnxbwqjudlj30ji0fpgma.jpg)

## 三.设置windows启动参数软件自启动
* <font size=3>如果不是uefi启动引导，那就没必要修改“引导”了，修改一下“启动”就行</font>
* <font size=3>`Win+R`打开`运行`，或者右键左下角开始键，再点`运行`，输入`MSCONFIG`，如图：</font>
![MSCONFIG](https://wx1.sinaimg.cn/mw690/0068Se8Tly1fnxc1pk9efj30b406nglp.jpg)

* <font size=3>打开第一个选项卡“常规”，勾选有选择的启动，去掉使用原有引导配置，如图：</font>
![常规](https://wx3.sinaimg.cn/mw690/0068Se8Tly1fnxc6gu2w3j30ih0dpaaf.jpg)

* <font size=3>打开第二个选项卡“引导”，勾选无GUI引导，超时改为3秒，如图：</font>
![引导](https://wx2.sinaimg.cn/mw690/0068Se8Tly1fnxc6he4lwj30ic0dnq3g.jpg)

* <font size=3>打开第四个选项卡“启动”，打开任务管理器，关闭那些自启动的软件，如图：</font>
![启动](https://wx3.sinaimg.cn/mw690/0068Se8Tly1fnxcib6km6j30if0gmaav.jpg)

## 四.取消不必要的计划任务及磁盘清理

### 1.取消不必要的计划任务
* <font size=3>有些人以为将软件自启禁用就万事大吉了，但是有些软件它会自动创建启动计划，所以还是有必要将其禁用的</font>
* <font size=3>右键开始菜单图标或`Win+X`，点击`计算机管理`，进入`任务和计划程序`，再进入`任务计划程序库`，右键点击需要关闭的计划任务，选择`禁用`即可，如图</font>
![取消不必要的计划任务](https://wx2.sinaimg.cn/mw690/0068Se8Tly1fnxcefxgsjj30rc0hewgq.jpg)

### 2.磁盘清理
* <font size=3>一些简单的清理其实根本没必要去使用第三方软件，windows本身就有清理功能</font>
* <font size=3>打开`我的电脑`，右键`磁盘C`-`属性`–`常规`–`磁盘清理`–`清理系统文件`–这里全部勾选一下，如果有备份，就别勾选备份了，最后`确定`，如图：</font>
![磁盘清理](https://wx4.sinaimg.cn/mw690/0068Se8Tly1fnxco5usm9j30c30hct9e.jpg)

## 五.显卡优化windows设置
* <font size=3>这个显卡优化设置来自我看B站蓝视星空所Get到的</font>
* <font size=3>找到`性能监视器`（管理权限打开，Windows管理工具里面），打开`数据收集器集`-`用户定义`，空白处右键新建`数据收集器集`，手动创建，`名称：GPU`，勾选`性能计数器`和`系统配置信息`，添加，打开`RemoteFX Graphics`，找到`Frame Quality`添加进去，找到`Graphics Compression ratio`添加进去，找到`Output Frames/Second`添加进去，然后一直下一步，直到到是否创建数据收集器集，选择打开该数据收集器集的属性，完成。添加`关键字：gpu`、自己显卡的名字（设备管理器可以看到自己显卡的名字）和2，停止条件，勾选总持续时间，并改为3秒，应用，确定，然后会有两个文件，一个性能计数器，一个配置，右键性能计数器属性，示例间隔改为144，最大示例打钩，改为288，确定，并重启</font>
![显卡优化](https://wx1.sinaimg.cn/mw690/0068Se8Tly1fnxejixlhdj30d00g8dg1.jpg)

## 六.CPU优化winodws设置
* <font size=3>这个CPU优化设置来自我看B站蓝视星空所Get到的</font>
* <font size=3>首先看一下自己cpu的线程数，1.修改系统配置，运行-`MSCONFIG`，`引导`-`高级选项`，勾选`处理器个数`，及选择你的`最大线程数目`，
确定。2.打开`性能监视器`（管理权限打开，Windows管理工具里面），打开`数据收集器集`-`用户定义`，空白处右键新建`数据收集器集`，手动创建，`名称：CPU`，勾选`性能计数器`，添加，找到`Processor`，浏览对象的实例选择最大线程数减一的那个值添加进去，打开`Process`，找到`Thread Count`添加进去，确定，然后重启。</font>
![CPU优化](https://wx1.sinaimg.cn/mw690/0068Se8Tly1fnxkoryhfwj30cs0g5q32.jpg)

## 七.网速优化windows设置
* <font size=3>这个网速优化设置来自我看B站蓝视星空所Get到的</font>

### 1.修改注册表
* <font size=3>`运行`-`RegEdit`，依次打开：</font>
> HKEY_LOCAL_MACHINE-Software-Microsoft-Windows-CurrentVersion
* <font size=3>空白处右键新建一个32位的`DWORD`值，重命名为：`MaxConnectionPerServer`，数值修改16
再空白处右键新建一个32位的DWORD值，重命名为：`MaxConnectionPer1_0Server`，数值修改16</font>

### 2.修改本地组策略编辑器
* <font size=3>`运行`-`gpEdit.msc`，`计算器配置`-`管理模板`-`网络`-`QoS数据包计划程序`，`禁用限制可保留宽带`，然后再上一个设置，`限制未完成数据包`，启用，数据包数量改为最大，40000000000</font>

### 3.运行dos命令
* <font size=3>`运行`-`cmd`(管理员权限)，输入下面代码，出现确定，重启即可</font>
``` html
netsh interface tcp set global autotuning = disabled
```

## 八.其他设置
* <font size=3>其实做完了以上的优化，基本上windows系统的优化已经好了，作为用户似乎所能做到的已经到了极限，但其实不然，大牛们似乎总有新的黑科技能对系统进行优化，所以这里推荐使用`Dism++`这款第三方优化设置软件，里面还有具体很多的个性化设置或是服务禁用等，至于其他管家或者安全中心之类的软件，说实话，安了还不如不安。当然智者见智，仁者见仁，这些使用习惯没什么好去争论的。</font>
![Dism++](https://wx1.sinaimg.cn/mw690/0068Se8Tly1fnxl9zc2s7j30r30ddq3g.jpg)