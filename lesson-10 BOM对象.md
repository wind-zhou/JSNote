# lesson-10 BOM对象

[Javascript之BOM与DOM讲解](https://blog.csdn.net/qq877507054/article/details/51395830?utm_medium=distribute.pc_relevant.none-task-blog-OPENSEARCH-3.control&depth_1-utm_source=distribute.pc_relevant.none-task-blog-OPENSEARCH-3.control)

# 一、概述

##**Javascript组成**

JavaScript的实现包括以下3个部分：

| ECMAScript(核心)      | 描述了JS的语法和基本对象。 |
| --------------------- | -------------------------- |
| 文档对象模型 （DOM）  | 处理网页内容的方法和接口   |
| 浏览器对象模型（BOM） | 与浏览器交互的方法和接口   |

 >1. 

## BOM与DOM简介

**定义：**

- DOM ----Document Object Model。是为了**操作文档出现的 API**。
- BOM ----Browser Object Model。是为了**操作浏览器出现的 API**。

**关系：**

1. DOM 是 W3C 的标准； [所有浏览器公共遵守的标准]
2. BOM 是 各个浏览器厂商根据 DOM在各自浏览器上的实现;[表现为不同浏览器定义有差别,实现方式不同]
3. window 是 BOM 对象，而非 js 对象**；javacsript是通过访问BOM（Browser Object Model）对象来访问、控制、修改客户端(浏览器)**。

![mark](http://qiniu.wind-zhou.com/blog/201216/eDGFDHDh2e.png?imageslim)



# 二、window对象

`BOM`的核心是`window`，而`window`对象又具有双重角色，它既是通过js访问浏览器窗口的一个接口，又是一个`Global`（全局）对象。这意味着在网页中定义的任何对象，变量和函数，都以window作为其`global`对象。

### 属性

**基本属性**

| 属性                                       | 描述                                                         |
| ------------------------------------------ | ------------------------------------------------------------ |
| **closed**                                 | **返回窗口是否已被关闭。**                                   |
| defaultStatus                              | 设置或返回窗口状态栏中的默认文本。                           |
| **innerheight**                            | **返回窗口的文档显示区的高度。**  （**浏览器视口，不包括工具栏和滚动条**） |
| **innerwidth**                             | **返回窗口的文档显示区的宽度。**（**浏览器视口，不包括工具栏和滚动条**） |
| **length**                                 | **设置或返回窗口中的框架数量。**                             |
| name                                       | 设置或返回窗口的名称。                                       |
| **opener**                                 | **返回对创建此窗口的窗口的引用。**                           |
| outerheight                                | 返回窗口的外部高度。                                         |
| outerwidth                                 | 返回窗口的外部宽度。                                         |
| pageXOffset                                | 设置或返回当前页面相对于窗口显示区左上角的 X 位置。          |
| pageYOffset                                | 设置或返回当前页面相对于窗口显示区左上角的 Y 位置。          |
| parent                                     | 返回父窗口。                                                 |
| **self**                                   | **返回对当前窗口的引用。等价于 Window 属性。**               |
| window                                     | window 属性等价于 self 属性，它包含了对窗口自身的引用。      |
| status                                     | 设置窗口状态栏的文本。                                       |
| top                                        | 返回最顶层的先辈窗口。                                       |
| screenLeft  screenTop<br />screenX screenY | 只读整数。声明了窗口的左上角在屏幕上的的 x 坐标和 y 坐标。IE、Safari 和 Opera 支持 screenLeft 和 screenTop，而 Firefox 和 Safari 支持 screenX 和 screenY。 |

**注释：**黄色的几个是最常用的。

**注释：JavaScript中的任何一个全局函数或变量都是window的属性。**

**练习：**

```js
<script type="text/javascript">
    var name="wind-zhou";
    document.write(window.name);
</script>
//输出：win-zhou
```

### window方法1-**对话框函数**

**window 对象定义了 3 个人机交互的方法，主要方便对 JavaScript 代码进行调试。**

#### alert（"提示信息"）

前面的window可以省略，因为window是全局对象

带确定按钮

#### confirm("提示信息")

带确定和取消按钮。

点击确定---返回true

点击取消--返回false

**练习：**

```js
<script>
    var x = window.confirm("hello")
    console.log("接收到的信息为：" + x)
</script>
```

**输出：**

![mark](http://qiniu.wind-zhou.com/blog/201221/3Jia0bE84E.png?imageslim)

#### prompt("提示信息"，"默认值")

上面的几种提示信息，主要是做调试。

因为上面的形式弹出框有诸多弊端。  例如网页进制弹出会影响到程序。

**练习：**

```js
<script>
    var x = prompt("这是提示信息", "这是传的默认值")
    console.log("通过prompt接收到的数据为：", x)
</script>
```

**输出：**

![mark](http://qiniu.wind-zhou.com/blog/201221/BmkKG60143.gif)

**注释：**显示系统对话框的时候，JavaScript 代码会停止执行，只有当关闭对话框之后，JavaScript 代码才会恢复执行。因此，不建议在实战中使用这 3 种方法，仅作为开发人员的内测工具即可。

### window方法2 打开 关闭

#### open("url","窗口名称"，"属性=值","属性=值",...)

**常用来做网页内的对话框。**

>**该方法返回值为新创建的 window 对象**

**窗口特征（Window Features）**

| channelmode=yes\|no\|1\|0 | 是否使用剧院模式显示窗口。默认为 no。                        |
| ------------------------- | ------------------------------------------------------------ |
| directories=yes\|no\|1\|0 | 是否添加目录按钮。默认为 yes。                               |
| fullscreen=yes\|no\|1\|0  | 是否使用全屏模式显示浏览器。默认是 no。处于全屏模式的窗口必须同时处于剧院模式。 |
| **height=pixels**         | 窗口文档显示区的高度。以像素计。                             |
| **left=pixels**           | 窗口的 x 坐标。以像素计。                                    |
| location=yes\|no\|1\|0    | 是否显示地址字段。默认是 yes。                               |
| menubar=yes\|no\|1\|0     | 是否显示菜单栏。默认是 yes。                                 |
| resizable=yes\|no\|1\|0   | 窗口是否可调节尺寸。默认是 yes。                             |
| status=yes\|no\|1\|0      | 是否添加状态栏。默认是 yes。                                 |
| titlebar=yes\|no\|1\|0    | 是否显示标题栏。默认是 yes。                                 |
| **width=pixels**          | 窗口的文档显示区的宽度。以像素计。                           |
| **top=pixels**            | 窗口的 y 坐标。                                              |
| toolbar=yes\|no\|1\|0     | 是否显示浏览器的工具栏。默认是 yes。                         |
| scrollbars=yes\|no\|1\|0  | 是否显示滚动条。默认是 yes。                                 |

**练习：**

```js
<body>
    <button onclick="chat()"> 点击进入聊天</button>
</body>

<script>
    function chat() {
        window.open("https://www.baidu.com", "朗科", "width=200,height=300,top=300,left=450")
    }
</script>
```



![mark](http://qiniu.wind-zhou.com/blog/201221/k3HHebH5F9.gif)



新创建的 **window 对象拥有一个 opener 属性**，**引用打开它的原始对象(这个域名可以实现不同窗口之间的通信)**。opener 只在弹出窗口的最外层 window 对象（top）中定义，而且指向调用 window.open() 方法的窗口或框架。

![mark](http://qiniu.wind-zhou.com/blog/201221/h1ikkkKFLf.png?imageslim)

##### 示例1

**下面示例演示了打开的窗口与原窗口之间的关系。**

```js
win = window.open();  //打开新的空白窗口
win.document.write ("<h1>这是新打开的窗口</h1>");  //在新窗口中输出提示信息
win.focus ();  //让原窗口获取焦点
win.opener.document.write ("<h1>这是原来窗口</h1>");  //在原窗口中输出提示信息
console.log(win.opener == window);  //检测window.opener属性值
```

使用 window 的 close() 方法可以关闭一个窗口。例如，关闭一个新创建的 win 窗口可以使用下面的方法实现。

```js
win.close();
```

如果在打开窗口内部关闭自身窗口，则应该使用下面的方法。

```js
window.close();
```

使用 window.closed 属性可以检测当前窗口是否关闭，如果关闭则返回 true，否则返回 false。

##### 示例2

下面示例演示如何自动弹出一个窗口，然后设置半秒钟之后自动关闭该窗口，同时允许用户单击页面超链接，更换弹出窗口内显示的网页 URL。

```js
    var url = "http://www.baidu.com"; //要打开的网页地址
    var features = "height=500, width=800, top=100, left=100, toolbar=no, menubar=no,scrollbars = no, resizable = no, location = no, status = no "; //设置新窗口的特性
    //动态生成一个超链接
    document.write('<a href="http://www.baidu.com" target="newW">切换到C语言中文网首页</a>');
    var me = window.open(url, "newW", features); //打开新窗口,返回新窗口的window对象
    setTimeout(function() { //定时器
        if (me.closed) {
            console.log("创建的窗口已经关闭。");
        } else {
            me.close();
        }
    }, 5000); //半秒钟之后关闭该窗口
```

#### close()

**关闭当前页面**

##### 示例

打开一个界面，1s后自动关闭。

```js
<script>   
function close11() {
        console.log("执行到了这里");
        window.close();
    }
    setTimeout(close11, 1000);
</script>
```

#### print()

**打印当前页面**

##### 示例

1s后打印当前页面

```js
<script>
    function print_test() {
        window.print();
    }
    setTimeout(print_test, 1000)
</script>
```

![mark](http://qiniu.wind-zhou.com/blog/201221/HE32b4diHm.png?imageslim)

### window方法3 控制窗口的位置和大小



window 对象定义了 3 组方法分别用来调整**窗口位置**、**大小**和**滚动条的偏移位置**：moveTo() 和 moveBy()、resizeTo() 和 resizeBy()、scrollTo() 和 scrollBy()。



这些方法都包含两个参数，分别表示 x 轴偏移值和 y 轴偏移值。**包含 To 字符串的方法都是绝对的**，也就是 x 和 y 是绝对位置、大小或滚动偏移；**包含 By 字符串的方法都是相对的**，也就是它们在窗口的当前位置、大小或滚动偏移上增加所指定的参数 x 和 y 的值。

下面重点讲两种。

####  moveTo(x,y)

```js
<!DOCTYPE html>
<html>

<head>
    <meta charset="utf-8">
    <title>菜鸟教程(runoob.com)</title>
    <script>
        function openWin() {
            myWindow = window.open('', '', 'width=200,height=100');
            myWindow.document.write("<p>这是我的窗口</p>");
        }

        function moveWin() {
            x = Math.ceil(Math.random() * 1024);
            y = Math.ceil(Math.random() * 760);
            console.log(x, y)
            myWindow.moveTo(x, y);
            myWindow.focus();
        }
    </script>
</head>

<body>

    <input type="button" value="打开我的窗口" onclick="openWin()" />
    <br><br>
    <input type="button" value="移动我的窗口" onclick="moveWin()" />

</body>

</html>
```

#### moveBy(x,y)

操作同上。

#### resizeTo(x,y)

把窗口大小调整到指定宽高**(仅IE支持)**

```js
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<title>菜鸟教程(runoob.com)</title>
<script>
    
var w;
function openwindow(){
	w=window.open('','', 'width=100,height=100');
	w.focus();
}
function myFunction(){
	w.resizeTo(500,500);
	w.focus();
}
</script>
</head>
<body>

<button onclick="openwindow()">创建窗口</button>
<button onclick="myFunction()">调整窗口</button>

</body>
</html>
```

#### resizeBy(x,y)

操作同上。

**仅IE支持**  

#### scrollBy(x,y)  



```js
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<title>菜鸟教程(runoob.com)</title>
	<style>
		input{
			position:fixed;
		}	
	</style>
<script>
function scrollWindow(){
	window.scrollBy(100,500);
}
</script>
</head>
<body>

<input  type="button" onclick="scrollWindow()" value="滚动条" />
<p>滚动 滚动 滚动 滚动 滚动 滚动 滚动 滚动</p>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<p>滚动 滚动 滚动 滚动 滚动 滚动 滚动 滚动</p>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<p>滚动 滚动 滚动 滚动 滚动 滚动 滚动 滚动</p>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<p>滚动 滚动 滚动 滚动 滚动 滚动 滚动 滚动</p>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<p>滚动 滚动 滚动 滚动 滚动 滚动 滚动 滚动</p>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<p>滚动 滚动 滚动 滚动 滚动 滚动 滚动 滚动</p>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<p>滚动 滚动 滚动 滚动 滚动 滚动 滚动 滚动</p>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<p>滚动 滚动 滚动 滚动 滚动 滚动 滚动 滚动</p>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>

</body>
</html>
```

渐变

#### scrollTo(x,y)

**用法同上。**

### window 方法3  定时函数

window 对象包含 4 个定时器专用方法，说明如下表所示，使用它们可以实现代码定时执行，或者延迟执行，**使用定时器可以设计演示动画。**

|      方法       |                       说明                       |
| :-------------: | :----------------------------------------------: |
|  setInterval()  | 按照执行的周期（单位为毫秒）调用函数或计算表达式 |
|  setTimeout()   |       在指定的毫秒数后调用函数或计算表达式       |
| clearInterval() |      取消由 setInterval() 方法生成的定时器       |
| clearTimeout()  |       取消由 setTimeout() 方法生成的定时器       |

#### setTimeout()

**定时，在指定毫秒数后调用函数** 

**做动画队列.**

setTimeout() 方法的第一个参数虽然是字符串，但是也可以是一个函数。

**一般建议把函数作为参数传递给 setTimeout() 方法，等待延迟调用**。

#### clearTimeout()

取消由setTimeout设置的定时

##### 示例

一个div 3s后宽度变为300px。如果3s内点击停止按钮则取消变换。

```js
<style>
        #one {
            width: 10px;
            height: 200px;
            background: pink;
            transition: width 1s;
        }
    </style>
---------------------------------------------------------------------------------------------------------------
<body>
    <div id="one">

    </div>

    <button onclick="stopChange()">暂停变换</button>
</body>
<script>
    function changeWidth() {
        document.getElementById("one").style.width = "300px"
    }

    i = setTimeout(changeWidth, 3000); //每个setTimeout会返回一个全局的标识

    function stopChange() {

        clearTimeout(i)
    }
</script>
```

#### setInterval()

 **语法：**

```js
setInterval(code, milliseconds);
setInterval(function, milliseconds, param1, param2, ...)
```

计时器，按指定周期调用函数和表达式（以毫秒为单位）

页面里所有的动画效果基本都是setinterval。



#### clearInterval

**取消计时**

##### 示例1

**用setInterval实现一个秒表**

```js
<body>
    <h1 id="time"></h1>
</body>

<script>
    function time() {
        var date = new Date();
        document.getElementById("time").innerHTML = date.toLocaleTimeString();
    }
    setInterval(time, 1000);
</script>
```

![mark](http://qiniu.wind-zhou.com/blog/201221/Ia3cFKEGhE.gif)

##### 示例2

实现一个秒表计时器

```js
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
</head>

<body>
    <div id="con">00:00:00</div>
    <button onclick="start()"> 开始</button>
    <button onclick="stop()"> 结束</button>
</body>

<script>
    var h = 0;
    var m = 0;
    var s = 0;

    var ss;
    var mm;
    var hh;
    var state = true;

    function start() {

        if (state) {
            i = setInterval(function() {
                s++;
                if (s >= 60) {
                    m++;
                    s = 0;
                }
                if (m >= 60) {
                    h++;
                    m = 0;
                }
                s < 10 ? ss = "0" + s : ss = s;
                m < 10 ? mm = "0" + m : mm = m;
                h < 10 ? hh = "0" + h : hh = h;

                document.getElementById("con").innerHTML = hh + ":" + mm + ":" + ss;
                console.log("本次开始的i的值" + i)

            }, 1000);
        }

        state = false;
    }

    function stop() {
        clearInterval(i)
            // 本次停止的i的值
        console.log("本次停止的i的值" + i)
        state = true;
    }
</script>

</html>
```

![mark](http://qiniu.wind-zhou.com/blog/201221/Bl10bf88c0.gif)

##### 示例3

用setInterval实现一个动画效果，点击按钮，div变大，当宽度达到100px后，停	止

```js
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <style>
        #one {
            height: 200px;
            background: pink;
        }
    </style>
</head>

<body>
    <div id="one" style="width:10px;">

    </div>

    <button onclick="start()">
        点击放大
    </button>
</body>

<script>
    function start() {
        i = setInterval(function() {
            if (parseInt(document.getElementById("one").style.width) >= 100) {
                clearInterval(i);
            } else {
                document.getElementById("one").style.width = parseInt(document.getElementById("one").style.width) + 10 + "px";
            }
        }, 50)
    }
</script>

</html>
```

![mark](http://qiniu.wind-zhou.com/blog/201221/L460dd5lc1.gif)

注; document.getElementById("time").style获取的样式为**行内样式的值。**

**原生js无法直接操控css。**

# Navigatior

##**对象属性：**

浏览器对象，包括一些浏览器型号，信息等。

### appCodeName

**返回浏览器的代码名**，所有浏览器输出都一样。

### appName

**返回浏览器名称**，所有的浏览器返回同一个名字

### **appVersion ** (最常用)

**返回浏览器版本(包括 体系版本)**

##### 示例1

三种信息比较

```js
<script>
    var appcodename = navigator.appCodeName;
    console.log("appcodename:\t\t" + appcodename);

    var appName = navigator.appName;
    console.log("appName:\t\t" + appName);

    var appversion = navigator.appVersion;
    console.log("appversion:\t\t" + appversion);
</script>
```

![mark](http://qiniu.wind-zhou.com/blog/201221/4AhmbCifCk.png?imageslim)

##### 示例2

**练习：判断手机操作系统**                 

```js
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
</head>

<body>

</body>

<script>
    function test() {
        var equip_type = "";
        var info = navigator.appVersion.toLowerCase();
        console.log(info);
        var window = info.indexOf("window");

        var android = info.indexOf("android");
        var iphone = info.indexOf("iphone");
        var ipad = info.indexOf("ipad");
        if (window != -1) {
            equip_type = "window"
        }
        if (android != -1) {
            equip_type = "android";

        }

        if (ipad != -1 || iphone != -1) {
            equip_type = "ios";
        }
        return equip_type;
    }

    var result1 = test();
    console.log(result1);
    document.write(result1);
</script>

</html>
```

**注：indexOf方法不只能检测字符还能检测字符串。**

### cookieEnabled

返回浏览器中是否启动了cookie

# screen对象

**screen包含有关客户端显示屏信息**

## 属性

### avaiHeight

返回显示屏幕的高度

### avaiWidth

返回显示屏幕的高度

**注：**不包含底部任务栏

### height

### width

##### 示例

```js
<script>
    var iw = window.innerWidth;  //视口的宽度
    var ih = window.innerHeight;

    var aw = screen.availWidth;//显示屏幕的高度，不包含底部任务栏
    var ah = screen.availHeight;

    var w = screen.width;//屏幕的真实高度  css像素
    var h = screen.height;

    document.write("<div>" + iw + "," + ih + "</div>")
    document.write("<div>" + aw + "," + ah + "</div>")
    document.write("<div>" + w + "," + h + "</div>")

</script>
```

![mark](http://qiniu.wind-zhou.com/blog/201221/b93BhDH9Fj.gif)

**注：此处测试avaiHeight和width相等，因为我的电脑设置没有底部任务栏。**



注：关于screen.width是理想视口的宽度，这里我的电脑分辨率为1920px，但此时我的电脑是150%缩放，因此屏幕的理想视口宽度只有1280个css像素！

# history对象

包含用户在浏览器中访问过的url

**可以用来实现前进和后退功能**

## 属性

### length

**返回浏览器历史列表中的url数量**

## 方法

### back

加载history里表中前一个url

#### forward

加载history列表中下一个url

### go

加载history列表中的某个页面

里面可以设置参数实现跳转的步骤

例：go(-1) 代表向前跳一步

# Location对象

## 属性

指的是当前对象包含的有关url信息（**JavaScript管理地址栏的内置对象**）

### hash（哈希） （重点记）

设置或返回从#开始的url（锚）

注：后端服务器并不能识别锚，但浏览器可以识别，因此**可以通过hash来实现不同网页的传值**。

### host

**获取和返回主机名和和当前url端口号**

### hostname

只返回主机名

###  href  (重点记)

**设置或返回完整**的url地址---**通常用来动态跳转**

实现页面的跳转：

- **超链接**
- **open方法**
- **location.href**

### pathname

设置或返回url的路径部分--URI（统一资源标识符）

### port

设置或返回当前url端口号

### protocol

设置或获取当前url协议

### search  （重点记）

设置或返回从“？”开始的url

**是模拟form表单传值的方式。**



练习：

```js
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
</head>

<body>

</body>


<script>
    var PORT = location.port;
    var PATHNAME = location.pathname;
    var PROTOCAL = location.protocol;
    var HOST = location.host;
    var HREF = location.href;

    console.log("host:" + HOST);
    console.log("pathname:" + PATHNAME);
    console.log("port:" + PORT);
    console.log("protocal:" + PROTOCAL);
    console.log("href:" + HREF);
</script>

</html>
```

输出：

![mark](http://qiniu.wind-zhou.com/blog/210102/aEJgda3bH8.png?imageslim)



![mark](http://qiniu.wind-zhou.com/blog/201221/IBFhH62hhD.png?imageslim)



























































