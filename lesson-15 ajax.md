# lesson-15 ajax

## 简介

AJAX即“Asynchronous Javascript And XML”（异步JavaScript和XML），**是指一种创建交互式网页应用的网页开发技术**。Ajax不是一种新的编程语言，而是**使用现有标准的新方法**。AJAX可以在不重新加载整个页面的情况下，与服务器交换数据。这种异步交互的方式，使用户单击后，不必刷新页面也能获取新数据。使用Ajax，用户可以创建接近本地桌面应用的**直接、高可用、更丰富、更动态**的Web用户界面。

## 同步与异步

1. 同步：是阻塞的，浏览器在向服务器发送请求之后一直等待服务器的响应，而没有做其他事情。
2. 异步：非阻塞的，浏览器向服务器发送请求之后，继续执行其他代码，知道服务器响应，浏览器
   中断当前的任务，处理服务器响应。

##  Ajax所包含的技术

大家都知道ajax并非一种新的技术，而是**几种原有技术的结合体**。它由下列技术组合而成。



> 1. 使用CSS和XHTML来表示。
>
> 2. 使用DOM模型来交互和动态显示。
>
> 3. **使用XMLHttpRequest来和服务器进行异步通信。**
>
> 4. 使用javascript来绑定和调用。



## 工作原理

**Ajax的工作原理相当于在用户和服务器之间加了—个中间层(AJAX引擎)**，使用户操作与服务器响应异步化。并不是所有的用户请求都提交给服务器。像—些数据验证和数据处理等都交给Ajax引擎自己来做,，只有确定需要从服务器读取新数据时再由Ajax引擎代为向服务器提交请求。



**具体工作流程：**

1. JavaScript程序创建一个XMLHttpRequest对象
2. 使用XMLHttpRequest对象向服务器发送http请求
3. 服务器响应并给客户端返回信息
4. 客户端JavaScript调用反馈的信息，将数据呈现在浏览器的窗口上



**来看看和传统方式的区别**

