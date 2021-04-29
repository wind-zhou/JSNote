# lesson-5 函数

## 内置对象

- array（数组）
- string（字符串对象）
- data（时间）
- MATH（数字）
- function（函数/方法）
- RegExp（正则表达式）
- Error（异常）

## 函数

### 自定义函数

函数是完成指定功能的程序段，可以反复调用，减少冗余。

语法

(1)函数定义/声明/创建

```js
function 函数名(形参，形参，....){
    语句；
    语句；
    ......；  
    return 表达式/值;
}
```

> ### 补充1：JavaScript的强制类型转换函数：
>
> JavaScript提供以下函数进行显式转换：
>
> **1.转换为数值类型**：Number(mix)、parseInt(string,radix)、parseFloat(string)
>
> **2.转换为字符串类型：**toString(radix)、String(mix)
>
> **3.转换为布尔类型**：Boolean(mix)
>
> ### 补充2  弱类型语言和强类型语言
>
> 一、强类型语言
>
> ​    **强类型语言是一种强制类型定义的语言，一旦某一个变量被定义类型，如果不经过强制转换，则它永远就是该数据类型了**，强类型语言包括Java、.net 、Python、C++等语言。
>
> ​    举个例子：定义了一个整数，如果不进行强制的类型转换，则不可以将该整数转化为字符串。
>
> 二、弱类型语言
>
> ​    弱类型语言是一种弱类型定义的语言，某一个变量被定义类型，**该变量可以根据环境变化自动进行转换，不需要经过显性强制转换**。弱类型语言包括vb 、PHP、javascript等语言。
>
> ​    举个例子：
>
> ```js
> var A =5;
> var B = "5";
> SumResult = A +B;
> MinResult = A -B；
> ```
>
> ​    输入SumResult的答案不是10，而是55，再次是将A的类型转化为了字符串，然后进行拼接。输入MinResult的答案是0，是将B的类型转化为了数字，然后进行减法。
>
> 三、强类型语言和弱类型语言区别
>
> ​    **无论是强类型语言还是弱类型语言，判别的根本是是否会隐性的进行语言类型转变**。强类型语言在速度上略逊于弱类型语言，但是强类型定义语言带来的严谨性又能避免不必要的错误。

### 带返回值函数

```js
<script>
    function sum(x, y) {
        var z = x + y;
        return z;
    }

    var num = sum(3, 5);
    alert(num)
</script>
```

程序遇到return，程序就会停下来。

写在函数最后一行。

### 匿名函数

匿名函数因为没有函数名，所以没办法像普通函数那样调用，所以**匿名函数需要保存到某个变量或者作为立即执行函数**

- 保存到变量中使用

  ```js
  <script>
      //1、将匿名函数付给一个变量
      document.getElementById("btn")
      var aaa = function(x, y) {
          var z = x + y;
          alert(z);
      }
      aaa(10, "a");
  </script>
  ```

  输出`10a`

- 立即执行

  ```js
  <script>
      //2、立即执行
      (function(x, y) {
          var z = x + y;
          alert(z);
      }(20, 10))
  </script>
  </html>
  ```

  输出：`30`

**匿名函数使用场景**

无法调用，一般用在**绑定事件**时和作为**回调函数**使用。

使用场景：

（1）绑定事件

（2）闭包函数

（3）回调函数

**匿名函数常用来实现闭包和回调函数。**



**回调函数：**

> 回调函数：把一个函数作为另一个函数的参数传入，并且在该函数中调用，被传入的函数称为回调函数。

例：使用回调函数实现一个加减功能。要求传入不同的函数，实现不同的运算。

```js
<script>
    function test(x, y, callback) {
        callback(x, y);
    }
//callback1 实现加运算
    var callback1 = function(x, y) {
        var z;
        z = x + y;
        alert(z);
    }
//callback2 实现减运算
    var callback2 = function(x, y) {
        var z;
        z = x - y;
        alert(z);
    }
    test(9, 5, callback2);
</script>
```



