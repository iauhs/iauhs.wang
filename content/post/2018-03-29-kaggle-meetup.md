---
title: kaggle_meetup
author: shuai
date: '2018-03-29'
categories:
  - kaggle
  - meetup
tags:
  - cdiscount
  - classify tge catalog with image
slug: kaggle-meetup
header:
  caption: ''
  image: ''
---

自从一年前去徒步崴伤了脚踝，几乎就没有参加过任何的meetup。今晚终于有动力跑来参加一个[kaggle的meetup](https://www.meetup.com/Kaggle-Paris-Meetup/events/247658535/)。

第一个分享的主题是Cdiscount的DS介绍他们的一个kaggle竞赛的结果。是用图片对产品进行分类。
这里就简单介绍一下前几名的解决方案吧。

1. bestfitting : 0.79567 第一名是中国人 :)
2. conv.pred. : 0.79352 队中也有两个中国人！
3. dylan : 0.79046 也是中国人：）

前三名的相同点：

* SOA architectures
  * Resnet inceptionResNetV2 Xception
  * InceptionV3 ResNext SE-block
  * DenseNet Dual Path Network
* 硬件 ：GPU+SSD(可以赢得时间)
* Ensemble of models（很难在PROD中实现）

3rd place, Dylan ： 8GPU on a single machine

Parameters : (完全不懂，有空要看一下图像识别的东西)

  * Optimiszer
    * NAdam
  * Data augmentation
    * Horizontal flip only
  * No Dropout

Training Speed  
  * 14 hr per epoch
  
Reduced image size to 160*160   
  * +25 PTS training speed  
  * -0.003 on local validation
  
Use MD5 hash ??
why ？ 没听懂。。。


2eme : team of 3 people, weighted result on validation set
GTX1080

Intrest point :  
* Number of image
* Image order important !!



1 place, bestfitting :
12 GPUs (1080 4 Titan X)
1300 hrs of training

performance par categorie : 发现 bad performance for books and CDs
就专门为这两个cat建模，得到一个较好的结果: OCR +0.14

最后结论中有关于线上Prod系统的三个难点 ： 
* Per category precision
* Re-training
* Ensemble de model


第二个分享的人很有趣，是世界上唯一一个靠嘴炮得到GrandMaster的:)叫Jean-Francois Puget。（“n°1 GrandMaster (only one in the world !) for discussion tasks”）

不过这个人一上来一直在吐槽中国人。。。因为他被一个中国人骗过一次。那个和他组队的中国人被发现在一个比赛中有三个compte，导致全队的都被取消成绩。



他的思路：

* baseline :
  * 先写好submission的code
  * 做一个最简单的model
  * 试一些复杂一点的models
  * 慢慢的加入engineered features

* CV setting :
Goal : 知道是否加入的新feature或使用的新model比之前的好 private LB score，

正确的方法：
用training model去validate model或是feature engineering
K fold cross validation （k>3 and k<10）

for Time based cross validation if time dependant data
  train on all train periods except last, and predict on last
  then retrian on all data and submit
  
EX. 
CV score : M1 : 0.98040 (LB pubilc)
          M2 : 0.97937 (CR result)

Train score :
0.99004
0.98313

Look at the gap between train and val score, a large gap is an indication of overfitting.
When there are changes, check that it change not the score a lot 

FE :
try a lot and fail fast
try common sense ideas
  try to understand the underlying bussiness
  in 2 sigma rental, trained a model to predic prices then used the delta between predicted price and actuel price to predict interest
  
try usual suspects
  counts
  targeting encoding
  clustering
  sin(x),cos(x) for hours, minutes, days不理解为什么要这样做。。。
  lag variables for time series


这个人应该有点老。。。说话好慢啊！！比我记得还慢 :)让我想到了 闪电！：）


HPO :

tune algo/model parameters

impossible without reliable validation setting
donot overtune your parameters

xgboost/lightgbm :
  start with subsample = 0.7
  play with 
  
  
Ensembling

use same folds for all models (CV)
"ensembleing guide kaggle"

Practice
reqd best solution after each competition


share what i find :) --> discussion grand master
这个人真的很爱分享：）


