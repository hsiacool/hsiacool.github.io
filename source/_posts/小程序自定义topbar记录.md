---
title: 小程序自定义topbar记录
date: 2021-01-23 14:41:09
tags: 小程序
categories: 教程与记录
---
整体思路是先定义自定义模式，后将自定义的那部分作为组件呈现
1.首先需要在全局先注册自定义tabbar,自定义模式"custom": true,其他所需参数补齐
```
//app.json
"tabBar": {
    "custom": true,
    "color": "#555555",
    "selectedColor": "#336DFF",
    "backgroundColor": "#fff",
    "list": [
      {
      "pagePath": "pages/index/index",
      "iconPath": "images/common/home.png",
      "selectedIconPath": "images/common/home-active.png",
      "text": "首页"
      },
      {
        "pagePath": "pages/index/index",
        "text": "组件"
        },
      {
        "pagePath": "pages/mine/index",
        "iconPath": "images/common/mine.png",
        "selectedIconPath": "images/common/mine-active.png",
        "text": "接口"
      }
    ]
  }
  ```
  2.根目录下新建custom-tab-bar，使用组件形式自定义tabbar

  ### 出现的问题
  1.点击tabbar的时候图标闪烁，不能及时切换的问题，此时需要在每个tab点击后要到达的页面写上以下代码，重新去确定selected
  ```
  onShow(){
   if (typeof this.getTabBar === 'function' && this.getTabBar()) {
     this.getTabBar().setData({
       selected: 0//这里是本页面在tabbar实例中的index
     })
   }
 }
 ```
2.在实际写项目的时候，出现了使用wx.navigateTo或navigate标签跳转层级过深，出现无法跳转的情况，这是由于小程序本身限制，层级不可超过10栈
解决方案：可以使用wx.navigateBack退回上级目录，减少栈的增加
注：使用navigator标签跳转的时候要注意跳到什么页面，open-type默认值是navigate，无法跳到switchTab页面，需要修改open-type值
