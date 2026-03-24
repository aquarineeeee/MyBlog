---
title: 从0开始编译Aseprite
date: 2026-03-23
tags: 
  - 编译
  - C++
categories:
  - 技术随笔
description: |
  起因是想做出一些用于开发的8-bit sprite动画
  算是自用存档吧，记录一下第一次编译这种开源项目
  也可以当作一篇教程，希望对看到的你有帮助
  源代码链接：https://github.com/aseprite/aseprite
comments: false
toc: true
toc_number: false
toc_style_simple:
---
## 起因
其实没什么好说的，一直很喜欢像素艺术（你怎么知道我有美术功底），高中就听说aseprite大名了但苦于价格没有下手。
**刚好**前段时间上图形学与多媒体技术的时候**碰巧**了解到了贝尔抖动（这不就是我最喜欢的半色调吗！这不就是《奥博拉丁的回归》用到的算法吗！）最近正好在做这个网站，想要像素感的界面，就想起了aseprite,本来准备买下但是突然看到有源代码，那还说啥了自己编译吧！前一天晚上想到做这个，今天起来两眼一睁就是干，现在看来那节课也算是埋下了伏笔。
## 编译大冒险
最开始其实有点无处下手，不过好在官方文档https://github.com/aseprite/aseprite/blob/main/INSTALL.md 写得很详细，可以一步一步跟着做。Aseprite90%以上都是用的c/c++，看到真是感觉非常亲切。
虽然要准备有点繁琐，但是不难，花时间最长的反而只是下载源代码。
### 依赖
整个编译过程最重要的就是准备依赖！真正的编译过程其实只有几分钟
- cmake
用choco下的。
最开始以为要去官网下，配置ninja环境变量的时候发现有choco,就直接用choco下了
- ninja
其实需要的ninja只是一个exe,就把VS里面的单独拎出来用了（太方便了）
- skia
官方文档里面给的预编译package
- Visual Studio Community 2022 
文档里面强制指定的，不过学计算机应该都下了吧
- Windows 10.0.26100.0 SDK from Visual Studio installer
更方便了，让VS自己下，唯一要留意的是版本编号
### 构建
看到有自动构建时以为很方便，结果自动构建问题太多了，看着是build.cmd双击即可运行，但实际上cmd还套了一连串：
- build.ps1
- build.sh
- PowerShell
- Git Bash
- Visual Studio

根本不能识别cmd配好的环境变量,直接转手动构建：
- 打开VS终端（不要用普通终端）
```x64 Native Tools Command Prompt for VS 2022
call "C:\Program Files\Microsoft Visual Studio\2022\Community\Common7\Tools\VsDevCmd.bat" -arch=x64
```
- 输入
```x64 Native Tools Command Prompt for VS 2022
cd aseprite
mkdir build
cd build
cmake -DCMAKE_BUILD_TYPE=RelWithDebInfo -DLAF_BACKEND=skia -DSKIA_DIR=C:\deps\skia -DSKIA_LIBRARY_DIR=C:\deps\skia\out\Release-x64 -DSKIA_LIBRARY=C:\deps\skia\out\Release-x64\skia.lib -G Ninja ..
ninja aseprite
```
其中skia换成你自己的路径。
然后你等着程序自己运行就好。
贴张构建截图：
![终端的输出](/images/building1.png)
大功告成！
![最终成果](/images/finally.png)
## 随笔
之前从来没有接触过这种程度的编译，都是在IDE里面直接编译了，编译出来真是非常有成就感，对我来说是一次很有趣的经历。
感谢Aseprite的作者和开源社区，也感谢指导文档的作者~