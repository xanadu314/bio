---
layout: post
title:  cazymes annotation and statistic analysis
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

注释软件为hmmer3,可以用conda安装，也可以手动编译安装。

  % wget http://eddylab.org/software/hmmer/hmmer.tar.gz 
  
  % tar zxf hmmer.tar.gz
  
  % cd hmmer-3.2.1
  
  % ./configure
  
  % make
  
  % make check
  
  % make install
  
再通过 vim ~/.bashrc_profile 将hmmer的路径添加到环境变量
  
注释脚本为：
  
  hmmscan --tblout test.txt -E 0.00001 --cpu 16 dbCAN-HMMdb-V7.txt test.fasta

用R统计注释信息
====================================

载入一些R包
library(readr)
library(stringr)
library(readr)
library(rpart)
library(dplyr)

fun1 <- function(x){
+ read.table("~/路径/x,head=TRUE)
+ }

filename <- list.files(pattern=".txt")

path <- "~/路径/"

data <- lapply(filePath, function(x){read_table2(x,col_types = cols(`E-value` = col_number(),query =col_number()) ,na = "empty",skip =1 )})


如果失败，可以用R studio自带的导入方式导入。

UP000000229 <- read_table2("UP000000229.txt", col_types = cols(`E-value` = col_number(),query = col_number()), skip = 1)

再用list将所有数据合并成一个大list

最后是去重加筛选条件
for (i in 1:最大值）

write.table(t(c(filenames_new[i],length(grep("GH",filter(data_new[i][[1]][!duplicated(data_new[i][[1]][[3]]),],query<=0.000000000000001)[[1]])),length(grep("GT",filter(data_new[i][[1]][!duplicated(data_new[i][[1]][[3]]),],query<=0.000000000000001)[[1]])),length(grep("CE",filter(data_new[i][[1]][!duplicated(data_new[i][[1]][[3]]),],query<=0.000000000000001)[[1]])),length(grep("AA",filter(data_new[i][[1]][!duplicated(data_new[i][[1]][[3]]),],query<=0.000000000000001)[[1]])),length(grep("PL",filter(data_new[i][[1]][!duplicated(data_new[i][[1]][[3]]),],query<=0.000000000000001)[[1]])),length(grep("CBM",filter(data_new[i][[1]][!duplicated(data_new[i][[1]][[3]]),],query<=0.000000000000001)[[1]])))),filenames_new[i],quote = FALSE,row.names = FALSE,col.names = FALSE)

切换到终端Terminal，用 cat **.txt > total.txt 合并txt文件

画一个箱线图

library(ggplot2)

library(ggsci)

ggplot(merge, aes(x=label,y=GT3))+geom_boxplot(aes(fill=label))+scale_fill_npg()+theme(axis.text.x = element_text(angle = 45, hjust = 1))



  
  
