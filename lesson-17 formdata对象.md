# lesson-17 formdata对象

## 简介

XMLHttpRequest 是一个浏览器接口，通过它，我们可以使得 Javascript 进行 HTTP (S) 通信。XMLHttpRequest 在现在浏览器中是一种常用的前后台交互数据的方式。2008年 2 月，XMLHttpRequest Level 2 草案提出来了，相对于上一代，它有一些新的特性，其中 FormData 就是 XMLHttpRequest Level 2 新增的一个对象，利用它来提交表单、模拟表单提交，**当然最大的优势就是可以上传二进制文件**。

## 作用

1、**将form表单元素的name与value进行组合，实现表单数据的序列化**，从而减少表单元素的拼接，提高工作效率。

 2、**异步上传文件**

## formdata对象

首先我们先看一下formdata对象长什么样。

![mark](http://qiniu.wind-zhou.com/blog/210312/j6jmIjJ67B.png?imageslim)



里面的方法都是对拼接数据的增删改查。

下面实验几个典型的方法。

（1）获取数据 get()与getAll()

get("username")方法会获取匹配到的第一个名字为username的 值。

getAll("usernmae")方法会获取所有匹配到的值，**如果有多个则会以数组方式返回**。



```js
<!DOCTYPE html>
<html lang="zh-CN">

<head>
    <meta charset="utf-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <script src="https://cdn.bootcdn.net/ajax/libs/jquery/3.5.1/jquery.min.js"></script>
    <!-- 上述3个meta标签*必须*放在最前面，任何其他内容都*必须*跟随其后！ -->
    <title>formdata</title>

</head>

<body>

    <form id="myform">

        <p>姓名1：<input type="text" name="username"></p>
        <p>姓名2：<input type="text" name="username"></p>
        <p>姓名3：<input type="text" name="username"></p>
        <p>姓名4：<input type="text" name="username"></p>
        <p>密码：<input type="password" name="userpwd"></p>
        <p>班级：<input type="text" name="userclass"></p>
        <p>权限：<input type="text" name="type"></p>

        <p>
            <select name="city" id="city">
                <option value="shanghai">上海</option>
                <option value="hangzhou">杭州</option>
                <option value="nanjing">南京</option>
                <option value="qinhuangdao">秦皇岛</option>
            </select>
        </p>
    </form>
    <button id="btn">提交</button>

</body>

<script>
    var submit = document.getElementById("btn");

    submit.onclick = function() {

        var myform = document.getElementById("myform");
        var myformdata = new FormData(myform);
        console.log(myformdata)

        console.log("使用get方法获取：" + myformdata.get("username")) //使用get方法获取username
        console.log("使用getALL方法获取：" + myformdata.getAll("username")) //使用getAll获取

        console.log("密码：" + myformdata.get("userpwd")) //拿到密码
        console.log("城市：" + myformdata.get("city")) //拿到城市

    }
</script>

</html>
```

输出：

![mark](http://qiniu.wind-zhou.com/blog/210312/GIi4IA7g0E.png?imageslim)



（2）添加数据append()



**通过append(key,value)在数据末尾追加数据**

```js
<script>
    var submit = document.getElementById("btn");

    submit.onclick = function() {

        var myform = document.getElementById("myform");
        var myformdata = new FormData(myform);

        myformdata.append("hobby", "travel")//添加数据
        console.log(myformdata.get("hobby"))

    }
</script>
```

输出：travel



（3） 修改数据set()

```js
<script>
    var submit = document.getElementById("btn");

    submit.onclick = function() {

        var myform = document.getElementById("myform");
        var myformdata = new FormData(myform);

        myformdata.set("city", "hengshui")  //修改city的值

        console.log("城市：" + myformdata.get("city")) //拿到城市
    }
</script>
```



**输出**：选中的是“杭州”，但是人为的修改成了衡水。

![mark](http://qiniu.wind-zhou.com/blog/210312/lA5mhdCg83.png?imageslim)

（4）删除数据 delete()



```js
<script>
    var submit = document.getElementById("btn");

    submit.onclick = function() {

        var myform = document.getElementById("myform");
        var myformdata = new FormData(myform);
        console.log(myformdata)

        myformdata.delete("city")   //删除city的值
        console.log("城市：" + myformdata.get("city")) //拿到城市


    }
</script>
```

输出：由于删除了city，因此输出位null

![mark](http://qiniu.wind-zhou.com/blog/210312/Fb8HmHgB74.png?imageslim)



## 使用ajax实现异步通信

**示例：**

新闻接口。

**目录结构：**

![mark](http://qiniu.wind-zhou.com/blog/210312/m023mGCaHG.png?imageslim)



**新闻列表html：**

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
    <ul id="navlist">

    </ul>
</body>

<script src="./myajax.js"></script>

<script>
    function process(data) {
        //1、遍历data
        console.log(data)
        var navlist = document.getElementById("navlist");
        for (var i in data) {
            var listcon = "<li><a href='newsdatail.html?m=" + data[i].id_news + "'>" + data[i].title_news + " " + data[i].time_news + "</a></li>";
            navlist.innerHTML += listcon;
        }
    }
    myajax("post", "http://qhdlink-student.top/student/newsa.php", "username=zyp&userpwd=123456&userclass=64&type=4", process)
</script>

</html>
```

**newdatail.html：**

```js
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
</head>

<body id="con">

</body>
<script src="./myajax.js"></script>
<script>
    var queryString = location.search;
    var num = queryString.split("=")[1];
    console.log(num);

    var dataSend = "username=zyp&userpwd=123456&userclass=64&type=4&m=" + num + "";

    function sucess(dataDetailObj) {
        var newCon = dataDetailObj[0].info_news;
        console.log(newCon)
        document.getElementById("con").innerHTML = newCon;
    }
    myajax("post", "http://www.qhdlink-student.top/student/newsinfo.php", dataSend, sucess)
</script>

</html>
```

**封装ajajx：**

```js
(function() {
    window.myajax = function(method, url, data, callback) {

        var xhr = new XMLHttpRequest();
        xhr.open(method, url)
        xhr.setRequestHeader("content-type", "application/x-www-form-urlencoded");
        xhr.send(data);

        xhr.onreadystatechange = function() {
            if (this.readyState == 4 & this.status == 200) {
                var resdata = this.responseText;
                var dataObj = JSON.parse(resdata);
                callback(dataObj)
            }
        }
    }
})()
```



formdata可以以二进制形式发送文件

![mark](http://qiniu.wind-zhou.com/blog/210310/e7JBaHIfgK.png?imageslim)





![mark](http://qiniu.wind-zhou.com/blog/210310/md01gmkc7I.png?imageslim)

可以拦截ajax





















