# lesson-8 date对象

**date对象---日期对象**

date对象的方法主要有三大类：

- get系列
- set系列
- toString系列

## 创建日期对象

使用new来创建date对象

```js
var myDate=new Date();
```

**注释：**Date 对象会自动把**当前日期和时间**保存为其初始值。

## get系列方法

| 方法                                                         | 描述                                             |
| :----------------------------------------------------------- | ------------------------------------------------ |
| [getDate()](https://www.runoob.com/jsref/jsref-getdate.html)     日 | 从 Date 对象返回一个月中的某一天 (1 ~ 31)。      |
| [getDay()](https://www.runoob.com/jsref/jsref-getday.html)   星期 | 从 Date 对象返回一周中的某一天 (0 ~ 6)。         |
| [getMonth()](https://www.runoob.com/jsref/jsref-getmonth.html)     月 | 从 Date 对象返回月份 (0 ~ 11)。                  |
| [getFullYear()  ](https://www.runoob.com/jsref/jsref-getfullyear.html)     年 | 从 Date 对象以四位数字返回年份。                 |
| [getHours()](https://www.runoob.com/jsref/jsref-gethours.html)    时 | 返回 Date 对象的小时 (0 ~ 23)。                  |
| [getMinutes()](https://www.runoob.com/jsref/jsref-getminutes.html)  分 | 返回 Date 对象的分钟 (0 ~ 59)。                  |
| [getSeconds()](https://www.runoob.com/jsref/jsref-getseconds.html) | 返回 Date 对象的秒数 (0 ~ 59)。                  |
| [getMilliseconds()](https://www.runoob.com/jsref/jsref-getmilliseconds.html)   毫秒 | 返回 Date 对象的毫秒(0 ~ 999)。                  |
| [getTime()](https://www.runoob.com/jsref/jsref-gettime.html)   时间戳 | 返回 1970 年 1 月 1 日至今的毫秒数。**时间戳。** |
| [getTimezoneOffset()](https://www.runoob.com/jsref/jsref-gettimezoneoffset.html)   时间票差 | 返回本地时间与格林威治标准时间 (GMT) 的分钟差。  |

### getDate()

**作用**：从date对象中返回一个月的某一天

### getDay()

**作用**：获取星期几（0-6）

周日是0，

### getMonth()

**作用**：返回月份（0-11）

**所以要输出真实月份还要加1**

###   getfullYear()

**作用**：获取年份 （四位年份）

### getHours()

### getMinutes()

### getSeconds()

### getMilliseconds()

### 时间戳  getTime()

**作用：返回1970年1月1日至今的毫秒数**

```js
<script>
    var date = new Date(); //创建date对象
    var day = date.getDate(); //获取日
    var wday = date.getDay(); //获取星期
    var month = date.getMonth() + 1; //获取月份
    var year = date.getFullYear(); //获取年份

    var hours = date.getHours(); //获取 小时
    var minutes = date.getMinutes(); //获取 分钟
    var seconds = date.getSeconds(); //获取 秒
    var milliSeconds = date.getMilliseconds(); //获取 毫秒

    var timeOffset = date.getTimezoneOffset();  //返回本地时间与格林尼治时间的时间差
    var time = date.getTime(); //获取时间戳
    console.log("日:" + day)
    console.log("星期:" + wday)
    console.log("月:" + month)
    console.log("年:" + year)
    console.log("时:" + hours)
    console.log("分:" + minutes)
    console.log("秒:" + seconds)
    console.log("毫秒:" + milliSeconds)
    console.log("时间戳:" + time)
    console.log("时间差:" + timeOffset)
</script>
```

输出：

![mark](http://qiniu.wind-zhou.com/blog/201214/Dg7JCD8b38.png?imageslim)



##set系列方法

set系列方法和get系列使用方法相同，下面就不赘述了，常用的set系列的方法有下。

| 方法                                                         | 描述                                  |
| :----------------------------------------------------------- | ------------------------------------- |
| [setDate()](https://www.runoob.com/jsref/jsref-setdate.html) | 设置 Date 对象中月的某一天 (1 ~ 31)。 |
| [setFullYear()](https://www.runoob.com/jsref/jsref-setfullyear.html) | 设置 Date 对象中的年份（四位数字）。  |
| [setHours()](https://www.runoob.com/jsref/jsref-sethours.html) | 设置 Date 对象中的小时 (0 ~ 23)。     |
| [setMilliseconds()](https://www.runoob.com/jsref/jsref-setmilliseconds.html) | 设置 Date 对象中的毫秒 (0 ~ 999)。    |
| [setMinutes()](https://www.runoob.com/jsref/jsref-setminutes.html) | 设置 Date 对象中的分钟 (0 ~ 59)。     |
| [setMonth()](https://www.runoob.com/jsref/jsref-setmonth.html) | 设置 Date 对象中月份 (0 ~ 11)。       |
| [setSeconds()](https://www.runoob.com/jsref/jsref-setseconds.html) | 设置 Date 对象中的秒钟 (0 ~ 59)。     |
| [setTime()](https://www.runoob.com/jsref/jsref-settime.html) | setTime() 方法以毫秒设置 Date 对象。  |

## 转换（toString系列）

**日期---->字符串**

先看一下date对象的构成：

```js
date对象:  Mon Dec 14 2020 11:51:41 GMT+0800 (中国标准时间)
```

从前到后分别是：`星期 月 日 年 时 分 秒`

| 方法                                                         | 描述                                                   |
| :----------------------------------------------------------- | ------------------------------------------------------ |
| [toString()](https://www.runoob.com/jsref/jsref-tostring-date.html) | 把 Date 对象转换为字符串。                             |
| [toDateString()](https://www.runoob.com/jsref/jsref-todatestring.html) | 把 Date 对象的**日期部分**转换为字符串。               |
| [toTimeString()](https://www.runoob.com/jsref/jsref-totimestring.html) | 把 Date 对象的**时间部分**转换为字符串。               |
| [toUTCString()](https://www.runoob.com/jsref/jsref-toutcstring.html) | **根据世界时**，把 Date 对象转换为字符串。             |
| [toLocaleString()](https://www.runoob.com/jsref/jsref-tolocalestring.html) | **根据本地时间格式**，把 Date 对象转换为字符串。       |
| [toLocaleDateString()](https://www.runoob.com/jsref/jsref-tolocaledatestring.html) | 根据本地时间格式，把 Date 对象的日期部分转换为字符串。 |
| [toLocaleTimeString()](https://www.runoob.com/jsref/jsref-tolocaletimestring.html) | 根据本地时间格式，把 Date 对象的时间部分转换为字符串。 |
| toGMTString()                                                | 已废弃。请使用 toUTCString() 方法代替。                |
| [toISOString()](https://www.runoob.com/jsref/jsref-toisostring.html) | 使用 ISO 标准返回字符串的日期格式。                    |
| [toJSON()](https://www.runoob.com/jsref/jsref-tojson.html)   | 以 JSON 数据格式返回日期字符串。                       |
| [UTC()](https://www.runoob.com/jsref/jsref-utc.html)         | 根据世界时返回 1970 年 1 月 1 日 到指定日期的毫秒数。  |
| [valueOf()](https://www.runoob.com/jsref/jsref-valueof-date.html) | 返回 Date 对象的原始值。                               |

```js
<script>
    var date = new Date(); //创建date对象

    var toString = date.toString(); //直接转换成字符串

    var toDateString = date.toDateString(); //转换日期部分
    var toTimeString = date.toTimeString(); //转换时间部分

    var utcString = date.toUTCString(); //根据世界时间转换成字符串
    var localString = date.toLocaleString(); //根据本地时间转换成字符串

    var localTimeString = date.toLocaleTimeString(); //根据本地时间，转换时间部分为字符串
    var localDateString = date.toLocaleDateString(); //根据本地时间，转换时间部分为字符串

    console.log("date对象:\t\t" + date)
    console.log("toString:\t\t" + toString)
    console.log("date 日期部分:\t\t" + toDateString)
    console.log("date 时间部分:\t\t" + toTimeString)

    console.log("utc时间:\t\t" + utcString)
    console.log("本地时间:\t\t" + localString)

    console.log("本地日期时间部分:\t\t" + localDateString)
    console.log("本地时间时间部分:\t\t" + localTimeString)
</script>
```

![mark](http://qiniu.wind-zhou.com/blog/201214/EgJ1g5mdLh.png?imageslim)

注：虽然local的本地时间和默认的date里的日期一样，但是格式有些差异。



实战：写个计时器

```js
<body>
    <i id="time"></i>
</body>
<script>
    function time() {
        var date = new Date();
        var day4 = date.getHours() //或取小时
        var day5 = date.getMinutes() //或取分钟
        var day6 = date.getSeconds() //或取秒
        var day7 = date.getMilliseconds() //或取毫秒
        document.getElementById('time').
        innerHTML = day4 + ":" + day5 + ":" + day6 + ":" + day7
    }
    setInterval(time, 1)
</script>
```



> 补充：
>
> # GMT和UTC
>
> [GMT](http://baike.baidu.com/view/37429.htm)，即格林尼治标准时间，也就是世界时。GMT的正午是指当太阳横穿格林尼治子午线（本初子午线）时的时间。但由于地球自转不均匀不规则，导致GMT不精确，现在已经不再作为世界标准时间使用。
>
> [UTC](http://baike.baidu.com/link?url=WuopdxowYjyGEkfBMX2QFm5kbOBdSo-gvISUJ4Q23HZ3bbYQkWhoJH4FQZhZmN59w2J3lQUY0y6s5GjpdxraAa)，即协调世界时。UTC是以原子时秒长为基础，在时刻上尽量接近于GMT的一种时间计量系统。为确保UTC与GMT相差不会超过0.9秒，在有需要的情况下会在UTC内加上正或负闰秒。UTC现在作为世界标准时间使用。
>
> 所以，UTC与GMT基本上等同，误差不超过0.9秒。
>
> # 时区
>
> 地球自西向东旋转，东边比西边先看到太阳，东边的时间也比西边的早。为了统一世界的时间，1884年的国际经度会议规规定将全球划分为24个[时区](http://baike.baidu.com/link?url=xSAbnav5DTWqenBEcapIMazIz-b7AZh9_3JKW_ZVqEaVMTkkuKM2LwnANOqgg8gBxCdGrNjsYV0p5Uuqjit84q)（东、西各12个时区）。规定英国（格林尼治天文台旧址）为零时区（GMT+00），东1-12区，西1-12区，中国北京处于东8区（GMT+08）。
>
> 若英国时间为6点整，则GMT时间为6点整，则北京时间为14点整。
>
> # UNIX时间戳
>
> 计算机中的[UNIX时间戳](http://baike.baidu.com/view/821460.htm)，是以GMT/UTC时间「1970-01-01T00:00:00」为起点，到具体时间的秒数，不考虑闰秒。这么做当然是为了简化计算机对时间操作的复杂度。
>
> 比如我的电脑现在的系统时间为2015年2月27日15点43分0秒，因为我的电脑默认时区为东8区，则0时区的时间为2015年2月27日7点43分0秒，则UNIX时间戳为1425022980秒。
>
>  



