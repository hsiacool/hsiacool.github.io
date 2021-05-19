---
title: 前端服务器代理/proxyTable
date: 2021-05-18 10:55:37
tags: 服务器
categories: 理解与总结
---
使用场景：当后端无法提供跨域服务，需要前端自行搭建代理服务器进行跨域
原理：浏览器有同源策略限制，无法跨域请求资源，因为服务器无跨域限制，此时可以搭建使用webpack提供的代理服务器去访问真实资源，代理服务器与浏览器同源。
```
proxyTable: {
  // 这里配置 '/api' 就等价于 target , 你在链接里访问 /api === https://localhost:54321
  '/api': {
    target: 'https://localhost:54321/', // 真是服务器的接口地址 // https://localhost:54321/json.data.json,
    secure: true, // 如果是 https ,需要开启这个选项
    changeOrigin: true, // 是否是跨域请求
    pathRewirte: {
      // 这里是追加链接,比如真是接口里包含了 /api,就需要这样配置.
      '/^api': 'api/',
      // 等价于
      // step 1  /api = http://localhost:54321/
      // step 2 /^api = /api + api == http://localhost:54321/api
    }
  }
 },
```
注：真实发布环境不起作用
### 引申问题：如果在开发中与多位后端人员共同开发（地址不同），如何设置proxy？
思路：主要思路是去访问一个假地址，当在假地址上判断出有xx关键词，就把这个假地址重写成真正的地址
### 一、配置所有后台地址服务
```
// proxyTarget.js
module.exports = {
  local: 'http://127.0.0.1:8080', // 本地
  sit: 'https://xxx.com/', // sit
  uat: 'http://100.xxx.xxx.xxx:8088/', // uat
}
```
### 二、新建baseUrl.js，写要访问的假地址baseUrl
```
// baseUrl.js

let baseURL = ''
//切换地址时只需要修改此处即可
let localPath = 'local' // 本地
// let localPath = 'sit' // di
// let localPath = 'uat' // uat

if (process.env.NODE_ENV === 'development') {
  baseURL = `/${localPath}/devApi`
} else {
  baseURL = '/api'
}

export default baseURL
```
### 三、更改webpack.dev.conf.js中的devServer
```
const path = require('path')
const targets = require('../proxyTarget')

const proxyInfo = (name)=>{
  return {
    target:targets[name],
    changeOrigin:true,
    ws:true,
    pathRewrite:{
      [`/${name}`]:''
    }
  }
}
const proxy = {};
//对每个接口地址进行处理，之后组成一个真实地址的proxy配置
Object.keys(targets).forEach(targetName=>{
  proxy[`/${targetName}`] = proxyInfo(targetName)
  })
```
### 四、把第三步组成的proxy配置传入
```
module.exports = {
    dev: {
        proxyTable: proxy
    }
}
```
