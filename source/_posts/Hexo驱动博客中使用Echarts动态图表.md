---
title: Hexo中插入使用Echarts动态图表
tags:
  - 记录
  - 教程
  - Hexo博客
reward: true
toc: false
abbrlink: 54640
date: 2018-04-04 17:13:06
---
![zhuyetu](https://wx3.sinaimg.cn/mw690/0068Se8Tgy1fq1kbbge2wj30cq05ktb3.jpg)
## 前言
* <font size=3>[ECharts](https://echarts.baidu.com/)，一个用较少的代码实现比较酷炫的动态数据统计表的图标库。</font>
<!-- more --> 

## 安装ECharts
* <font size=3>在博客站点目录下执行：</font>
```
npm install hexo-tag-echarts --save
```
* <font size=3>在所用主题目录下`layout\_partial`中的`head.ejs`里加入：</font>
``` html
<script src="https://echarts.baidu.com/dist/echarts.common.min.js"></script>
```
* <font size=3>或者直接到[ECharts下载页面](https://echarts.baidu.com/download.html)里面去下下载js文件放在`js目录`下并在`head.ejs`里加入：</font>
``` html
<script type="text/javascript" src="/js/echarts.min.js"></script>
```
* <font size=3>最后直接在文章中引入echarts，复制option部分，形成下面这个样式就可以了</font>
``` JavaScript
{% echarts 400 '85%' %}
\\TODO option goes here
{% endecharts %}
```
* <font size=3>下面这段是前面图表的代码：</font>
``` JavaScript
{% echarts 400 '81%' %}
{
tooltip : {
        trigger: 'axis',
        axisPointer : {            // 坐标轴指示器，坐标轴触发有效
            type : 'shadow'        // 默认为直线，可选为：'line' | 'shadow'
        }
    },
    legend: {
        data:['直接访问','邮件营销','联盟广告','视频广告','搜索引擎','百度']
    },
    grid: {
        left: '3%',
        right: '4%',
        bottom: '3%',
        containLabel: true
    },
    xAxis : [
        {
            type : 'category',
            data : ['周一','周二','周三','周四','周五','周六','周日']
        }
    ],
    yAxis : [
        {
            type : 'value'
        }
    ],
    series : [
        {
            name:'直接访问',
            type:'bar',
            data:[320, 332, 301, 334, 390, 330, 320]
        },
        {
            name:'邮件营销',
            type:'bar',
            stack: '广告',
            data:[120, 132, 101, 134, 90, 230, 210]
        },
        {
            name:'联盟广告',
            type:'bar',
            stack: '广告',
            data:[220, 182, 191, 234, 290, 330, 310]
        },
        {
            name:'视频广告',
            type:'bar',
            stack: '广告',
            data:[150, 232, 201, 154, 190, 330, 410]
        },
        {
            name:'搜索引擎',
            type:'bar',
            data:[862, 1018, 964, 1026, 1679, 1600, 1570],
            markLine : {
                lineStyle: {
                    normal: {
                        type: 'dashed'
                    }
                },
                data : [
                    [{type : 'min'}, {type : 'max'}]
                ]
            }
        },
        {
            name:'百度',
            type:'bar',
            barWidth : 5,
            stack: '搜索引擎',
            data:[620, 732, 701, 734, 1090, 1130, 1120]
        },
    ]
};
{% endecharts %}
```
* <font size=3>其中，参数400指定图表展示的高度为400px，81%则指定图表展示的宽度为81%，如不写明这两项参数则默认值为高度400px，宽度81%。</font>

## 参考
[在 Hexo 中插入 ECharts 动态图表](https://kchen.cc/2016/11/05/echarts-in-hexo/)
[Hexo驱动博客中使用Echarts动态图表](https://www.jianshu.com/p/8ae0d3b734ed)