![img](https://img-blog.csdn.net/20150716193059952)

**再来看看它们各自的交互**

（1）浏览器的普通交互方式



![mark](http://qiniu.wind-zhou.com/blog/210309/HKmEckm1m4.png?imageslim)



（2）浏览器的Ajax交互方式



![mark](http://qiniu.wind-zhou.com/blog/210309/A44DhD1h2G.png?imageslim)





## ajax对象的属性和方法



输出一个ajax对象：

![mark](http://qiniu.wind-zhou.com/blog/210309/BmHbLGAemb.png?imageslim)



###ajax属性

#### **1. onreadystatechange 属性**

onreadystatechange 属性存有处理服务器响应的函数。
下面的代码定义一个空的函数，可同时对 onreadystatechange 属性进行设置：

```javascript
xmlHttp.onreadystatechange = function() {
    //我们需要在这写一些代码
}
```

#### **2. readyState 属性**

readyState 属性存有服务器响应的状态信息。**每当 readyState 改变时，onreadystatechange 函数就会被执行**。

 onreadystatechange 事件被触发 4 次（0 - 4）, 分别是： 0-1、1-2、2-3、3-4，对应着 readyState 的每个变化。

readyState 属性可能的值：

| 状态 | 描述                                                         |
| :--- | :----------------------------------------------------------- |
| 0    | 请求（**XMLHttpRequest对象**）未初始化（在调用 open() 之前） |
| 1    | XMLHttpRequest开始发送请求（调用 send() 之前）               |
| 2    | 请求已发送（这里通常可以从响应得到内容头部）                 |
| 3    | 请求处理中（**正在读取响应**）（响应中通常有部分数据可用，但是服务器还没有完成响应） |
| 4    | 请求已完成（可以访问服务器响应并使用它）                     |

我们要向这个 onreadystatechange 函数添加一条 If 语句，来测试我们的响应是否已完成(意味着可获得数据)：

```javascript
xmlHttp.onreadystatechange = function() {
    if (xmlHttp.readyState == 4) {
        //从服务器的response获得数据
    }
}
```

#### **3. responseText 属性**

可以通过 responseText 属性来**取回由服务器返回的数据**。  （以字符串形式，包括字符串形式的json数据）
在我们的代码中，我们将把时间文本框的值设置为等于 responseText：

```javascript
xmlHttp.onreadystatechange = function() {
    if (xmlHttp.readyState == 4) {
        document.myForm.time.value = xmlHttp.responseText;
    }
}
```

其它属性如下：

![img](https://img-blog.csdn.net/20150716190337737)

###  XMLHttpRequst的方法

#### **1. open() 方法**

open() 有三个参数。第一个参数定义发送请求所使用的方法，第二个参数规定服务器端脚本的URL，第三个参数规定应当对请求进行异步地处理。



```javascript
xmlHttp.open("GET","test.php",true);
```

![mark](http://qiniu.wind-zhou.com/blog/210309/KFjD5fDAkh.png?imageslim)



#### **2. send() 方法**

send() 方法将请求送往服务器。如果我们假设 HTML 文件和 PHP 文件位于相同的目录，那么代码是这样的：

```javascript
xmlHttp.send(string);
```

**open()方法并不会真正发送请求，而只是启动一个请求以备发送**。通过 send()方法进行发送请求，send()方法接受一个参数，作为请求主体发送的数据。如果不需要则，必须填 null。执行 send()方法之后，请求就会发送到服务器上。

其它方法如下：

![img](https://img-blog.csdn.net/20150716190353170)



## ajax编程过程

>1. 创建XMLHttpRequest对象。
>2. 设置请求方式。
>3. 调用回调函数。
>4. 发送请求。



（1）创建XMLHttpRequest对象

**直接上兼容性写法：**

```js
 // 创建ajax对象
        if (window.XMLHttpRequest) {
            var xmlHttp = new XMLHttpRequest()
        } else {
            var xmlHttp = new ActiveXObject("Microsoft.XMLHTTP") //兼容ie6
        }
```



（2）创建连接请求

在WEB开发中，请求有两种形式，一个是get，一个是post，所以在这里需要设置一下具体使用哪个请求，

XMLHttpRequest对象的open()方法就是来设置请求方式的。

```js
   xmlHttp.open("post", "http://qhdlink-student.top/student/login.php");
```

>## GET 还是 POST？
>
>与 POST 相比，GET 更简单也更快，并且在大部分情况下都能用。
>
>然而，在以下情况中，请使用 POST 请求：
>
>- 无法使用缓存文件（更新服务器上的文件或数据库）
>- 向服务器发送大量数据（POST 没有数据量限制）
>- 发送包含未知字符的用户输入时，POST 比 GET 更稳定也更可靠
>
>## 异步 - True 或 False？
>
>AJAX 指的是异步 JavaScript 和 XML（Asynchronous JavaScript and XML）。
>
>XMLHttpRequest 对象如果要用于 AJAX 的话，其 open() 方法的 async 参数必须设置为 true：
>
>xmlhttp.open("GET","ajax_test.html",true);
>
>对于 web 开发人员来说，发送异步请求是一个巨大的进步。很多在服务器执行的任务都相当费时。AJAX 出现之前，这可能会引起应用程序挂起或停止。
>
>通过 AJAX，JavaScript 无需等待服务器的响应，而是：
>
>- 在等待服务器响应时执行其他脚本
>- 当响应就绪后对响应进行处理

（3）设置http请求头

```js
  // 设置请求头中的content-type 

        xmlHttp.setRequestHeader("content-type", "application/x-www-form-urlencoded");
```

（4）发送

   ```js
   xmlHttp.send(data);
   ```

如果是使用post方法，则需要设置data。

（5）调用回调函数

open方法的第三个参数选择的是true，那么当前就是异步请求，这个时候需要写一个回调函数，XMLHttpRequest对象有一个onreadystatechange属性，这个属性返回的是一个匿名的方法，所以回调函数就在这里写xmlHttp.onreadystatechange=function{},function{}内部就是回调函数的内容。所谓回调函数，就是请求在后台处理完，再返回到前台所实现的功能。

```js
 xmlHttp.onreadystatechange = function() {
            if (xmlHttp.readyState == 4 && xmlHttp.status == 200) {
                var resdata = xmlHttp.responseText;
                console.log(resdata)
                alert("登陆成功")
            }
        }
```



>**AJAX状态值与状态码区别**:
>
> **AJAX状态值是指**，运行AJAX所经历过的几种状态，无论访问是否成功都将响应的步骤，可以理解成为AJAX运行步骤。如：正在发送，正在响应等，由AJAX对象与服务器交互时所得；使用“ajax.readyState”获得。（由数字1~4单位数字组成）
>**AJAX状态码是指**，无论AJAX访问是否成功，由HTTP协议根据所提交的信息，服务器所返回的HTTP头信息代码，该信息使用“ajax.status”所获得；（由数字1XX,2XX三位数字组成，详细查看RFC）
>这就是我们在使用AJAX时为什么采用下面的方式判断所获得的信息是否正确的原因。

**实战练习：**



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

    // 兼容写法
    function login() {
        // 创建ajax对象
        if (window.XMLHttpRequest) {
            var xmlHttp = new XMLHttpRequest()
        } else {
            var xmlHttp = new ActiveXObject("Microsoft.XMLHTTP") //兼容ie6
        }

            // 初始化ajax
        xmlHttp.open("post", "http://qhdlink-student.top/student/login.php");

        // 设置请求头中的content-type 
        xmlHttp.setRequestHeader("content-type", "application/x-www-form-urlencoded");

        // 拼接数据并发送数据
        var user = document.getElementById("username").value;
        var pwd = document.getElementById("password").value;
        var userclass = document.getElementById("userclass").value;
        var ctype = document.getElementById("usertype").value;

        var data = "username=" + user + "&userpwd=" + pwd + "&userclass=" + userclass + "&type=" + ctype;

        console.log(data)

        xmlHttp.send(data);

        xmlHttp.onreadystatechange = function() {
            if (xmlHttp.readyState == 4 && xmlHttp.status == 200) {
                var resdata = xmlHttp.responseText;
                console.log(resdata)
                alert("登陆成功")
            }
        }
    }


    document.getElementById("btn").onclick = login;

</script>

</html>
```



输出：

![mark](http://qiniu.wind-zhou.com/blog/210309/I9bFh2bbg4.png?imageslim)



##  jquery AJAX

　ajax有两种实现方式，其实原理都是应用的javascript。**第一种是原生的ajax**，就是用原生的javascript实现的，这种方式应用的很少，但是能体现出ajax的实现原理，我在这里就不做过多的陈述了，有兴趣的小伙伴可以自己去查找一些资料。今天着重要说的是js的一个nb的封装库实现的ajax，没错，就是jqury，这个库实在是太好了，爱不释手啊，为什么这么多js的封装库，但是jquery最流行呢，因为它免费啊！免费的东西我们在用的时候，感觉到很爽，开个玩笑，jquery之所以流行主要的原因是因为它是一个轻量级的js封装库，而且封装的也非常好，但是也跟免费有一点关系。还有一些常用的js封装库，例如ReactJS、Angular、vue.js、Meteor、Ember.js。

　　jquery实现的ajax有三种表现形式：

　 **(1)$.ajax({...})**

　**(2)$.get(...)**

​    **(3)$.post(...)**



### $.ajax()

**关于 jQuery 与 AJAX：**

jQuery 提供多个与 AJAX 有关的方法。

通过 jQuery AJAX 方法，您能够使用 HTTP Get 和 HTTP Post 从远程服务器上请求文本、HTML、XML 或 JSON - 同时您能够把这些外部数据直接载入网页的被选元素中。



**如果没有 jQuery，AJAX 编程还是有些难度的。**编写常规的 AJAX 代码并不容易，因为不同的浏览器对 AJAX 的实现并不相同。这意味着您必须编写额外的代码对浏览器进行测试。不过，jQuery 团队为我们解决了这个难题，我们只需要一行简单的代码，就可以实现 AJAX 功能。

**语法：**

```js
$.ajax({option});
```

option表示用于设置ajax请求的类型，其实是一个对象。





```js
$(function () {
    $.ajax({
        url: "test.json",
        type: "get",
        cache: false,
        async: false,　　　　 
        data: null,
        beforeSend: function (request) {
            console.log(request);
            console.log("请求之前");
        },
        complete: function (request, testStatus) {
            console.log("\n");
            console.log("请求完成");
            console.log(request);
            console.log(testStatus);
        },
        success: function (data,textStatus, request) {
            console.log("\n");
            console.log("请求成功");
            console.log(data);
        },
        error: function (request, textStatus, errorThrown) {
            console.log("\n");
            console.log("请求出错");
            console.log(request);
            console.log(textStatus);
            console.log(errorThrown);
        },
        dataType: "json",
        dataFilter: function (data, type) {
            console.log("\n");
            console.log("拦截成功");
            console.log("拦截的数据为："+data);
            console.log("拦截的数据类型为："+type);
        }
    })
});
```





这就是ajax请求的示例代码，可以看到，好像参数很多啊，没事，咱们慢慢来说

- **url：请求的地址**，上面的代码是我模拟的json数据，单独挡在了test.json中，当我们向服务器进行请求时，把这个url换成对应的url就行，注意，url后面是一个字符串，我刚开始学习ajax的时候就是总忘写那对双引号。
-  **type：请求的类型**，就是get请求还是post请求，当然，也可以为其它，但是前提是浏览器必须也得支持。默认为get。

- cache：请求时是否使用浏览器缓存的数据，默认为true，即开启缓存。当dataType为xml时，默认为false。

- **data**: 请求的数据，如果是get方式请求，就是拼接在url问号后面的参数，post请求就是在请求参数中的内容。

  **会自动转换为字符串，以json方式发送到服务器。**如果不需要给服务器发数据可以不写。

- **async**：是否开启异步请求，默认为true，我认为，把**这个改为false的，都是脑袋里有炮**，既然都用ajax了，寻求的就是异步的那种快感。
-   beforeSend：这里的value为一个函数，就是当请求之前执行的函数，这个函数里有一个参数，就是XMLHttpRequest，这个是一些请求的信息，如果此函数返回false，此次请求就会被取消。
-   complete：当请求处理完成之后（success执行完之后）执行的函数，参数为XMLHttpRequest和textStatus，第一个参数和之前的相同，第二个参数为请求的状态，即error或者success。
-   **success**：请求成功执行的函数，参数为data、textStatus、XMLHttpRequest，data就是请求回来的数据。

- error: 当请求失败时执行的函数，参数为XMLHttpRequest， textStatus、errorThrown，error打印出来的信息就像是java抛出来异常的打印堆栈的信息。
-  **dataType**：期望被请求方返回的数据类型，常见的有html、xml、json、jsoup、text、script。
-   dataFilter：这个是拦截器，和servlet中的filter是一样的，回拦截到被请求方返回的数据，data就是被拦截的数据，而type就是dataType中填写的内容。

关于第一种ajax的讲解就有目前这些，其实这里面的参数不只这些，但是我列举出来的都是一些常用的。

>参考链接:[ajax详细](https://www.cnblogs.com/Lighting-Sui/p/11494298.html)



**实战练习：**

```js
   
<script>
    $(function() {

        var ajaxObj = {
            url: "http://qhdlink-student.top/student/login.php",
            dataType: "text",
            type: "post",
            data: {
                "username": "zyp",
                "userpwd": "123456",
                "userclass": "64",
                "type": "4",
            },
              "async": "true",
            success: function(data) { //状态码等于4和200时调用，jquery会自动判断
                console.log(data)
            },
            error: function(error) {
                console.log("请求失败")
            }
        }
        $.ajax(ajaxObj);
    })
</script>
```





### $.get()和$.post()

这两个方法是$.ajax()的快捷方式，他们分别使用get和post发送数据，并且根据各自的语法，可以省略选项的名称，按照顺序，直接写值。

#### jQuery $.get() 方法

$.get() 方法通过 HTTP GET 请求从服务器上请求数据。

 **语法：**

>**$.get(*URL*,*callback*);**
>
>必需的 *URL* 参数规定您希望请求的 URL。
>
>可选的 *callback* 参数是请求成功后所执行的函数名。

#### jQuery $.post() 方法

$.post() 方法通过 HTTP POST 请求向服务器提交数据。

**语法:**

>$.post(*URL,data,callback*);
>
>必需的 *URL* 参数规定您希望请求的 URL。
>
>可选的 *data* 参数规定连同请求发送的数据。
>
>可选的 *callback* 参数是请求成功后所执行的函数名。

**实战练习**：将上面案例使用$.post()重写

```js
    $(function() {
        var urlX = "http://qhdlink-student.top/student/login.php";

        var data = {
            "username": "zyp",
            "userpwd": "123456",
            "userclass": "64",
            "type": "4",
            "async": "true"
        };

        var success = function(data) { //状态码等于4和200时调用，jquery会自动判断
            console.log(data)
        };

        $.post(urlX, data, success);
    })
```



这是$.post()的参数不再是一个对象，而是三个参数。

## websocket

亲后端交互的方式还有websocket

![mark](http://qiniu.wind-zhou.com/blog/210308/Ad36lEHgEf.png?imageslim)





![mark](http://qiniu.wind-zhou.com/blog/210308/fHEgbm04JC.png?imageslim)







![image-20210308111154702](C:\Users\zhouzheng\AppData\Roaming\Typora\typora-user-images\image-20210308111154702.png)











