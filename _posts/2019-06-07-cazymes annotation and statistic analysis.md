---
layout: post
title:  KEGG GO GESA enrich analysis
date:   2019-06-07 01:08:00 +0800
categories: document
tag: 教程
---



下载数据
====================================

## 蛋白质组序列下载 Download Proteome sequence

之前发现通过wget ftp://ftp.uniprot.org/pub/databases/uniprot/current_release/knowledgebase/reference_proteomes/Bacteria/*.fasta.gz 只能下载参考基因组对应的蛋白质序列。

后来通过[biostars](https://www.biostars.org/p/292993/)了解到可以通过 https://www.uniprot.org/uniprot/?query=proteome:UP000005640&format=fasta 下载，但是不能自动命名很麻烦。

最后我用RCurl这个R包进行批量下载。

write.table(getURL("https://www.uniprot.org/uniprot/?query=proteome:UP000000815&format=fasta"),file="~/test2/R/genome/UP000000815.fasta",quote=F,col.name=F,row.names=F)

用Excel生成批量下载脚本。

CAZYmes注释
=====================================

Cazymes为碳水化合物活性酶，其在线注释网站为http://bcb.unl.edu/dbCAN2/，但在线注释不能改参数。所以采用本地注释。

注释用的Database从[dbCAN2](http://bcb.unl.edu/dbCAN2/download/Databases/) 下载
