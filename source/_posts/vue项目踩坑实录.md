---
title: vue项目踩坑实录
date: 2021-02-24 16:38:50
tags: vue
categories: 教程与记录
---
### 1.项目中使用了sass，然而在进行打包时未成功，报错显示 unknown word
经查，写代码时不小心使用了//注释方式，经过webpack.prod.config.js的代码压缩，就造成了语法错误的情况，代码里尽量不要使用//这种注释方法

### 2.图片放到线上发现无法显示
1.图片路径的问题，可以查一下打包文件build/utils.js里的publicPath问题
2.访问路径的问题，查一下config/index.js文件，可能是文件层级问题，将绝对路径assetsPublicPath: '/'改为相对路径assetsPublicPath: './'

### 3.webpack打包去掉console.log
```
//webpack.prod.conf.js
new UglifyJsPlugin({
  uglifyOptions: {
    compress: {
      warnings: false,
      drop_debugger: true,
      drop_console: true //更改此行为true
    }
  },
  sourceMap: config.build.productionSourceMap,
  parallel: true
})
```

### 4.当页面中有定时器时，离开页面需要手动销毁定时器
```
const getNow = setInterval(() =>{
    setTimeout(function(){
      that.getNowTime();
    },0)
}, 1000);
that.$once('hook:beforeDestroy', () => {
    clearInterval(getNow);
})
```

### 5.vue-cli2和vue-cli3的区别
1.包名称由vue-cli改成了@vue/cli
2.vue-cli3继承了webpack，使用vue-cli3创建的项目在配置webpack的时候可以直接在vue.config.js里面配置

### 6.项目中引入了node-sass，后和同事统一了node版本，项目报错
原因：node-sass依赖于node，故更新node也要更新node-sass
这里记录一下node-sass，sass-loader，style-loader三个的关系：
sass-loader：加载sass/scss, 并且把sass/scss编译成css,依赖于node-sass,所以使用时要先下载node-sass
style-loader（官方封装了vue-style-loader）：将JS字符串生成为style节点、将样式插入到style标签
css-loader（自带）：将CSS转化成CommonJS模块，例如url转为require等

### 7.配置404页面
需要注意放在所有路由的最后
```
path: '*',
name: '404',
component: () => import('../views/404.vue')
```

### 8.切换路由时，要把之前页面的内容留存
1.使用keep-alive
2.在beforeRouteLeave里进行处理
