# lesson-12 事件

## 事件驱动

1. 首先，在这个对象上**绑定**这个事件
2. 其次、又在这个对象上，发生了这个事件
3. 最后、系统（js解释器） 自动调用处理函数进行响应

事件的绑定方式（主要有三种）：

（1）行内绑定（不推荐）

```js
<div onclick="test()"></div>
```

是以属性的方式绑定。

缺点：无法实现标记和动作的分离。

（2）对象名.事件名=function(){语句}   

**最常用：**

（3）事件监听

对象名.addEventListener("事件名"，函数名，捕获过程true/冒泡过程false)

注：事件名不带on

兼容性问题：IE6/7/8的兼容性写法：对象名.attachEvent("on事件名"，函数)



## 事件类型

###（1）onload  文档.	加载完成时触发(加载事件)

**绑定到window对象上** 。网页渲染完毕时。

一般用来做一些文档加载完成后才能做的事：例如

**注：window.onload在一个文档中只能使用一次。**

### （2）unonload 写在文件事件（网页关闭或刷新，或打开超链接时的覆盖）

**用法：例如关闭页面时提示是否关闭**。  （用得不多）

### （3）onresize  窗口大小改变时触发、

### （4）onscroll  滚动事件

###（5）鼠标事件

- onclick  点击事件
- ondblclick 双击事件
- onmousedown  鼠标键按下

  **注：**实验证明，鼠标的左中右键都会触发，而onclick只会由左键触发。
- onmouseup 鼠标左键抬起

  **注：**实验证明，此事件只能由由左键抬起触发。
- onmouseover  获取鼠标（）  onmouseseenter  

  **注：此项最为常用，常用于二级菜单的显示。**
- onmouseout     鼠标划出时（）    onmouseleave
- onmousemove  
  鼠标移动  例如做跟随鼠标移动的放大镜

### （6）键盘事件

​	**常用于限制输入的字符个数**

- onkeydown   键盘按下  
- onkeyup   键盘抬起
- onkeypress  按键盘

###（7）表单相关事件

- **改变事件**    onchange 和oninput

  onchange：触发时机：1、文本框内容改变2、失去焦点
  oninput：只要内容改变就触发，不需要失去焦点

-  **获得焦点**onfocus；**失去焦点**onblur

  h5出现后，**placeholder已经可以代替了**
  
- **重置事件**  onreset ；**提交事件**  onsubmit  （表单）

  **注：这两个事件绑定在form标记上**

  onreset常用于重置前的提示信息

## 综合练习

### 示例1 表格颜色动起来

生成固定行列的单元格，并随机填充颜色，点击某一个单元格时，则所有的单元格变成当前点击的单元格颜色

```js
<!DOCTYPE html>
<html>

<head>
    <meta charset="utf-8">
    <title></title>

    <style>
        table {
            border: 1px solid #000;
            border-collapse: collapse;
        }
        
        td {
            width: 40px;
            height: 40px;
            border: #000 1px solid;
        }
    </style>
</head>

<body>
    <table id="one"></table>

    <button onclick="createTab()">点击生成表格</button>
    <button onclick="start()">点击使颜色动起来</button>

</body>

<script>
    var flag = true;

    var isRestart = true;

    function createTab() {
        if (flag) {
            flag = false;
            var rows = 10;
            var cols = 10;
            var tableNode = document.getElementById("one");
            //初始化颜色数组


            for (var i = 0; i < rows; i++) {
                var trNode = document.createElement("tr");


                for (var j = 0; j < cols; j++) {
                    var tdNode = document.createElement("td");
                    //给每个td绑定一个事件

                    tdNode.onclick = function() {
                        isRestart = true;
                        clearInterval(f);
                        var tdColor = this.style.backgroundColor;
                        var tdList = document.getElementsByTagName("td");
                        for (var m = 0; m < tdList.length; m++) {
                            tdList[m].style.background = tdColor;
                        }
                        console.log(tdColor);
                    }
                    trNode.appendChild(tdNode);
                }
                tableNode.appendChild(trNode);
            }
        }
        changeColor();

    }

    //改变单元格颜色函数
    function changeColor() {
        var colArray = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, "a", "b", "c", "d", "e", "f"]
            //1、拿到所有的单元格
        var tdList = document.getElementsByTagName("td");
        //2、遍历 填充颜色

        for (var i = 0; i < tdList.length; i++) {

            // 填充颜色
            var color = "#";
            for (var k = 0; k < 6; k++) {
                var ranIndex = Math.floor(Math.random() * 16); //生成随机索引值
                color += colArray[ranIndex];
            }
            tdList[i].style.background = color; //填充颜色到单元格
        }

    }

    function start() {
	//进行状态控制，防止重复触发
        if (isRestart) {
            f = setInterval(changeColor, 50);
            isRestart = false;
        }
    }

</script>

</html;
```

