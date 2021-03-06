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

KEGG 或者GO富集分析的软件和网站有很多。模式生物可以用网站或者专门的包来做富集分析。如：
[clusterProfiler](http://www.bioconductor.org/packages/release/bioc/html/clusterProfiler.html)

网页版有
[metascape](http://metascape.org/gp/index.html)

[DAVID](https://david.ncifcrf.gov)

[NOA(官网维护中）](http://europepmc.org/articles/pmc3141273)

非模式生物可以用一些软件包如TBtools手动输入背景注释，差异基因来进行富集分析。

（代码有空再上传）
