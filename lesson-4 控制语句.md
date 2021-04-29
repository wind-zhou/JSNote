# lesson-4 控制语句

- 顺序结构
- 分支结构
  1. 单分支
  2. 双分支
  3. 多分支
- 多选一结构
- for循环
- while循环
- continue break

## 顺序结构

所有语句从上往下，逐条执行

## 分支结构

### 单分支结构

语句

```js
if(条件){
    语句1；
    语句2；
    ...;
}
```

**注：if后面的{}当只有一条语句时可以省略。**

### 双分支

语法

```js
if(条件){
    语句1；
    语句2；
    ...;
}else{
     语句1；
    语句2；
    ...;
}
```

### 多分支结构

```js
if(条件){
    语句1；
    语句2；
    ...;
}else if{
     语句1；
    语句2；
    ...;
}else if{
     语句1；
    语句2；
    ...;
}else{
    语句1；
    语句2；
    ...;
}
```

**有一个条件成立，就跳出判断。（类似电梯的过程）**

例：根据输入的分数，给出相应评级

```js
<script>
    var num = prompt("请输入分数");
    if (num >= 90) {
        document.write("A")
    } else if (num >= 80) {
        document.write("B")
    } else if (num >= 70) {
        document.write("C")
    } else if (num >= 60) {
        document.write("D")
    } else if (num < 60 && num >= 0) {
        document.write("不及格")
    }
</script>
```

### 多选一（switch）

语法

```js
switch(表达式/变量){
    case 值1:
        语句1；
        语句2；
        ...；
        break；
        
        case 值2:
        语句1；
        语句2；
        ...；
        break；
        
        case 值3:
        语句1；
        语句2；
        ...；
        break；
        
        default:
        语句；
}
```

例：根据输入的网址跳转指定页面

```js
<script>
    var webSite = prompt("输入网址");
    switch (webSite) {
        case "百度":
            location.href = "http://baidu.com";
            break;
        case "网易":
            location.href = "http://163.com";
            break;
        case "腾讯":
            location.href = "http://tecent.com";
            break;

        default:
            document.write("输错了憨逼！")
    }
</script>
```

## 循环结构

###for循环

语法

```js
<script>
    for (var i = 0; i < 10; i++) {
        document.write("<h3>hello 周正</h3>")
        document.write("<h3>hello" + i + "</h3>") 
    }
</script>
```

注：当在中间需要连接变量时。要把之前的用“”断开

几个实例：

1、 计算1-100所有的奇数的和 

```js
    var sum = 0;
    for (var i = 0; i <= 100; i++) {
        if (i % 2 != 0) {
            sum += i;
        }
    }
    document.write(sum)
```

2、写一个9*9乘法表

```html
<style>
    table {
        border-collapse: collapse;
    }
    
    td {
        height: 50px;
        width: 100px;
        border: 1px solid #000;
        text-align: center;
    }
</style>

<script>
    document.write("<table>")
    for (var i = 1; i <= 9; i++) { //i为行，j为列
        document.write("<tr>")
        for (var j = 1; j <= i; j++) {
            document.write("<td>" + j + "*" + i + "=" + i * j + "</td>")
        }
        document.write("</tr>")
    }
    document.write("</table>")
</script>
```

输出：

