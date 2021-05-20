# lesson-7 string

可以是基本数据类型，也可以是一个对象（这与string的创建方式有关）

##创建string

- 直接赋值

  ```js
  var str="wind-zhou"
  ```

- new string();构造函数创建

  ```js
  var s=new string("wind-zhou")
  ```


他们在使用时没什么区别，**不过数据类型不同**（在内存中的存储方式不同）

```js
<script>
    var string1 = "wind-zhou";
    var string2 = new String("wind-zhou");
    console.log(string1)
    console.log(string2)
</script>
```

![mark](http://qiniu.wind-zhou.com/blog/201214/Jd485F6lgA.png?imageslim)

## string属性

**主要为：length**

## string 方法

###1、返回指定位置字符

#### charAt（index）

**作用：返回指定位置的字符**

*不怎么使用*

```js
<script>
    var s1 = "hello world";
    console.log(s1.charAt("1"))//输出：e
</script>
```

###2、返回指定字符的位置

####indexOf(检索值 [,开始检索位置])

**作用： 检索字符串**，**返回指定字符的位置**

语法：

```js
<script>
    var s1 = "hello world";
    var s2 = new String("wind-zhou");
    console.log(s1.indexOf("l", 4))     //输出9
</script>
```

#### lastIndexOf(检索值 [,开始检索位置])

**作用：从后往前检索字符串**

使用方法与indexOf相同

###3、拼接字符串

####concat（string1,string2,...）

**作用：拼接字符串**

语法：

```js
<script>
    var s1 = "hello world";
    var s2 = new String("wind-zhou");
    console.log(s2.concat(s1))   //输出  ：wind-zhouhello world
</script>
```

但这种方法不怎么,因为直接使用“+”来拼接更简单直观。



###4、截取字符串

####slice(start,end)

**作用：截取字符串**

语法：

```js
<script>
    var s1 = "hello world";
    var s2 = new String("wind-zhou");
    console.log(s1.slice(2, 7))//输出： llo w
</script>
```

截取部分包括start，不包括end，若第二个参数end不写，则代表截至末尾，两个参数也可以是负数。

>**为什么s1是基本的数据类型。也可以使用方法？**
>
>基本数据类型string会继承string对象的方法。



#### substr(start,长度)

**作用：截取字符串**

```js
<script>
    var s1 = "hello world";
    var s2 = new String("wind-zhou");
    var s3 = s2.substr(2, 3)
    console.log(s3)//输出：nd-
</script>
```

####substring(start,stop)

返回一个字符串的子串，包含start，不包含end，**不能写负数**

###5、字符串转数组

#### split()  **（重点）**

将字符串分割成**字符串数组**

括号里的参数是分隔符，注意，这里是选取目标字符串里的该字母作为分隔符。

```js
<script>
    var s1 = "hello world";
    var s2 = new String("wind-zhou");
    var s3 = "jhduohgiwohiqhcoburwytfioc"
    
    
    console.log(s1.split())  //整体作为一个字符串
    console.log(s1.split(""))//默认空格分隔  全部切割
    console.log(s3.split("o"))
</script>
```

![mark](http://qiniu.wind-zhou.com/blog/201213/Aak0jLcGhL.png?imageslim)

###6、转换大小写

#### toLowerCase()

#### toUpperCase()

将字符串转换成小写

## 练习（解析字符串参数）

```js
<script>
    var str1 = "http://baidu.com?name=wind-zhou&pwd=123456&age=18";
    //1、以问号分割一次
    //2、截取？后面内容
    //3、以&分隔
    //4、遍历此时的字符串数组
    //4.1、 以= 进行分隔
    //4.2 将所偶需要部分存储起来

    var str2 = str1.slice(str1.indexOf("?") + 1);
    var str3 = str2.split("&");
    var qarr = [];
    for (var i in str3) {
        var tmp = str3[i].split("=");
        qarr.push(tmp[1]);
    }
    console.log(qarr)

</script>
```

输出：

![mark](http://qiniu.wind-zhou.com/blog/201213/42eF8IjdHL.png?imageslim)





|    查询    |        charAt()<br />indexOf()         |
| :--------: | :------------------------------------: |
|     改     |             concat()<br />             |
| 转换为数组 |                split()                 |
|    截取    | slice()<br />substr()<br />substring() |
| 转换大小写 |    toLowerCase()<br />toUpperCase()    |



**数组和string对象对比**：

|            | 数组                                                         | string                                                       |
| ---------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| 常用属性   | length                                                       | length                                                       |
| 增         | push()<br />unshift()                                        | 无                                                           |
| 删         | pop()<br />shift()<br />delete()                             | 无                                                           |
| 查         | indexOf()                                                    | charAt()<br />indexOf()                                      |
| 改         | 颠倒---reverse()<br />拼接---concat()<br />截取---splice()slice()<br />转换---tostring()、join() | <br />拼接---concat()<br />截取---slice()、substr()、substring()<br />转换---split() |
| 遍历       | foreach()<br />map()<br />filter()                           | 无                                                           |
| 转换大小写 | 无                                                           | toLowerCase()<br />toUpperCase()                             |





















