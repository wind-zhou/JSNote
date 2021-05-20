# lesson-25 本地存储和离线存储

## 前言

前端的存储方式有：**localStorage、sessionStorage、cookie、**UserData、**webSQL、indexeddb**、HTML5离线存储等。各个存储方式有各自的优缺点，本文我们来探讨一下不同存储的功能及区别。

h5有个新增的功能使本地数据库，这个我还没没弄明白，现在不做讨论。

## 本地存储

**本地存储的概念：**

本地存储**将用户的一些偏好，用户当前的状态**等等简单的信息，**存储到本地电脑上**。再次再访问的时候就可以直接调用。

客户端的存储遵循“**同源策略**”，不同站点之间的页面是无法互相读取对方存储的数据，而同一站点的不同页面之间是可

以互相共享存储的数据，网页**可以选择他们存储数据的有效期限**。



**本地存储有三种主要的实现方式：**

- cookie
- localStorage
- sessionStorage

### cookie

#### 什么是cookie

cookie的内容是一个个的键值对组成的字符串。

cookie的设计初衷是**给服务器端脚本用来存储少量数据的**，该数据会在每次请求一个相关的urI时**传递到服务器中**，不同

浏览器对于本地cookie的数量都有一定的限制，不允许大量的使用cookie,并且每个cookie文件的大小不能大于4KB;

**（每次请求服务器时，会将cookie放在http的请求头中。）**



下图是打开百度时的http请求报文结构：