效果：

![mark](http://qiniu.wind-zhou.com/blog/201226/13c7Acj8gL.gif)



### 示例2  

**下面几个一般都绑在window上。**



##### onload

```js
<head>
    <script>
        window.onload = function() {
            document.getElementById("one").innerHTML = "hello world";
        }
    </script>
</head>

<body>
    <div id="one"></div>
</body>
```

结论：onload事件类似于go中的延迟执行，在加载完html后再调用js程序。

例如上面的例子，因为js代码写在了html代码前面，如果不在onload事件中执行，则会报错：

`Uncaught TypeError: Cannot set property 'innerHTML' of null   at 加载事件.html:10`,此时找不到id="one"的div。

##### onresize

(1)  **改变窗口大小时，实时显示屏幕视口的宽度**

```js
<!DOCTYPE html>
<html>

<head>
    <meta charset="utf-8">
    <title></title>
</head>

<body>
    <h2>尝试着改变窗口</h2>
    <i id="demo"></i>
</body>

<script>
    function x() {
        var w = window.innerWidth;
        var h = window.innerHeight;
        var txt = "窗口大小: 宽度=" + w + ", 高度=" + h;
        document.getElementById("demo").innerHTML = txt;
    }
    window.onresize = x;
</script>
</html>
```

>使用document.write输出有问题

(2) 利用onresize写一个媒介查询

```js
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8">
    <title></title>
</head>

<body>
    <h2>此时的font-size值为：</h2>
    <i id="demo"></i>
</body>

<script>
    function mediaQuery() {
        var width = window.innerWidth;
        var fontSize = 100 * width / 640;
        document.getElementById("demo").innerHTML = fontSize;
    }
    window.onresize = mediaQuery;
    mediaQuery(); //用于窗口尚未改变时的输出。
</script>

</html>
```

**注**：以上实验是在窗口以``innerWidth=640，font-size=100px；``为参考。

##### onscroll

使用这个事件，做导航条功能

（1）页面向下滑动，导航条跟着上走

（2）当导航条触碰到顶时，便固定在顶部

（3）当页面网上滑动，导航条到之前触发固定的临界值时，便解除固定，根素网页移动

（4）当导航条发生移动后（scrollTop>200px），如果不在滑动，导航条会在5ms后消失，当再次滑动时，导航条出现



```js
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <style>
        * {
            padding: 0;
            margin: 0;
            box-sizing: border-box;
        }
        
        #top {
            width: 700px;
            height: 200px;
            background: pink;
            margin: 0 auto;
        }
        
        .nav {
            list-style-type: none;
            width: 700px;
            height: 30px;
            margin: 0 auto;
            background-color: blueviolet;
            opacity: 1;
            transition: all 0;
        }
        
        li {
            float: left;
            width: 100px;
            height: 30px;
            text-align: center;
            line-height: 30px;
            border-right: 1px solid #000;
        }
        
        .footer {
            width: 700px;
            background: pink;
            height: 2000px;
            margin: 0 auto;
        }
        
        .fix {
            position: fixed;
            top: 0;
            left: 50%;
            transform: translateX(-50%)
        }
         
        .trans {
            /* 设置透明属性 */
            opacity: 0;
        }
    </style>
</head>

<body>
    <div id="top"></div>
    <ul id="nav" class="nav">
        <li>首页</li>
        <li>首页</li>
        <li>首页</li>
        <li>首页</li>
        <li>首页</li>
        <li>首页</li>
        <li>首页</li>
    </ul>

    <div class="footer">
        fwioeuf9weuf9-vu-09erj[pk块级【开票【哦VB诶看人品【概况【不骗人就不怕【我就让他回家不打牌【价目表vpembjrb0[p ]] fwioeuf9weuf9-vu-09erj[pk块级【开票【哦VB诶看人品【概况【不骗人就不怕【我就让他回家不打牌【价目表vpembjrb0[p ]] fwioeuf9weuf9-vu-09erj[pk块级【开票【哦VB诶看人品【概况【不骗人就不怕【我就让他回家不打牌【价目表vpembjrb0[p ]] fwioeuf9weuf9-vu-09erj[pk块级【开票【哦VB诶看人品【概况【不骗人就不怕【我就让他回家不打牌【价目表vpembjrb0[p
        ]] fwioeuf9weuf9-vu-09erj[pk块级【开票【哦VB诶看人品【概况【不骗人就不怕【我就让他回家不打牌【价目表vpembjrb0[p ]] fwioeuf9weuf9-vu-09erj[pk块级【开票【哦VB诶看人品【概况【不骗人就不怕【我就让他回家不打牌【价目表vpembjrb0[p ]] fwioeuf9weuf9-vu-09erj[pk块级【开票【哦VB诶看人品【概况【不骗人就不怕【我就让他回家不打牌【价目表vpembjrb0[p ]] fwioeuf9weuf9-vu-09erj[pk块级【开票【哦VB诶看人品【概况【不骗人就不怕【我就让他回家不打牌【价目表vpembjrb0[p
        ]] fwioeuf9weuf9-vu-09erj[pk块级【开票【哦VB诶看人品【概况【不骗人就不怕【我就让他回家不打牌【价目表vpembjrb0[p ]] fwioeuf9weuf9-vu-09erj[pk块级【开票【哦VB诶看人品【概况【不骗人就不怕【我就让他回家不打牌【价目表vpembjrb0[p ]] fwioeuf9weuf9-vu-09erj[pk块级【开票【哦VB诶看人品【概况【不骗人就不怕【我就让他回家不打牌【价目表vpembjrb0[p ]] fwioeuf9weuf9-vu-09erj[pk块级【开票【哦VB诶看人品【概况【不骗人就不怕【我就让他回家不打牌【价目表vpembjrb0[p
        ]] fwioeuf9weuf9-vu-09erj[pk块级【开票【哦VB诶看人品【概况【不骗人就不怕【我就让他回家不打牌【价目表vpembjrb0[p ]]
    </div>

</body>

<script>
    function scroll() {

        var topScroll = document.documentElement.scrollTop;
        if (topScroll > 200) {
            //当不在滚动时，5s后进入透明（通过给ul叠加class="nav trans"实现）
            clearClass();
            document.getElementById("nav").className = "nav fix";
            //给导航条设置滑动显示功能，不滑动式便渐渐隐形
        } else {
            document.getElementById("nav").className = "nav";
        }
    }

    window.onscroll = scroll;
    //定时5s实现隐形
    function clearClass() {
        setTimeout(function() {
            document.getElementById("nav").className = "nav trans";
        }, 5000)
    }
</script>
</html>
```

![mark](http://qiniu.wind-zhou.com/blog/201228/hhGG4d9lde.gif)

上面的程序的程序实现：

（1）滑动超过一定距离导航条固定好说

（2）想要实现的效果固定后不滑动时隐藏，因此不滑动时要是ul的``opaticy=0`,这里通过定是函数setTimeout实现，，到时间后给ul叠加一个类实现隐形，在滚动触发的出现，再次通过叠加一个class实现，这个class作用`opacity=1`.

这个程序还有bug：

（1）定时隐形功能有多次触发的时间混乱问题

（2）当导航不固定后。导航条还是隐形，需要在此触发一下才可以出现。



还要注意在添加属性是的css优先级问题，id>class，因为我这里ul的css是直接用class定义的，因此没有出现问题，但是如果ul的属性使用#nav来写，name后面叠加的隐形的类（里面是`opacity=0`）不会生效。



#### 鼠标事件

##### onmousedown

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
            width: 200px;
            height: 200px;
            border: 1px solid #000;
        }
    </style>
</head>

<body>
    <div id="one"> </div>
</body>

<script>
    document.getElementById("one").onmousedown = function() {
        alert("你是用鼠标左键点击了一下我.")
    }
</script>

</html>
```

**注：**实验证明，鼠标的左中右键都会触发，而onclick只会由左键触发。onmouseop也只有左键触发。



#####  onmouseover

示例：二级菜单的显示和隐藏

```js
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>

    <style>
        * {
            padding: 0;
            margin: 0;
            box-sizing: border-box;
        }
        
        ul {
            overflow: hidden;
            list-style-type: none;
        }
        
        #father {
            width: 400px;
            margin: 0 auto;
            margin-top: 50px;
        }
        
        #father>li {
            width: 100px;
            border-right: 1px solid #000;
            float: left;
        }
        
        #father>li>ul {
            display: none;
        }
    </style>
</head>

<body>
    <ul id="father">
        <li>手机
            <ul>
                <li>huawei</li>
                <li>apple</li>
                <li>oppo</li>
                <li>vivo</li>
            </ul>

        </li>
        <li>手机
            <ul>
                <li>huawei</li>
                <li>apple</li>
                <li>oppo</li>
                <li>vivo</li>
            </ul>

        </li>
        <li>手机
            <ul>
                <li>huawei</li>
                <li>apple</li>
                <li>oppo</li>
                <li>vivo</li>

            </ul>

        </li>
        <li>手机
            <ul>
                <li>huawei</li>
                <li>apple</li>
                <li>oppo</li>
                <li>vivo</li>
            </ul>
        </li>
    </ul>
</body>
<script>
    var List = document.getElementById("father").children;
    for (var i = 0; i < List.length; i++) {

        List[i].onmouseover = function() {
            this.children[0].style.display = "block";
        }

        List[i].onmouseout = function() {
            this.children[0].style.display = "none";
        }
    }
</script>

</html>
```

三步走：

1. 拿到ul的所有li
2. 遍历每个li
3. 在每个li划入划出时**设置li的儿子ul放入显示隐藏**

##### onmousemove

**鼠标移动式，div里颜色改变。**

```js
<!DOCTYPE html>
<html>

<head>
    <meta charset="utf-8">
    <title></title>

    <style>
        #one {
            margin: 0 auto;
            margin-top: 200px;
            width: 300px;
            height: 300px;
            border: 1px solid #000;
        }
    </style>

</head>

<body>
    <div id="one">  </div>
</body>

<script>
    //改变颜色
    function changeColor() {
        var colArray = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, "a", "b", "c", "d", "e", "f"]
            //1、拿到div
        var divGet = document.getElementById("one");
        //2、填充颜色
        var color = "#";
        for (var k = 0; k < 6; k++) {
            var ranIndex = Math.floor(Math.random() * 16); //生成随机索引值
            color += colArray[ranIndex];
        }
        divGet.style.background = color; //填充颜色到div
    }

    document.getElementsByTagName("html")[0].onmousemove = function() {
        changeColor();
    }
</script>

</html;
```

效果：

![mark](http://qiniu.wind-zhou.com/blog/201227/a3gDmbg6iA.gif)

#### 键盘事件

##### onkeydown onkeyup  onkeypress

（1）比较三种的区别

```js
<!DOCTYPE html>
<html>

<head>
    <meta charset="utf-8">
    <title></title>


</head>

<body>

    <h1>测试下onkeyup、onkeydown和onkeypress的区别</h1>

    测试onkeyup：<input type="text" id="test1"><br><br> 测试onkeydown：
    <input type="text" id="test2"><br><br> 测试onkeypress：
    <input type="text" id="test3"><br><br> 测试onkeyup、onkeydown和onkeypress：
    <input type="text" id="test4"><br><br>


</body>

<script>
    //绑定onkeyup
    document.getElementById("test1").onkeyup = function() {
        alert("我是onkeyup");
    }


    document.getElementById("test2").onkeydown = function() {
        alert("我是onkeydown");
    }

    document.getElementById("test3").onkeypress = function() {
        alert("我是onkeypress");
    }


    document.getElementById("test4").onkeyup = function() {
        alert("我是onkeyup");
    }


    document.getElementById("test4").onkeydown = function() {
        alert("我是onkeydown");
    }

    document.getElementById("test4").onkeypress = function() {
        alert("我是onkeypress");
    }
</script>

</html>
```

结果：

**在火狐浏览器测试得出结论：**

 onkeyup是在键盘按下去并松开后执行

 onkeydown在键盘下去就会执行，不管是数字键还是字母键还是任何的功能键(所有键)
 onkeypress在键盘下去就会执行，不管是数字键还是字母键还是任何的功能键(所有键)
 onkeydown和onkeypress效果是一样的

**在谷歌浏览器测试得出结论：**
 onkeyup是在键盘按下去并松开后执行
 onkeydown在键盘下去就会执行，不管是数字键还是字母键还是任何的功能键(所有键)
 onkeypress在键盘下去就会执行，但是**按下功能键(F1到F12还有下箭头键下箭头键等这些功能键)不会执行**
 onkeydown和onkeypress效果是不一样的

>**注意：**
>
>三者在事件的响应上还有一点不同，**就是onkeydown 、onkeypress事件响应的时候输入的字符并没有被系统接受**，**而响应onkeyup的时候，输入流已经被系统接受。**
>由于onkeydown 比onkeypress先执行，再根据上面的例子可以知道，onkeydown 触发的时候输入流正要进入系统，也就是说onkeydown 事件一完，输入流就进入了系统，无法改变。所以通过onkeydown 事件可以改变用户是按了哪个键；而onkeypress事件则是在输入流进入系统后触发的，但输入流暂未被系统处理，此时已经不能改变输入流了；onkeyup则是输入流被系统处理后发生的。
>
>**测试：**
>
>```js
><body>
>    <span>测试onkeyup </span><input type="text" value="" id="con1"><br>
>
>    <span>测试onkeydpen</span> <input type="text" value="" id="con2"> <br>
>
>    <span> 测试onkeypress </span><input type="text" value="" id="con3">
>
></body>
>
><script>
>    document.getElementById("con1").onkeyup = function() {
>
>        var strLen = this.value.length; //注：这里使用value即可
>        console.log("onkeyup的输出：\t" + strLen);
>    }
>
>    document.getElementById("con2").onkeydown = function() {
>
>        var strLen = this.value.length; //注：这里使用value即可
>        console.log("onkeydown的输出：\t" + strLen);
>    }
>
>    document.getElementById("con3").onkeypress = function() {
>
>        var strLen = this.value.length; //注：这里使用value即可
>        console.log("onkeypress的输出：\t" + strLen);
>    }
></script>
>```
>
>
>
>
>
>![mark](http://qiniu.wind-zhou.com/blog/201227/dIgegl9G3E.png?imageslim)

(2)判断输入框的字符的个数

```js
<body>
    <input type="text" value="请输入姓名" id="one"> <span>*</span>
</body>

<script>
    document.getElementById("one").onkeyup = function() {
        var strLength = this.value.length;
        if (strLength > 10) {
            this.nextElementSibling.innerHTML = "太长了憨逼！";
        } else if (strLength < 3) {
            this.nextElementSibling.innerHTML = "你家的名字这么短呀！";
        } else {
            this.nextElementSibling.innerHTML = "这么长正好，臭宝。";
        }
    }
</script>
```

(3) 限制输入框输入的字数

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
    <textarea name="" id="con" cols="30" rows="10"></textarea>
    <p id="num"><span>0</span><span>/15</span></p>
</body>

<script>
    document.getElementById("con").onkeyup = function() {
        console.log(this.value);
    }

    //统计输入框的字符个数
    document.getElementById("con").onkeyup = function() {
        var str = this.value
        var strLen = str.length;

        document.getElementById("num").firstElementChild.innerHTML = strLen;

        if (strLen >= 15) {
            //大于15时，截取前15个字母
            var tmp = str.slice(0, 15);
            console.log(tmp)
                // j将截取的字符串传入输入框
            //str=value  问什么这么写不行？
            this.value = tmp;
            strLen = this.value.length;
            //重新赋值长度
            //这句话如果不写则会导致同级的值诶16，因为当点击第16次时，点击结束后
            //，触发事件前新输入的次被压入了输入流，此时计数加1，尽管后面判定把输入的第16个
            //字符截掉了，但刚才计数的值仍未16,因此需要重新赋值一下长度
            document.getElementById("num").firstElementChild.innerHTML = strLen;
        }
    }
</script>

</html>
```

####表单事件

#####onchange和oninput

**示例1：**体会onchange和oninput的异同

````js
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
</head>
·

<body>
    <span>测试 oninput</span>
    <input type="text" name="username" id="test1"><span>*</span> <br>
    <span>测试onput</span>
    <input type="text" name="username" id="test2"><span>*</span>

</body>

<script>
    document.getElementById("test1").oninput = function() {
        var len = this.value.length;
        console.log(len)
        if (len < 5) {
            this.nextSibling.innerHTML = "长度太小了弟弟！"
        } else {
            this.nextSibling.innerHTML = "";
        }
    }


    document.getElementById("test2").onchange = function() {
        var len = this.value.length;
        console.log(len)
        if (len < 5) {
            this.nextSibling.innerHTML = "长度太小了弟弟！"
        } else {
            this.nextSibling.innerHTML = "";
        }
    }
</script>

</html>
````



![mark](http://qiniu.wind-zhou.com/blog/201228/kb3D5Dmm1E.gif)

**结论**：oninput只要内容变化就会触发，而onchange需要内容改变和失去焦点两个各个条件

##### onfocus和onblur

**示例：**

使用onfocus和onblur实现placeholder的效果

```js
<!DOCTYPE html>
<html>

<head>
    <meta charset="utf-8">
    <title></title>
</head>

<body>
    <input type="text" value="请输入用户名" id="one"> <span>*</span>
</body>

<script>
    //聚焦时值为0
    document.getElementById("one").onfocus = function() {
        this.value = "";
    }
    //失去焦点时
    document.getElementById("one").onblur = function() {
        //判断input是否有用户填写的值？
        if (this.value == "") {
            this.value = "请输入用户名";
        }
    }

</script>

</html>
```



![mark](http://qiniu.wind-zhou.com/blog/201228/hc90LKlHlE.gif)



总结：当输入框有用户输入的值时， 失去焦点时里面内容保留，否则变回“请输入用户名”的提示信息。

##### onreset和onsubmit

**示例：**

**进行表单验证：**

（1）输入时统计字数，并做出反馈

（2）重置前弹出提示信息

（3）提交时如果输入的不是大写字母，则拒绝提交

（4）聚焦时提示信息消失

（5）失去焦点时，如果输入为空则恢复提示信息

```js
<!DOCTYPE html>
<html>

<head>
    <meta charset="utf-8">
    <title></title>


</head>

<body>

    <form action="abc.php" id="myform" method="GET">

        <input type="text" value="请输入用户名" id="one"> <span>*</span>

        <input type="reset" value="重置">
        <input type="submit" value="提交">

    </form>

</body>

<script>
    //绑定重置事件
    document.getElementById("myform").onreset = function() {
            //此事件在重置前触发，用于重置前的提醒
            var x = window.confirm("Are You Sure?")

            if (!x) {
                return false; //终止重置
            }
        }
        //输入时验证输入字数
    document.getElementById("one").oninput = function() {


        var strLen = this.value.length;
        if (strLen < 5) {
            this.nextElementSibling.innerHTML = "阁下输了个寂寞！";
        } else {
            this.nextElementSibling.innerHTML = "输入字数达标！";
        }
    }

    //提交前验证是否有都是大写字母
    document.getElementById("myform").onsubmit = function() {
            //判断输入是否都是小写字母？
            var str = document.getElementById("one").value
            console.log(str)
            var strUP = str.toUpperCase();
            console.log(strUP)
            if (str != strUP) {
                alert("输入有问题憨逼！")
                    //如果不全是小写字母，则停止提交
                return false;
            }
        }
        //设置聚焦时事件
    document.getElementById("one").onfocus = function() {
        if (this.value == "请输入用户名") {
            this.value = "";
        }
    }

    document.getElementById("one").onblur = function() {
        if (this.value == "") {
            this.value = "请输入用户名"
        }
    }
</script>

</html>
```



![mark](http://qiniu.wind-zhou.com/blog/210107/hCdBfKJLBd.png?imageslim)



## 事件对象

###**什么是事件对象？**

 

>浏览器读到绑定事件的代码时**自动生成**。
>
>事件对象作为参数传递给处理程序函数。
>
>事件对象创建：
>
>- 系统  自动创建
>- chrome 支持e和window.event写法
>- fireFox只支持e的标准写法不支持window.event
>- IE9/10支持e的写法，也支持window.event



- **就是当你触发了一个事件以后，对该事件的一些描述信息**

- 例如：
  - 你触发一个点击事件的时候，你点在哪个位置了，坐标是多少
  - 你触发一个键盘事件的时候，你按的是哪个按钮

- 每一个事件都会有一个对应的对象来描述这些信息，我们就把这个对象叫做 事件对象

**我们可以来输出一下event来看看里面有哪些信息。**



```js
 document.getElementById("test").onclick = function(e) {
        e = window.event || e; //兼容性写法
        console.log(e)
    }
```

输出：

![mark](http://qiniu.wind-zhou.com/blog/210304/AA4LKIfBL5.png?imageslim)

### event的兼容性写法



- 浏览器给了我们一个 黑盒子，叫做 window.event ，就是对事件信息的所有描述

- 这个玩意很好用，但是一般来说，好用的东西就会有 兼容性问题 ，在 IE低版本里面这个东西好用，但是在 高版本IE 和 Chrome 里面不好使了



- 我们就得用另一种方式来获取 事件对象，在每一个事件处理函数的行参位置，默认第一个就是 事件对象

```js
    var box = document.querySelector('.box')
    console.log(box)
    box.onclick = function fn1(e){
        //window.event.X轴坐标点信息 根据页面来显示的
        console.log(e.x)
    }
```

-  综上所述，我们以后在每一个事件里面，想获取事件对象的时候，都用兼容写法

```js
box.onclick = function (e) {
    //兼容写法
    e = e || window.event
}
```

### 几个常用的属性

![mark](http://qiniu.wind-zhou.com/blog/210304/A70Ia3CDfl.png?imageslim)

![mark](http://qiniu.wind-zhou.com/blog/210304/BJHc00c7KL.png?imageslim)



![mark](http://qiniu.wind-zhou.com/blog/210304/29Ff9kIC5g.png?imageslim)



###几组常用的坐标

####offsetX 和 offsetY

- 是相对于**你点击的元素的边框内侧**开始计算 有边框的话会出现负值

```js
  document.getElementById("test").onclick = function(e) {
        e = window.event || e; //兼容性写法
        console.log(e)
        console.log("offsetX:" + e.offsetX)
        console.log("offsetY:" + e.offsetY)
    }
```

![mark](http://qiniu.wind-zhou.com/blog/210304/lk2D8jJ8dh.png?imageslim)

#### clientX 和 clientY

- 是**相对于浏览器窗口**来计算的，从浏览器**可视区域左上角**开始（不包含菜单栏和导航栏）

```js
    document.getElementById("test").onclick = function(e) {
        e = window.event || e; //兼容性写法
        console.log(e)
       console.log("clientX:" + e.clientX)
        console.log("clientY:" + e.clientY)
    }
```



![mark](http://qiniu.wind-zhou.com/blog/210304/B1jEgClAeF.png?imageslim)

#### screenX 和 screenY

- 是**相对于整个页面**的坐标点， 从页面左上角开始,即是以页面为参考点。

```js
    var box = document.querySelector('.box')
    box.onclick = function (e) {
        //根据你浏览器的窗口来计算的，Y轴不包含导航地址栏和标签栏这些
        console.log(e.screenY)
        console.log(e.screenX)
    }
```

上图

![mark](http://qiniu.wind-zhou.com/blog/210304/3m1mgALc25.png?imageslim)

 

注：clientX,clientY，screenX，screenY的值会因滚动条的移动而改变。

#### pageX和pageY

- pageX和pageY也是获取的点前位置和可视区域的横纵距离，和clientX，clientY规则类似，但又有不同，确切地说pageX，pageY是相对于所编写页面的左侧和顶部而言。

下面举例：

滚动条没动时：

![mark](http://qiniu.wind-zhou.com/blog/210304/L2EkKAGmF7.png?imageslim)

滚动一段距离后：

![mark](http://qiniu.wind-zhou.com/blog/210304/bgI83Ch1le.png?imageslim)

 #### x和y

这两个坐标时IE的写法，完全等同于clientX和clientY。

 

### 事件监听

- addEventListener : 非 IE 7 8 下使用

- 语法： 元素.addEventListener('事件类型'， 事件处理函数， 冒泡还是捕获)



```js
    var box = document.querySelector('.box')
    box.addEventListener('click', function () {
        console.log('我是第一个事件')
    },false)
    box.addEventListener('click', function () {
        console.log('我是第二个事件')
    },false)
```



  ° 当你点击 div 的时候，两个函数都会执行，并且会按照你注册的顺序执行

  ° 先打印 我是第一个事件 再打印 我是第二个事件

  ° 注意： 事件类型的时候不要写 on，点击事件就是 click，不是 onclick

• attachEvent ：IE 7 8 下使用

• 语法： 元素.attachEvent('事件类型'， 事件处理函数)

```js
    box.attachEvent('onclick', function () {
        console.log('我是第二个事件')
    })
    box.attachEvent('onclick', function () {
        console.log('我是第二个事件')
    })
```

  ° 当你点击 div 的时候，两个函数都会执行，并且会按照你注册的倒序执行

  ° 先打印 我是第二个事件 再打印 我是第一个事件

  ° 注意： 这个需要些on方法

### 事件的传播

- **事件传播也称为事件流，指的是事件的流向**，事件的执行顺序。比如在一个大盒子里有一个小盒子，都给他们绑定点击事件。点击小盒子大盒子的事件也会被触发

- 这个就叫事件的传播

    ° 当元素触发一个事件的时候，其父元素也会触发相同的事件，父元素的父元素也会触发相同的事件

    ° 也就是说，页面上任何一个元素触发事件，都会一层一层最终导致 window 的相同事件触发，前提是各 层级元	素得有注册相同的事件，不然不会触发

- 在事件传播的过程中，有一些注意的点：

   　　 1.  只会传播同类事件
   　　 2.  只会从点击元素开始按照 html 的结构逐层向上元素的事件会被触发
　　 3. 内部元素不管有没有该事件，只要上层元素有该事件，那么上层元素的事件就会被触发

### 冒泡和捕获

- 冒泡

  　　° 就是从事件 目标 的事件处理函数开始，依次向外，直到 window 的事件处理函数触发

    　　° 也就是从下向上的执行事件处理函数

-  捕获

  　　° 就是从 window 的事件处理函数开始，依次向内，只要事件 目标 的事件处理函数执行

    　　° 也就是从上向下的执行事件处理函数

![img](https://img2020.cnblogs.com/blog/1948294/202003/1948294-20200312212151050-1805000883.png)

 

### 阻止事件传播

-  如果想只触发当前点击对象的事件，不想让外层的事件触发 ，可以使用不冒泡**e.cancelBubble=true**或不传播 **e.stopPropagation()**



```js
    var box = document.querySelector('.box')
    var atr = document.querySelector('.atr')
    box.onclick = function (e) {
        e.stopPropagation() // 不传播
        console.log('我被点击了box')
    }
    atr.onclick = function (e) {
        e.cancelBubble=true //不冒泡
        console.log('我被点击了atr')
    }
```

### 事件委托

-  就是把我要做的事情委托给别人来做

- 因为我们的冒泡机制，点击子元素的时候，也会同步触发父元素的相同事件 ，所以我们就可以把子元素的事件委托给父元素来做

-  点击子元素的时候，不管子元素有没有点击事件，只要父元素有点击事件，那么就可以触发父元素的点击事件

```js
    var box = document.querySelector('.box')
    var atr = document.querySelector('.atr')
    
    atr.onclick = function (e) {
        console.log('我被点击了atr')
    }
```

**target属性：**

• target 这个属性是事件对象里面的属性，表示你点击的目标

• 当你触发点击事件的时候，你点击在哪个元素上，target 就是哪个元素

• 这个 target 也不兼容，在 IE 下要使用 srcElement

```js
    var box = document.querySelector('.box')
    var atr = document.querySelector('.atr')
    
    atr.onclick = function (e) {
        var e = e || window.event //event兼容写法
        var target = e.target || e.srcElement //target兼容写法
        console.log(target)
    }
```

### 委托

**原理**：利用冒泡原理，把事件添加到父元素或祖先元素上，触发执行效果。

• 这个时候，当我们点击 box里面的元素的时候，也可以触发 box 的点事件

• 并且在事件内不，我们也可以拿到你点击的到底是哪个对象

• 这个时候，我们就可以把 li 的事件委托给 box 父级来做



**示例：**在ul上绑定事件，每个li，包括新增加的li都可以点击变色



```js
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <style>
        ul {
            list-style-type: none;
        }
        
        li {
            border: 1px black solid;
            line-height: 30px;
            height: 30px;
        }
    </style>
</head>

<body>


        <ul id="ul">
            <li class="item">1</li>
            <li class="item">2</li>
            <li class="item">3</li>
            <li class="item">4</li>
            <li class="item">5</li>
        </ul>

        <button id="btn">点击添加节点</button>

</body>
<script>

    document.getElementById("ul").onclick = function(e) {
        var e = e || window.event //event兼容写法
        var target = e.target || e.srcElement //target兼容写法

        if (e.target.nodeName == "LI") {
            e.target.style.background = "red";
        }
    }

    document.getElementById("btn").onclick = function() {
        var nodeDiv = document.createElement("li");
        document.getElementById("ul").appendChild(nodeDiv)

    }
</script>

</html>
```



#### 为啥使用事件委托？

1. 提高性能和效率
2. 减少事件注册，节省内存占用

3. 未来元素无需再次注册事件

4. 后面添加的元素也会有事件



#### 默认行为

• 默认行为，就是不用我们注册，它自己就存在的事情

　　° 比如我们点击鼠标右键的时候，会自动弹出一个菜单

　　° 比如我们点击 a 标签的时候，我们不需要注册点击事件，他自己就会跳转页面

• 这些不需要我们注册就能实现的事情，我们叫做默认事件

### 阻止默认行为

• 有的时候，我们不希望浏览器执行默认事件

　　- 比如我给 a 标签绑定了一个点击事件，我点击你的时候希望你能告诉我你的地址是什么 ，而不是直接跳转链接

　　- 那么我们就要把 a 标签原先的默认事件阻止，不让他执行默认事件

• 我们有两个方法来阻止默认事件

　　- e.preventDefault() : 非 IE 使用

　　- e.returnValue = false ：IE 使用

• 我们阻止默认事件的时候也要写一个兼容的写法



```js
    var oA = document.querySelector('a')
    a.addEventListener('click', function (e) {
        e = e || window.event
        console.log(this.href)
        //下面这个是兼容写法
      //  e.preventDefault ? e.preventDefault() : e.returnValue = false  //写法1
        
         if (event.preventDefault()) {         //写法2
            event.preventDefault();
        } else {
            event.returnValue = false;
        }
    })
```



作者：东城以东

出处：https://www.cnblogs.com/dcyd/

本文版权归作者和博客园共有，欢迎转载，但未经作者同意必须保留此段声明，且在文章页面明显位置给出原文连接，否则保留追究法律责任的权利。





