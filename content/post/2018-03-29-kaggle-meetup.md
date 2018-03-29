---
title: kaggle_meetup
author: shuai
date: '2018-03-29'
slug: kaggle-meetup
categories:
  - kaggle
  - meetup
tags:
  - cdiscount
  - classify tge catalog with image
header:
  caption: ''
  image: ''
---

自从一年前去徒步崴伤了脚踝，几乎就没有参加过任何的meetup。今晚终于有动力跑来参加一个[kaggle的meetup](https://www.meetup.com/Kaggle-Paris-Meetup/events/247658535/)。

第一个分享的主题是Cdiscount的DS介绍他们的一个kaggle竞赛的结果。是用图片对产品进行分类。
这里就介绍一下前几名的解决方案吧。
1. bestfitting ： 0.79567 第一名是中国人 :)
2. : 0.79352 
3. dylan 0.79046 也是中国人：）

前三名的相同点：
SOA architectures
  Resnet inceptionResNetV2 Xception
  InceptionV3 ResNext SE-block
  DenseNet Dual Path Network
GPU+SSD(可以赢得时间)
Ensemble of models（很难在PROD中实现）

Dylan ： 8GPU on a single machine

Parameters :
  Optimiszer
    NAdam
  Data augmentation
    Horizontal flip only
  No Dropout

Trqining Speed  
  14 hr per epoch
Reduced image size to 160*160
  +25 PTS training speed
  -0.003 on local validation
  
Use MD5 hash ??
why ？ 没听懂。。。


2eme :
GTX1080

Number of image
Image order important !!



1:
12 GPUs (1080 4 Tian X)
1300 hrs of training

performance par categorie : 发现 bad performance for books and CDs
就专门为这两个cat建模，得到一个较好的结果

OCR +0.14



第二个分享的人很有趣，是世界上唯一一个靠嘴炮得到GrandMaster的，叫CPMP Jean-Francois Puget。（“n°1 GrandMaster (only one in the world !) for discussion tasks”）

不过这个人一上来一直在吐槽中国人。。。因为他被一个中国人骗过一次。那个和他组队的中国人被发现在一个比赛中有三个compte，导致全队的都被取消成绩。



他的思路：


baseline :
先写好submission的code
做一个最简单的model
试一些复杂一点的models
慢慢的加入engineered features

CV setting :
Goal : 知道是否加入的新feature或使用的新model比之前的好 private LB score，

正确的方法：
用training model去validate model或是feature engineering
K fold cross validation （k>3 and k<10）

for Time based cross validation if time dependant data
  train on all train periods except last, and predict on last
  then retrian on all data and submit
  









