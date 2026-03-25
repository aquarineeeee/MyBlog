---
title: 基于QT开发导航系统
date: 2026-03-21 15:48:07
tags: 
  - QT
  - C++
  - 最短路径算法
categories:
  - 项目
description: |
  纯C++实现重庆轨道交通的导航系统
  项目链接：https://gitee.com/Reetr0/cq-metro
comments: false
copyright: false
copyright_author: false
copyright_author_href: false
copyright_url: false
copyright_info: false
---
## 简介

一个用QT开发的导航系统，可以根据起点和终点规划路线（主要是Dijkstra算法）纯C++实现。

---

## 预览
![导航系统预览](/images/metroline.png)
（现在看来这个真的太简陋了，当时调QT的依赖真是调得晕头转向，不过好在导航功能还是能用的对吧！）

---

## 技术随笔

实际上这个项目开发的时候相当痛苦，因为QT太难用了（真的很难用...）而且网上也没有多少相关的文档，教学视频也没有，ui功能更是难用中的难用（如果算是ui功能的话），动不动就报错，当时边做边想这个还不如我自己用终端手搓呢...算是我心中同类产品里面最难用的了...也可能是我还没找到正确的打开方式吧...
留下的印象实在太深刻，不过听说新版微信居然是用QT开发的，也许是我还没发掘QT的优势？