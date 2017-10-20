# html（超文本编辑语言）

## 基本结构

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title>Hello world</title>
  </head>
  <body>
  </body>
</html>
```



## 常见标签

- 标题`<h1></h1>`
- `<a href="http://baidu.com" target="_blank"></a>1`
- `<p></p>`
- `<img src="" width=""  height="">`
- `<table><tr><th></th></tr></table>`
- 列表`<ol></ol>  <ul><ul>`
- `<div></div>  <span> </span>`
- 表单`<form action="" method="post">`
- 下拉列表`<select></select>`
- 属性：id（独一无二的） , class（表示一类） 

# css(层叠样式表)

## 基本结构

选择器+样式（key:value）

## 引入css的三种方法

- 引入外部css样式
- 在html中使用css样式
- 在元素中使用内联样式（style）

## 常用选择器

- 元素名
- id
- class
- 后代选择器
- 子元素选择器
- 相邻兄弟选择器，普通相邻兄弟选择器
- 伪类 hover

## 常见样式

- 背景：background-color,background-image,background
- 大小：width，height
- 大小单位：px，% , em
- 文本：color,  text-align, text-decoration, text-indent, line-height, font-size, font-family
- 留白：margin,padding
- 边框：border, border-radius, box-shadow
- 显示：display
- 定位：static，fixed，relative，absolute，float

## CSS3

- animation（动画）：@keyframes myanimation{ 0% }

# js

js决定了如何动态的改变HTML元素

## 使用js

- 在HTML中使用js
- 引入外部的js文件

## 内容

- document.write()
- getElementById()
- onclick="myfunction"
- console.log()
- 变量var：数值，字符，数组，字典/对象
- 运算符，条件，循环
- 注释
- 函数 function myfunction { 执行的代码 }
- 作用域
- 事件

# JQuery