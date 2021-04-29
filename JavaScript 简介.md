# lesson-1 JavaScript 简介

计算机语言

- 面向过程开发
- 面向对象开发
- 基于对象开发

js在网站中的应用

- 网页中的特效

  焦点图
  二级菜单

  放大镜等

- 表单验证

- ajax

- h5其他内容





课程三步走：

1. js基础

2. js高级应用

3. es6

js概念和特点



JavaScript 是一种**基于对象**（object）和**事件驱动**（Event Driven）并有安全性能的脚本语言。

>什么是事件？
>
>还有哪些语言由事件驱动？
>
>事件分为鼠标事件、键盘事件等、

JavaScript与Java的区别



javascript与JScript 和ecmascript的联系

JavaScript的嵌入方式

- 内嵌式
- 外链式

## 1.内嵌脚本

内嵌脚本就是直接在HTML代码中引用JavaScript代码
**代码实现：**

```js
 <input type="button" value="点我" onclick="alert('helloworld')">
```

> onclick="alert('helloworld')"就是内嵌脚本代码

## 2.内部脚本

内部脚本就是直接在HTML文件中创建JavaScript代码并引用
**代码实现:**

```js
<script type="text/javascript">
	alert("helloworld2 ");
</script>
```

## 3.外部脚本:

外部脚本就是单独创建JavaScript文件，以.js为文件后缀，在HTML文件中调用文件
**代码实现：**
*HTML内引用:*

```js
<script type="text/javascript" src="js/helloworld.js"></script>
```

*helloworld.js文件内容:*

```js
alert("helloworld3");
```

 ![mark](http://qiniu.wind-zhou.com/blog/201203/8maB8A91Ik.png?imageslim)

