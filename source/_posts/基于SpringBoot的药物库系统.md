---
title: 基于SpringBoot的药物库系统
date: 2026-03-21 
tags: 
  - Web开发
  - SpringBoot
  - Java
  - MySQL
  - Redis
categories:
  - 项目
description: |
  Web开发基础与主流框架应用、前后端交互与文件传输、API调用与权限管理
  SpringBoot, maven, java, MySQL, redis, MyBatis, ORM框架
  项目链接：https://gitee.com/Reetr0/medicine-system（更详细有代码解析的文档在仓库文件夹里面）
  已部署到阿里云：
comments: false
toc: true
toc_number: false
toc_style_simple:
---
# 简介
一个基于Spring Boot和MyBatis的医疗管理应用，主要实现了药物信息管理、患者管理、医生管理和权限控制等功能。系统采用了分层架构设计，实现了RESTful API接口，支持多角色访问控制和数据缓存功能。

1. 药物信息的增删改查操作
2. 患者信息管理
3. 医生信息管理
4. 权限控制和访问管理
5. 数据缓存和性能优化
6. 分页查询和数据展示
7. 前后端分离的页面展示

---

# 预览
设计的时候考虑到属于医疗系统，登录时需要先勾选角色“患者/医生/管理员”再输入用户名密码，注册也需要（一个用户可能既是医生又是患者）
![登录页面](/images/login.png)
![医生页面](/images/doctor.png)
![患者页面](/images/patient.png)
![患者页面ai功能](/images/patient-ai.png)
![管理员页面](/images/admin1.png)
![管理员页面](/images/admin2.png)
![管理员页面](/images/admin3.png)

---

# 技术栈
## SpringBoot

因为方便，可以自动配置很多东西，还内置了tomcat，这个项目就是用的tomcat

## RESTful API

后端通过Controller暴露接口，前端通过HTTP请求与后端进行数据交互。

## 文件上传与下载

专门写了一个文件处理类，可以上传和下载markdown文件（比如那个ai接口，ai的回答就可以保存md）

## 第三方 API

老师给的deepseek密钥k-1e65951420154b4890abc671bb466f53，不过缺点就是比较慢

## RBAC权限模型

采用JWT完成身份验证。用户登录成功后，系统生成Token，前端在后续请求中携带该Token访问受保护资源。


## MySQL

创建了一个数据库“medicine_system”。MySQL确实好用，但是很崩溃的是有次数据库怎么都连接不上，其他都可以，只有重新弄一个，还好当时里面没什么数据

## ORM框架

引入ORM减少手写SQL代码

## 数据库事务

@transaction保证数据的完整性和一致性

## Redis

非常好用，不过测试的时候发现改数据库网页里面要等一会才会生效，为了测试方便所以给自己加了一个强制刷新缓存的功能


---

# 技术随笔

其实写增改删查是最简单的，写各种controller才是最痛苦的，要一个一个改