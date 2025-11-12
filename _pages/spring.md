---
title: Spring
author: Chu Ying
date: 2022-02-04
category: java
layout: post
---
>
浏览器请求

    ↓
    
Controller接收请求 → 从Model获取数据

    ↓
    
调用Service处理业务逻辑

    ↓
    
Service调用Repository访问数据库

    ↓
    
Repository通过Entity操作数据库表

    ↓
    
数据返回 → Service → Controller

    ↓
    
Controller将数据放入Model → 指定模板文件

    ↓
    
模板引擎结合Model数据 + HTML模板

    ↓
    
生成最终HTML → 返回浏览器

    ↓
    
浏览器加载HTML + static中的静态资源







