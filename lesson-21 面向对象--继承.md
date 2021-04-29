# lesson-21 面向对象--继承



## 原始对象继承

通过new关键字继承js原生构造函数Object的属性和方法

`var obj=new Object()`

## 原型链继承

**核心：将父类的示例作为子类的原型。**



```js
<script>
    function Father(name, age) { //父类构建函数
        this.name = name;
        this.age = age;
        this.run = function() {
            alert(this.name + "会跑")
        }
    }

    Father.prototype.fly = function() { //父类原型中添加方法
        alert(this.name + "会飞")
    }

    function Son(grade) { //子类的构造函数
        this.grade = grade;
    }


    Son.prototype = new Father("王富贵", "87"); //将子类原型指向父类的实例
    var son1 = new Son("3");
    console.log(son1)

    son1.fly(); //王富贵会飞
    son1.run(); //王富贵会跑  
    // 上面的run和fly方法一个在原型函数中定义，一个在构造函数中定义，都可以被访问到
</script>
```

这里分析一下son1的构成：

![mark](http://qiniu.wind-zhou.com/blog/210317/mla24FJEG0.png?imageslim)



**关于实例化子类后，修改属性和方法造成的影响：**



（1）实例化子类后，在对象中添加或修改属性和方法

​	实验证明：可以修改，**但是不影响父类中的属性**，只是添加了个属于自己的属性，在访问时也会被优先访问到。

```js

<script>
    function Father(name, age) { //父类构建函数
        this.name = name;
        this.age = age;
        this.run = function() {
            alert(this.name + "会跑")
        }

        Father.prototype.fly = function() { //父类原型中添加方法
            alert(this.name + "会飞")
        }
    }


    function Son(grade) { //子类的构造函数
        this.grade = grade;
    }


    Son.prototype = new Father("王富贵", "87"); //将子类原型指向父类的实例

    var son1 = new Son("3");

    son1.name = "trump";//自定义修改子类中的属性

    son1.fly(); //trump会飞

    console.log(son1)
</script>
```

![mark](http://qiniu.wind-zhou.com/blog/210317/3BkchFmIJf.png?imageslim)



（2）通过子类Son修改原型里的属性和方法



```js
  Son.prototype.name = "trump"
```

![mark](http://qiniu.wind-zhou.com/blog/210317/iE3HKI3bDF.png?imageslim)

(3)子类实例化后，通过实例化的对象son1添加方法



```js
    var son1 = new Son("3");

    son1.eat = function() { //在实例化子类后为期添加方法
        alert(this.name + "会吃饭")
    }
```

![mark](http://qiniu.wind-zhou.com/blog/210317/i9EEE57gKi.png?imageslim)

(4)子类实例化后，通过``__ __proto_ __ ``修改原型对象里的属性和方法



```js
   var son1 = new Son("3");

    son1.__proto__.eat = function() { //在实例化子类后为期添加方法
        alert(this.name + "会吃饭")
    }
    son1.__proto__.name = "trump";
```

<img src="http://qiniu.wind-zhou.com/blog/210317/618FeafkAi.png?imageslim" alt="mark" style="zoom:25%;" />



总结：确定继承关系后。可以通过子类的`prototype`修改原型对象中的参数和属性,也可以在实例化对象后通过

`__ __proto_ _`来修改原型对象的属性和方法。



**原型继承的优点：**

- 非常纯粹的继承关系,实例是子类的示例也是父亲的实例
- 父类新增的原型方法/原型属性，子类都可以访问到
- 简单，易于实现

**缺点：**

- 想要为子类新增方法和属性，必须在new Father()这样的语句后执行，不能放到构造器中
- **无法实现多继承**
- 来自原型对象的引用属性是所有实例共享的
- **创建子类时无法向父类构造函数传参**



为了解决原型中包含引用类型值带来的问题，可以使用构造函数继承的方式解决。



## 构造继承

**核心**：使用父类的构造函数来增强子类实例，等于是复制父类的实例属性给子类（没用到原型）



```js
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>构造继承</title>
</head>

<body>

</body>

<script>
    function ClassA(sColor) { //父类
        this.color = sColor;
        this.sayColor = function() {
            alert(this.color)
        }
    }

    function ClassB(bColor, name) { //子类

        this.newMethod = ClassA;

        this.newMethod(bColor); //通过子类的实例对象，调用父类的构造函数，改变this的指向（父类构造函数里的this）

        delete this.newMethod; //删除newMethod方法

        this.name = name;

        this.sayName = function() {

            alert(this.name)
        }
    }

    var b = new ClassB("red", "wind")

    console.log(b)
</script>

</html>
```





![mark](http://qiniu.wind-zhou.com/blog/210318/F0h1ACEHEa.png?imageslim)



构造函数可以实现多继承，并且可以传参。



构造继承最核心的是通过子类的方法调用父类的构造函数来改变this指针的指向。

那么到底是怎么改变的呢？

首先要知道构造函数里的里的this指向的是该构造函数实例化的对象，此题中的`this.newMethod`里的this指向的是对象b；然后，方法里的this指向的是调用该方法的对象，因此通过`this.newMethod(bColor); `这个方法调用时，ClassA里的this就指向了调用他的this，同时前面说了`this.newMethod(bColor)`这个this指向了b，因此构造函数ClassA里的this也就间接的指向了b，这时b便可以调用ClassA里的属性和方法，便实现了继承。



**可以用下面的图来表示**

![mark](http://qiniu.wind-zhou.com/blog/210318/cHC1bjha8H.png?imageslim)





**多继承：**

构造继承可以很简单的实现多继承。

看下面代码。

```js
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>构造继承</title>
</head>

<body>

</body>

<script>
    function ClassA(sColor) { //父类1
        this.color = sColor;
        this.sayColor = function() {
            alert(this.color)
        }
    }


    function ClassC(swim) { //父类2
        this.hobby = swim;
        this.sayHello = function() {
            alert(this.hobby)
        }
    }


    function ClassB(bColor, name, swim) { //子类

        this.newMethod1 = ClassA;
        this.newMethod2 = ClassC;



        this.newMethod1(bColor); //继承父类1
        this.newMethod2(swim); //继承父类2

        delete this.newMethod1; //删除newMethod方法
        delete this.newMethod2; //删除newMethod方法


        this.name = name;

        this.sayName = function() {

            alert(this.name)
        }
    }

    var b = new ClassB("red", "wind", "swim")

    console.log(b)
</script>

</html>
```





![mark](http://qiniu.wind-zhou.com/blog/210318/jkcK13c0H2.png?imageslim)





**思考：**

>**构造继承相比于原型继承的优点在哪里呢？**
>
>构造继承有一个很大的缺点就是子类通过原型继承父类后，因为共享一块空间，因此，子类若修改原型，则父类里面的东西也会被改变，这样就会导致，如果多个子类同时继承同一个父类，其中一个子类修改了父类，那么所有的子类继承的东西都会被改变。
>
>构造继承如何解决这个问题呢？构造函数通过改变this的指向是父类指向了子类，同时子类继承时，并不是继承了实例化后的父类，而是指向了构造函数，每个子类实例化时，再对父类进行实例化（同时父类的实例化可以在子类实例化时接收子类传入的参数），因此不存在改变父类的问题。也就是说，两个子类都通过构造继承继承了父类，其中一个子类在实例化对象son1后，又修改了父类，这样对其他子类是无影响的，因为他相当于只修改了自己实例化时的父类。
>
>**不影响其他，可传参。多继承。**
>
>**看下面的例子：**
>
>```js
><!DOCTYPE html>
><html lang="en">
>
><head>
>    <meta charset="UTF-8">
>    <meta name="viewport" content="width=device-width, initial-scale=1.0">
>    <meta http-equiv="X-UA-Compatible" content="ie=edge">
>    <title>构造继承</title>
></head>
>
><body>
>
></body>
>
><script>
>    function Father(sColor) { //父类1
>        this.color = sColor;
>        this.sayColor = function() {
>            alert(this.color)
>        }
>    }
>
>
>
>    function Son1(bColor, name) { //子类1
>
>        this.newMethod = Father;
>
>        this.newMethod(bColor); //继承父类
>
>        delete this.newMethod; //删除newMethod方法
>
>        this.name = name;
>
>        this.sayName = function() {
>
>            alert(this.name)
>        }
>    }
>
>    function Son2(bColor, height) { //子类2
>
>        this.newMethod = Father;
>
>        this.newMethod(bColor); //继承父类
>
>        delete this.newMethod; //删除newMethod方法
>
>        this.height = height;
>
>        this.sayHeight = function() {
>
>            alert(this.height)
>        }
>    }
>
>
>    var son1 = new Son1("red", "周正"); //实例化子类1
>    var son2 = new Son2("blue", "173cm"); //实例化子类2
>
>    son1.color = "yellow"; //子类1修改继承过来的属性
>
>
>    console.log(son1)
>    console.log(son2)
></script>
>
></html>
>```
>
>![mark](http://qiniu.wind-zhou.com/blog/210318/7Aa3IC9K2f.png?imageslim)
>
>上图可见，子类son1修改了name属性，但子类son2里的name并没有改变。
>
>



![mark](http://qiniu.wind-zhou.com/blog/210317/ihaBgHLkK6.png?imageslim)

## apply()和call()

apply和call实现继承还是通过改变this的指向，**本质属于构造继承的扩展**，**只是对其进行了封装**。

看下面代码：



```js
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>apply继承</title>
</head>

<body>

</body>

<script>
    function ClassA(sColor) { //父类
        this.color = sColor;
        this.sayColor = function() {
            alert(this.color)
        }
    }


    function ClassB(bColor, name) { //子类

        // this.newMethod = ClassA;

        // this.newMethod(bColor);

        // delete this.newMethod;

        ClassA.apply(this, [bColor]); //将classA的this替换成classB的this，正好classB的this指向的是b
        //实现原理就是前面的构造继承，相当于对前面构造函数的东西做了封装

        this.name = name;

        this.sayName = function() {

            alert(this.name)
        }
    }


    var b = new ClassB("red", "wind")

    console.log(b)
</script>

</html>
```



输出：![mark](http://qiniu.wind-zhou.com/blog/210318/AE2CebAIk1.png?imageslim)



![mark](http://qiniu.wind-zhou.com/blog/210317/0LEg89909h.png?imageslim)



apply和call方法实现了一样的功能，区别只在于传参的方法不同，call方法 需要传入的参数是一个队列，apply传入的参数是一个数组。



![mark](http://qiniu.wind-zhou.com/blog/210318/Ji6H2C3A7h.png?imageslim)





## 组合继承

概念：就是将原型链继承和构造函数继承结合到一起。

**思路是使用原型链实现对原型方法的继承，通过构造函数事件对示例属性的继承。**

这样可以使原型上定义的方法得到复用，又能保证每个实例都有自己的属性。



看下面的例子：

```js
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>apply继承</title>
</head>

<body>

</body>

<script>
    function Father(sColor) { //父类
        this.color = sColor;
    }


    Father.prototype.jump = function() { //在父类原型上定义方法
        alert(this.color + "会跳");
    }



    function Son(bColor, name) { //子类

        Father.apply(this, [bColor]); //将classA的this替换成classB的this，正好classB的this指向的是b
        //实现原理就是前面的构造继承，相当于对前面构造函数的东西做了封装

        this.name = name;
        this.sayName = function() {
            alert(this.name)
        }
    }

    Son.prototype = new Father("yellow"); //使用原型继承确定继承关系
    Son.prototype.constructor = Son; //修改子类原型函数里的constructor的指向 


    var b = new Son("red", "wind")
    b.jump()  //输出：red会飞
    console.log(b)
</script>

</html>
```





![mark](http://qiniu.wind-zhou.com/blog/210318/dffk7gLik8.png?imageslim)



组合继承的分析：

优点：

- 你补了构造继承的缺陷，可以继承示例的属性/方法，也可以继承原型的属性/方法
- 即是子类的实例，也是父类的实例
- 不存在信用属性共享问题
- 可传参
- 函数可复用

**缺点：无论什么情况下都调用两次父类型的构造函数，一次是创建子类原型的时候，一次是在子类型构造函数内部**



## 寄生式继承



![mark](http://qiniu.wind-zhou.com/blog/210317/03G1DCHKll.png?imageslim)



不能实现多继承。

##寄生组合继承

![mark](http://qiniu.wind-zhou.com/blog/210317/FkD7GlD2ml.png?imageslim)





![mark](http://qiniu.wind-zhou.com/blog/210317/jk4m8FfbaJ.png?imageslim)



问题：

- 寄生继承和原型链继承有什么本质的区别，感觉他们的作用只是原型链继承的一种改动，本质都是将子类的原型指向了父类的实例，只不过原型链继承是直接指向，寄生式继承是通过Object.creeat()方法实现
- 寄生继承是不在实例化父类，而是实例化了一个父类的副本（1、这样为什么可以是其不共享，2、为什么会减少一次创建？）
- 从构造继承过渡到组合寄生继承，到底优化了什么地方？优化了构造函数两次调用父类的构造函数，是减少了一次吗？为什么会减少？

**开销主要是来自属性实例化的开销**，由于把父类的原型给了空空对象的原型，此时空对象里是没有属性的，因此之后把空对象实例化后再赋值给子类的原型，这就省去了实例化时的开销，同时也避免了通过原型继承方法时也属性也继承的问题。

原型里的东西是不占内存的 。

使用object创建的对象没有constructor。

就是说，使用组合寄生的模式，优化了的地方有两点：1、是父类的构造函数少调用了一次，2、是父类的prototype里的东西和子类的prototype里的东西做了个隔离，这样子类修改prototype里的东西。父类prototype里的东西不发生改变



![mark](http://qiniu.wind-zhou.com/blog/210325/k86I8L1Dh0.png?imageslim)

那么是怎样实现的呢？  

https://www.jb51.net/article/132291.htm



https://zhuanlan.zhihu.com/p/110175302

https://segmentfault.com/a/1190000016708006



















































