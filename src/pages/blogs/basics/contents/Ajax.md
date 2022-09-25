---
layout: '../../../../layouts/BlogPost.astro'
---

# Ajax定义

> Asynchronous Javascript And XML 异步数据请求

- 一种异步无刷新加载数据方案

## XML

> 可扩展标记语言

- 用于传输和存储数据 （被JSON取代）

- 对比HTML
    1. XML数据传输，HTML数据呈现
    2. XML标签自定义，HTML标签固定

## AJAX优缺点

### 优点

1. 页面无刷新发送请求
2. 允许根据事件发送请求

### 缺点

1. 没有浏览历史，不能回退
2. 存在跨域
3. SEO不友好

# HTTP 协议

> 超文本传输协议

是一种浏览器与服务器之间的协议规定

## 请求

### 请求报文

- 格式+参数

### 格式

1. 请求行： 请求方法 请求路径 请求协议版本
2. 请求头：以键值对形势 各种请求头 如 Host Cookie Content-type User-Agent
3. 空行
4. 请求体：请求数据

## 响应

### 响应报文

1. 响应行： 协议版本 状态码 状态字符串
2. 响应头：形式同请求头
3. 空行
4. 响应体：返回数据

# Ajax 案例

## 后端

### 技术栈

node.js + express

### 初次使用

终端键入：

1. `npm init -y` 初始化项目
2. `npm i express` 下载express框架
3. 键入测试代码：

    ```node
    const { response } = require('express')
    const express = require('express')

    const app = express()

    app.get('/',(request,response)=>{
        response.send("hello express")
    })

    app.listen(8000,()=>{
        console.log("服务已经启动，在8000端口监听")
    })
    ```

4. 本地输入 `localhost:8000` 查看到页面中出现 hello
5. 打开网络，查看当前请求到**标头**、**预览**、**响应**