![mark](http://qiniu.wind-zhou.com/blog/201207/4DmjIcBg8H.png?imageslim)

3、输出4行*

（1）上三角

```js
<script>
    for (var i = 0; i <= 3; i++) {
        for (var j = 1; j <= (4 - i); j++) {
            document.write("*")
        }
        document.write("<br>")
    }
</script>
```

输出：

![mark](http://qiniu.wind-zhou.com/blog/201207/mI9dj8FA47.png?imageslim)



（2）下三角

```js
<script>
    for (var i = 1; i <= 4; i++) {
        for (var j = 1; j <= i; j++) {

            document.write("*")
        }
        document.write("<br>")
    }
</script>
```

输出：

![mark](http://qiniu.wind-zhou.com/blog/201207/hhd2K8HfJA.png?imageslim)

(3)输出正三角

```js

<script>
    for (var i = 1; i <= 4; i++) {
        //输出空格顶位置
        for (var a = 1; a <= 5 - i; a++) {
            document.write("&nbsp");
        }
        for (var j = 1; j <= (2 * i - 1); j++) {

            document.write("*")
        }
        document.write("<br>")
    }
</script>

```

输出：

![mark](http://qiniu.wind-zhou.com/blog/201207/7I0EdL6bGB.png?imageslim)

注：此题内套了两个for，一个用来输出空格

（4）倒三角

```js
<script>
    for (var i = 1; i <= 3; i++) {
        //输出空格
        for (var x = 0; x <= i; x++) {
            document.write("&nbsp");
        }
        //输出*
        for (var y = 1; y <= (7 - 2 * i); y++) {

            document.write("*")
        }
        document.write("<br>")
    }
</script>
```

输出：

![mark](http://qiniu.wind-zhou.com/blog/201207/1BlGhkjHkf.png?imageslim)	

>##分析：
>
>共两部分
>
>（1）使用一个for循环来输入空格 。来顶开`*`的位置
>
>| 位置 i | 空格数 x |
>| :----: | :------: |
>|   1    |    1     |
>|   2    |    2     |
>|   3    |    3     |
>
>所以：x=i
>
>（2）再使用一个for循环输出`*`
>
>| 位置 i | *的数量  y |
>| :----: | :--------: |
>|   1    |     5      |
>|   2    |     3      |
>|   3    |     1      |
>
>关系式为：`y=7-2*i` 
>
>###**关系式的由来：**
>
>设一个中间变量n
>
>| 位置 i | 中间变量 n | *的数量  y |
>| ------ | :--------: | :--------: |
>| 1      |     3      |     5      |
>| 2      |     2      |     3      |
>| 3      |     1      |     1      |
>
>y-n：y=2n-1
>
>n-i: n=4-i
>
>因此：y-i: 7-2i
>
>**扩展：当输出行数为num时**
>
>y=2*num+1-2i
>
>```js
><script>
>    // var num = prompt("输入需要输出的行数");
>    var num = 6;
>    for (var i = 1; i <= num + 1; i++) {  //注：倒三角比正三角行数少一行
>        //     //输出空格顶位置
>        for (var a = 1; a <= num + 2 - i; a++) {
>            document.write("&nbsp");
>        }
>        for (var j = 1; j <= (2 * i - 1); j++) {
>
>            document.write("*")
>        }
>        document.write("<br>")
>    }
>    for (var i = 1; i <= num; i++) {
>        //第二个倒三角
>        for (var x = 0; x <= i; x++) {
>            document.write("&nbsp");
>        }
>        for (var y = 1; y <= (2 * num + 1 - 2 * i); y++) {
>
>            document.write("*")
>        }
>        document.write("<br>")
>    }
></script>
>```
>
>![mark](http://qiniu.wind-zhou.com/blog/201207/95kgje4Fh2.png?imageslim)

### while循环

####while

while循环 直到型循环，直到条件为false退出

语法

```js
var 循环变量初始化；
while（条件）{
    语句1；
    语句2；
    ....;
    循环变量变化；
}
```

例：用while循环，计算1-100的和

```js
<script>
    var i = 0;
    var sum = 0;
    while (i <= 100) {
        sum += i;
        i++;
    }
    document.write(sum)
</script>
```

```js
输出：5050
```

#### do-while

语法

```js
do{
    语句;
    语句;
    ...；
    增量
}while(条件)；
```

**循环体至少执行一次。**

### break和continue

break 跳出循环

continue 结束本次循环，开始下一次循

例：

1、输出100个7的倍数

```js
<script>
    var count = 0;
    for (var i = 1; i >= 1; i++) {
        if (i % 7 == 0) {
            document.write(i + "<br>");
            count++;
            if (count == 100) {
                break
            }
        }
    }
</script>
```

```js
输出：
7
14
21
28
35
42
49
56
63
.....
```

2、输出10以内的奇数

```js
<script>
    for (var i = 0; i <= 10; i++) {
        if (i % 2 == 0) {
            continue;
        }
        document.write(i)
    }
</script>
```

```js
输出：
13579
```