作用：打破了函数作用域的界限。

```js
<script>
    // 回调函数
    //定义函数 里面又有一个参数是函数
    function test(x, callback) {
        var y = 10;
        var z = x + y;
        callback(z)
    }
    //调用函数test，并传入两个参数（数值和函数）
    test(50, function(c) {
        alert(c)
    })
</script>
```

**闭包：**

**闭包函数可以通过回调函数实现。**但并不是所有使用回调函数的都是闭包。



例：闭包：

```js
<script>
    function box() {
        var a = 10;
        function inner() {
            return a;
        }
        return inner;
    }
    var outer = box();
    alert(outer())
</script>
```

> 闭包的作用：
>
> 闭包本身定义比较抽象，MDN官方上解释是：*A closure is the combination of a function and the lexical environment within which that function was declared.*
>  中文解释是：**闭包是一个函数和该函数被定义时的词法环境的组合。**
>  很多地方可以看到一个说法：js中每个函数都是一个闭包，这样理解也是没有问题的，不过会增加对闭包的理解难度，这里先不这么理解，可以按照闭包起的作用来理解它：
>
> **就是能在一个函数外部执行这个函数内部定义的方法，并访问这个函数内部定义的变量。**
>
> 参考链接：https://www.jianshu.com/p/0a3150afb7ed



**练习：实现一个计算器**

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
</head>
<!--  html 结构-->
<input type="text " id="num1" value="0">

<select name="" id="select">
    <option value="sum">+</option>
    <option value="reduce">-</option>
    <option value="mul">*</option>
    <option value="div">/</option>
</select>

<input type="text" id="num2" value="0"><button onclick="test()">=</button>
<input type="text" id="num" readonly value="0">

<body>

</body>

<script>
    function test() {
        //拿到select的值
        var symbol = document.getElementById("select").value;
        //根据输入的值，判断调用哪个函数
        switch (symbol) {
            case "sum":
                sum();
                break;
            case "reduce":
                reduce();
                break;
            case "mul":
                multiplication();
                break;
            case "div":
                division();
                break;
        }
        //定义加减乘除函数
        //加
        function sum() {
            var x = document.getElementById("num1").value;
            var y = document.getElementById("num2").value;
            document.getElementById("num").value = parseFloat(x) + parseFloat(y);
        }
        //减
        function reduce() {
            var x = document.getElementById("num1").value;
            var y = document.getElementById("num2").value;
            document.getElementById("num").value = parseFloat(x) - parseFloat(y);
            //注：这里要转换一下数据类型，因为input里的输入默认是string
        }
        //乘
        function multiplication() {
            var x = document.getElementById("num1").value;
            var y = document.getElementById("num2").value;
            document.getElementById("num").value = parseFloat(x) * parseFloat(y);
        }
        //除
        function division() {
            var x = document.getElementById("num1").value;
            var y = document.getElementById("num2").value;
            if (y == 0) {
                alert("输入错误")
            }
            document.getElementById("num").value = parseFloat(x) / parseFloat(y);
        }
    }
</script>
</html>
```

![mark](http://qiniu.wind-zhou.com/blog/201208/2Bhc0mbiEC.png?imageslim)

### 变量的作用域

#### 全局变量

函数外创建的变量，在当前程序段内都可以调用。

#### 局部变量

函数内创建的变量，只能在当前函数使用。

使用局部变量时，一定要在函数内使用**var**进行声明，否则就会变成全局变量。



js解释器碰到没使用var声明的变量时，会替程序去声明，但是在函数的外部声明，因此变成了全部变量。

## 内置函数

URL编码函数：encodeURI()   地址栏中的汉字会进行编码，以方便传输

URL解码函数：decodeURI()  

parseFloat()

parsrInt()

判断是否非数字：isNaN

eval()