![mark](http://qiniu.wind-zhou.com/blog/210325/ILBh2fkbCH.png?imageslim)



#### 各个浏览器对cookie数量的限制

不同浏览器对cookie数量有限制，不允许大量使用cookie

![mark](http://qiniu.wind-zhou.com/blog/210322/D89IgK5bCm.png?imageslim)

#### cookie的用途

主要应用：**购物车、客户端登录**

#### cookie的存取

（1）**首先判断浏览器是否支持cookie**

注：chrome放到远程服务器才能看到效果。

```js
<script>
    if (navigator.cookieEnabled) {
        alert("支持cookie")
    } else {
        alert("不支持cookie")
    }
</script>
```

(2)**创建cookie**

JavaScript 可以使用 **document.cookie** 属性来创建 、读取、及删除 cookie。

JavaScript 中，创建 cookie 如下所示：

```js
document.cookie="username=John Doe";
```

您还可以为 cookie 添加一个过期时间（以 UTC 或 GMT 时间）。**默认情况下，cookie 在浏览器关闭时删除**：

```js
document.cookie="username=John Doe; expires=Thu, 18 Dec 2043 12:00:00 GMT";
```

您可以使用 path 参数告诉浏览器 cookie 的路径。**默认情况下，cookie 属于当前目录**。

```js
document.cookie="username=John Doe; expires=Thu, 18 Dec 2043 12:00:00 GMT; path=/";
```



>**实验证明**：如果设置path路径，默认为当前目录，也就是说是由该文件所在目录的同级文件或者下级文件才能共享cookie。



(3) **读取cookie**

在 JavaScript 中, 可以使用以下代码来读取 cookie：

```js
var x = document.cookie;
```

(4) **删除 cookie**

删除某个cookie只需将对应的属性的过期时间设置为现在之前的事件即可。

如下所示，设置为 Thu, 01 Jan 1970 00:00:00 GMT:

```js
document.cookie = "username=; expires=Thu, 01 Jan 1970 00:00:00 GMT";
```

**注意**，当您删除时不必指定 cookie 的值。



**看下面例子：**



```js
   setCookie('username', 'zhouzheng', 7);
        setCookie('age', '24', 7);
        setCookie('sex', 'man', 7);
        setCookie('height', '173', 7);
        setCookie('hobby', 'travel', 7);
        setCookie('age', '12', 7);
     var x = document.cookie;
        console.log(x)
```



此时输出为：

![mark](http://qiniu.wind-zhou.com/blog/210325/LjFLl1AdI4.png?imageslim)

删除sex后：

```js
    document.cookie = "sex=; expires=Thu, 01 Jan 1970 00:00:00 GMT";
```

![mark](http://qiniu.wind-zhou.com/blog/210325/akD9iji0Cm.png?imageslim)



>### 几点常识：
>
>
>
>####（1）多条cookie的拼接问题
>
>注：如果写多个document.cookie来设置cookie，则会产生多条cookie，不过会被用“；”做间隔拼接在一起。
>
>例：
>
>在a.html设置cookie
>
>```js
><script>
>if (navigator.cookieEnabled) {
>   // alert("支持cookie")
>   // document.cookie = "username=John Doe; expires=Thu, 18 Dec 2043 12:00:00 GMT; path=/";
>   // 设置cookie
>
>   var date = new Date();
>   var timestamp = date.getTime();
>   console.log(timestamp)
>   var time = timestamp + 3 * 60 * 1000;
>   document.cookie = "user=trump&age=78&hobby=swim;expires=" + time;
>   document.cookie = "address=hangzhou&job=coder;expires=" + time;
>   var x = document.cookie;
>   console.log(x)
>} else {
>   alert("不支持cookie")
>}
></script>
>```
>
>![mark](http://qiniu.wind-zhou.com/blog/210325/95lElLGbiB.png?imageslim)
>
>

>#### （4）手动封装setCookie函数
>
>cookie 并没有专有的API来进行设置，需要自己进行手动封装。
>
>例：
>
>```js
>    function setCookie(cname, cvalue, exdays) {
>        var d = new Date();
>        d.setTime(d.getTime() + (exdays * 24 * 60 * 60 * 1000));
>        var expires = "expires=" + d.toGMTString();
>        document.cookie = cname + "=" + cvalue + "; " + expires;
>    }
>```
>
>####（5）重复给cookie赋值的覆盖问题
>
>如果设置cookie时，设置了已经有的cookie值（给相同的键赋值），则会对之前的进行覆盖。
>
>
>
>**看下面例子：**
>
>
>
>![mark](http://qiniu.wind-zhou.com/blog/210325/e2a18IJfeh.png?imageslim)
>
>```js
>   setCookie('sex', 'women', 7);
>```
>
>重新赋值后：
>
>![mark](http://qiniu.wind-zhou.com/blog/210325/8dCI0LcmL0.png?imageslim)
>
>

#### cookie的优缺点

- **优点**：
  可控制过期时间，使其不会长期有效
  可扩展、可用性比较好
  可加密减少cookie被破解的可能性
- **缺点**：
  数量和长度有限制，最多20条，最长不能超过4k
  在请求头上带着数据安全性差

#### 综合实例：使用cookie实现登录后用户名预加载

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

    <ul>
        <li> 姓名：<input type="text" id="username"></li>
        <li> 密码： <input type="password" id="password"></li>
        <li>班级： <input type="text" id="userclass"> </li>
        <li> 权限号码： <input type="text" id="usertype"></li>
        <li></li>
    </ul>

    <button id="btn" type="button">登录</button>

</body>

<script>
    // 每次刷新页面时获取cookie，并将相应的值填入输入框
    var cookieOfName = document.cookie;
    var xxxxx = cookieOfName.split('=')[1];
    // console.log(xxxxx)
    document.getElementById("username").value = xxxxx;

    function setCookie(cname, cvalue, exdays) {
        var d = new Date();
        d.setTime(d.getTime() + (exdays * 24 * 60 * 60 * 1000));
        var expires = "expires=" + d.toGMTString();
        document.cookie = cname + "=" + cvalue + "; " + expires;
    }


    function login() {

        if (window.XMLHttpRequest) {
            var xmlHttp = new XMLHttpRequest()
        } else {
            var xmlHttp = new ActiveXObject("Microsoft.XMLHTTP") //兼容ie6
        }

        xmlHttp.open("post", "http://www.qhdlink-student.top/student/login.php");
        xmlHttp.setRequestHeader("content-type", "application/x-www-form-urlencoded");

        var user = document.getElementById("username").value;
        var pwd = document.getElementById("password").value;
        var userclass = document.getElementById("userclass").value;
        var ctype = document.getElementById("usertype").value;


        var data = "username=" + user + "&userpwd=" + pwd + "&userclass=" + userclass + "&type=" + ctype;

        xmlHttp.send(data);

        xmlHttp.onreadystatechange = function() {
            if (xmlHttp.readyState == 4 && xmlHttp.status == 200) {

                var resData = this.responseText;
                console.log(resData)
                setCookie("username", 'zyp', 7) //设置cookie
                    // document.cookie = "username=; expires=Thu, 01 Jan 1970 00:00:00 GMT";
                var x = document.cookie;
                console.log(x)
            }
        }
    }

    document.getElementById("btn").onclick = login;
</script>

</html>
```



效果：

![mark](http://qiniu.wind-zhou.com/blog/210326/5kcKeJIajH.png?imageslim)



存储大小，是否发往服务器，时间作用域，空间作用域



### localStroage

**本地存储包括cookie和web存储，web存储又包含localStorage和sessionStorage。**

> web存储最初作为HTML5的一部分被定义成api形式，但是后来被剥离出来作为独立的标准，目前该标准还在制定当中，但是其中一部分内容已经被所有的主流浏览器兼容。**web存储标准描述的API包含localStorage和sessionStorage对象**。 **web本地存储更加安全和快速**，**这些数据不会被保存在服务器上**，只是用于用户请求网站数据，**他可以存储大量的数据，而不影响网站的性能。**



#### 语法



```js
window.localStorage
```

**保存数据语法：**

```js
localStorage.setItem("key", "value");
```

**读取数据语法：**

```js
var lastname = localStorage.getItem("key");
```

**删除数据语法：**

```js
localStorage.removeItem("key");
```

**清空：**

```js
localStorage.clear();
```



#### localStorage的特点

- **优点：**
  localStorage拓展了cookie的4k限制
  localStorage可以将第一次请求的5M大小数据直接存储到本地，相比于cookie可以节约带宽
  **localStorage的使用也是遵循同源策略的**，所以不同的网站直接是不能共用相同的localStorage
- **缺点：**
  需要手动删除，否则长期存在
  浏览器大小不一，版本的支持也不一样
  localStorage只支持string类型的存储，JSON对象需要转换
  localStorage本质上是对字符串的读取，如果存储内容多的话会消耗内存空间，会导致页面变卡
- **特点：**
  **同源策略限制、只在本地存储、永久保存、数据存储量大、同浏览器共享**

### sessionStorage



- sessionStorage的使用方法和localStorage对象的使用方法完全一样，**他们的区别在于存储的有效**
  **期和作用域不同**。
- localstorage存储的数据是永久性的，除非刻意的去删除，否则数据会一直保留在用户的电脑上永不
  过期
- sessionStorage存储的数据是临时的，当该脚本所在的最顶层的窗口或浏览器关闭以后，数据就会被
  删除。
- localStorage的作用域是限定在文档源级别的，(文档源是通过协议, 主机名以及端口三者来确定
  的)同一文档源之间的不同页面可以共享localStorage数据，可以互相读取,设置覆盖修改。
- sessionStorage的作用域也被限制在文档源中，不仅如此sessionStorage的作用域还被限定在窗口
  中，如果同源的文档渲染在不同的浏览器标签中，他们各自的sessionStorage数据无法共享;一个标
  签页面中的脚本是无法读取或者覆盖有另一个标签页脚本写入的数据，哪怕这两个标签页渲染的是同
  -个页面，运行的是同一个脚本也不行



>和localStroage的区别在于**有效期**和**作用域**不同。
>
>localStorage 永久有效除非可以删除，而sessionStorage只在当前**会话**过程中有效。
>
>localstorage的作用域是同源，sessionStorage的作用域是同源同窗口





##离线缓存

![mark](http://qiniu.wind-zhou.com/blog/210323/dF1iLJjD7C.png?imageslim)



离线存储

离线存储（浏览器缓存，客户端缓存)
传统的浏览器缓存，通过浏览器来判定需要缓存网页的那些内容到本地，例如缓存网页上的所有图片，css文件，js文件等等，当再次访问该页面时，浏览器会优先从浏览器缓存中读取缓存的内容，没有被缓存的内容才会向服务器请求相关内容。只有当缓存过期或者用户强制刷新缓存时才会重新向服务器请求内容。如果服务器页面内容发生了改变，但是浏览器缓存中的内容，还是旧页面内容，用户浏览的可能还会是日页面的内容。



传统的浏览器缓存无法控制缓存内容。并且可能会发生缓存过期。

control+F5强制缓存

类似于预加载

## H5离线缓存



![mark](http://qiniu.wind-zhou.com/blog/210323/0jmedgiJ71.png?imageslim)



可以自定义缓存内容，使用manifest 



![mark](http://qiniu.wind-zhou.com/blog/210323/feK7bDFcEl.png?imageslim)

![mark](http://qiniu.wind-zhou.com/blog/210324/bmf0mF9GJH.png?imageslim)

![mark](http://qiniu.wind-zhou.com/blog/210324/AF0K0LJJK3.png?imageslim)

![mark](http://qiniu.wind-zhou.com/blog/210324/6hjL6L6IDl.png?imageslim)

有些资源虽然已经缓存，但是浏览器识别不出来（强缓存没命中）



## 防抖和节流

防抖主要在前后台交互时的登录时

节点主要处理一些连续触发的事件，例如onresize事件、onmove事件，onscroll事件



![mark](http://qiniu.wind-zhou.com/blog/210324/eHd5kkaIGI.png?imageslim)



节流让规定的时间内只触发一次，（相当于用setTimeout把需要执行的函数保护起来）



