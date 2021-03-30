---
title: css揭秘读书笔记
date: 2021-01-03 14:09:46
tags: css
categories: 读书笔记
---
1.transform带来的元素模糊问题
```
transform-style:preserve-3d;
```
2.定宽定高元素的垂直水平居中简化写法
```
width:0.96rem;
height:0.96rem;
position: absolute;
top:calc(50% - 0.48rem);
left:calc(50% - 0.48rem);
```
3.布局高度在一屏以内之footer吸底（当body高度大于一屏幕失效）
```
<body>
    <header></header>
    <main></main>
    <footer></footer>
</body>
body{
    display:flex;
    min-height:100vh;
    flex-flow:column;
}
main{
    flex:1
}
```
在总高度固定的情况下，flex:1则main拥有了除去底部footer高度之外的所有高度。
4.min-content：采用内部元素最小宽度值最大的那个元素的宽度作为最终容器的宽度
5.用box-shadow实现多重边框
```
/*重点在于box-shadow可以设置多个值*/
div {
	width: 100px;
	height: 60px;
	margin: 25px;
	background: yellowgreen;
	box-shadow: 0 0 0 10px #655,
            0 0 0 15px deeppink,
            0 2px 5px 15px rgba(0,0,0,.6);
}
```
