---
layout: post
title:  KEGG GO GESA enrich analysis
date:   2019-05-16 01:08:00 +0800
categories: document
tag: 教程
---



#超几何分布Hypergeometric Distribution#
====================================
基因的数据是离散的。对基因进行富集分析，类似于高中数学中从黑盒子里取不同颜色的小球，每次取完不放回。比如，当盒子里面有10个红球和10个白球时，不放回地取10次，理论上有5次是白球，5次是红球。这种情况就代表基因的表达量是相同的。但是当取到8次白球，2次红球的时候，我们就认为白球的“表达量”更高。可以计算具体的p值。

超几何分布的前提是数据是离散的（基因ID并不连续），数据的总量是已知的（基因总数已知），数据的组成是已知的（基因组注释比较完全）。对于未知物种和无参考基因组的物种，是难以进行基因的富集分析的。

在一次实验中，总数为N的基因列表（表达的基因或者基因组）中中有M个基因和某过程相关，每次抽n个基因，其中所得和该相关基因的数量X=k，那么

$$P_(x=k)=\frac{C_{M}^{k}C_{N-M}^{N-k}}{C_{N}^{n}}$$

该公式计算出来的P值是x=k的情况，也就是说有k=1个基因的概率或者k=2或k=n的概率，在进行假设检验时，我们需要将各种情况的p值累加起来。

$$P=1-\sum_{k=0}^{n}\frac{C_{M}^{k}C_{N-M}^{N-k}}{C_{N}^{n}}$$

认为P<0.05的信号通路为富集分析得到的显著性结果。然而，即便如此，假阳性依旧有5%的可能出现，当富集到的信号通路特别多，例如有100条时，可能就有5条为错误的富集。因此，要进行多重假设检验。

多重假设检验的方法有很多，比如Bonferroni法就是强行降低P值，当进行了100次的假设检验，就认为p<0.0005时才有显著性意义。

FDR法则通过控制false discovery rate来校正P值，计算FP/(TP+FP)的期望值，如果期望值小于我们的阈值0.05，则认为该检验的结果具有生物学意义。

还是要根据生物学表型，具体情况具体分析。
使用							{#How-to-use}
====================================

下载							{#Download}
------------------------------------

使用git从[LessOrMore](https://github.com/luoyan35714/LessOrMore.git)主页下载项目

```bash
git clone https://github.com/luoyan35714/LessOrMore.git
```


$$a*b$$
<p>
\begin{align}\notag 
\dot{x}&=\mathbf{A}x+\mathbf{B}u\\
y&=\begin{bmatrix}1&0\\
0&1\end{bmatrix}x+\begin{bmatrix}1&0\\
0&1\end{bmatrix}u
\end{align}
</p>

配置							{#Configuration}
------------------------------------

`LessOrMore`项目需要配置的只有一个文件`_config.yml`，打开之后按照如下进行配置。

> 特别注意`baseurl`的配置。如果是`***.github.io`项目，不修改为空''的话，会导致JS,CSS等静态资源无法找到的错误

```bash
name: 博客名称
email: 邮箱地址
author: 作者名
url: 个人网站
### baseurl修改为项目名，如果项目是'***.github.io'，则设置为空''
baseurl: "/LessOrMore"
resume_site: 个人简历网站
github: github地址
github_username: github用户名称
FB:
  comments :
    provider : duoshuo
    duoshuo:
        short_name : 多说账户
    disqus :
        short_name : Disqus账户
```

如何写文章							{#How-to-write-document}
------------------------------------

在`LessOrMore/_posts`目录下新建一个文件，可以创建文件夹并在文件夹中添加文件，方便维护。在新建文件中粘贴如下信息，并修改以下的`titile`,`date`,`categories`,`tag`的相关信息，添加`* content {:toc}`为目录相关信息，在进行正文书写前需要在目录和正文之间输入至少2行空行。然后按照正常的Markdown语法书写正文。

```bash
---
layout: post
#标题配置
title:  标题
#时间配置
date:   2016-08-27 01:08:00 +0800
#大类配置
categories: document
#小类配置
tag: 教程
---

* content
{:toc}


我是正文。我是正文。我是正文。我是正文。我是正文。我是正文。
```

执行							{#execute}
------------------------------------

```bash
jekyll server
```

效果							{#result}
------------------------------------
打开浏览器并输入URL`http://localhost:4000/`,回车。


为什么重复造轮子					{#why}
====================================

很明显，我在重复造轮子。在13年接触到GIT，14年末接触到Jekyll，然后搭建了自己的博客，当时是选用了[JekyllThemes](http://jekyllthemes.org/)上的[Solar](https://github.com/mattvh/solar-theme-jekyll)主题，一直到现在。不过中间一直感觉页面风格还是偏暗，阅读不方便。并且有一些小的细节做的不是很好。在页面的跨平台浏览上有一些瑕疵。并且不区分一级标题和二级标题，导致没有重点强调。诸如此类，用了2年，用的越多，越发吃力，中间就一直在寻找新的能够让我一眼认定的主题。

虽然设计好看的主题很多。但是真正适合拿来做博客的却不多。中间一直没有找到合适的主题。直到有一天看到Less官网的主题之后，豁然觉得这就是我的博客想要的样子。简单而又不平凡。所以就决定了要把博客迁移到这个主题，然后拿了两天晚上来把这个主题做出来。

重复造了轮子，但是这个是迄今为止自己觉得最适合我的博客的轮子，所以是值得的！

关于作者						{#about-author}
====================================

热爱开源，热爱折腾的Java程序猿。更多个人信息和联系方式可以参照[我的简介](http://www.hifreud.com/Resume.io/)。