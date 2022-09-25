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

## 项目初始化

### 后端

#### 技术栈

node.js + express

#### 初次使用

终端键入：

1. `npm init -y` 初始化项目
2. `npm i express` 下载express框架
3. 键入测试代码：

    ```Javascript
    //1. 引入express
    const express = require('express')

    //2. 创建应用对象
    const app = express()

    /* 
        3. 创建路由规则
        request 是对请求报文对封装
        response 是对响应报文对封装 
    */
    app.get('/',(request,response)=>{
        response.send("hello express")
    })

    //4. 监听端口启动服务
    app.listen(8000,()=>{
        console.log("服务已经启动，在8000端口监听")
    })
    ```

4. 本地输入 `localhost:8000` 查看到页面中出现 hello
5. 打开网络，查看当前请求到**标头**、**预览**、**响应**

## GET 请求

### 前端

1. 使用按钮控制发送 Ajax请求
2. 下方文本框接受内容

代码如下：

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>AJAX GET 请求</title>
</head>
<body>
    <button class="btn">发送GET</button>
    <div id="result"></div>
    <script>
        // 获取button元素
        const btn = document.querySelector('.btn')
        // 获取result文本框
        const res = document.getElementById('result')
        // 绑定事件
        btn.onclick = function(){
            // 1. 创建对象
            const xhr = new XMLHttpRequest()
            // 2. 设置请求方法和URL
            xhr.open('GET','http://localhost:8000/server?a=1&b=2&c=3')
            // 3. 发送请求
            xhr.send()
            // 4. 事件绑定 处理服务端返回到结果
            // on 事件状态 when 当...时候
            // readystate 是shr的属性，表示xhr对象状态，有 0 初始化对象 1 已open 2 已发送请求 3 部分数据返回 4 全部数据返回 五种状态
            // change 改变 对应上述有四次改变
            xhr.onreadystatechange = function(){
                // 判断（服务端返回了全部数据）
                if(xhr.readyState === 4){
                    // 判断响应状态码是否成功
                    if(xhr.status >= 200 && xhr.status <300) {
                        // 处理结果 行 头 空行 体
                        console.log(xhr)
                        // 1. 响应行
                        console.log(xhr.status) // 状态码
                        console.log(xhr.statusText) // 状态字符串
                        // 2. 响应头
                        console.log(xhr.getAllResponseHeaders()) //所有响应头
                        // 3. 响应体
                        console.log(xhr.response) // 响应体
                    res.innerHTML = xhr.response
                    }
                }
            }
        }
    </script>
</body>
</html>
```

### 后端

修改上述代码，如下：

```Javascript
    //1. 引入express
    const express = require('express')

    //2. 创建应用对象
    const app = express()

    /* 
        3. 创建路由规则
        request 是对请求报文对封装
        response 是对响应报文对封装 
    */
    // 修改路由地址
    app.get('/server',(request,response)=>{

        response.send("hello express")
    })

    //4. 监听端口启动服务
    app.listen(8000,()=>{
        console.log("服务已经启动，在8000端口监听")
    })
```

## POST 请求

### 前端

```Javascript
const xhr = XMLHttpRequest()
xhr.open('POST','http://localhost:8000/server')
xhr.send('a=1&b=2&c=3')
```

### 后端

```Javascript
app.post('/server',(request,response)=>{
    // 设置响应头 允许跨域
    response.setHeader('Access-Control-Allow-Origin','*')
    // 设置响应体
    response.send("hello AJAX POST")
})
```
