# lesson-20 面向对象--封装

## 面向对象与面向过程

###前言:

如果你很想搞明白面向对象是什么，面向过程是什么，或者说二者之间的区别是什么，那么就花费一点时间来研读一下这篇博客，你一定会有很大的收获的！

###一、面向对象与面向过程的区别

**面向过程**就是分析出解决问题所需要的步骤，然后用函数把这些步骤一步一步实现，使用的时候一个一个依次调用就可以了；**面向对象是把构成问题事务分解成各个对象**，**建立对象的目的不是为了完成一个步骤，而是为了描叙某个事物在整个解决问题的步骤中的行为。**

可以拿生活中的实例来理解面向过程与面向对象，例如五子棋，面向过程的设计思路就是首先分析问题的步骤：**1、开始游戏，2、黑子先走，3、绘制画面，4、判断输赢，5、轮到白子，6、绘制画面，7、判断输赢，8、返回步骤2，9、输出最后结果**。把上面每个步骤用不同的方法来实现。

如果是面向对象的设计思想来解决问题。面向对象的设计则是从另外的思路来解决问题。整个五子棋可以分为1、**黑白双方**，这两方的行为是一模一样的，2、**棋盘系统**，负责绘制画面，3、**规则系统**，负责判定诸如犯规、输赢等。第一类对象（玩家对象）负责接受用户输入，并告知第二类对象（棋盘对象）棋子布局的变化，棋盘对象接收到了棋子的变化就要负责在屏幕上面显示出这种变化，同时利用第三类对象（规则系统）来对棋局进行判定。

可以明显地看出，**面向对象是以功能来划分问题**，**而不是步骤**。同样是绘制棋局，这样的行为在面向过程的设计中分散在了多个步骤中，很可能出现不同的绘制版本，因为通常设计人员会考虑到实际情况进行各种各样的简化。而面向对象的设计中，绘图只可能在棋盘对象中出现，从而保证了绘图的统一。

上述的内容是从网上查到的，觉得这个例子非常的生动形象，我就写了下来，现在就应该理解了他俩的区别了吧，其实就是两句话，面向对象就是高度实物抽象化、面向过程就是自顶向下的编程！

###二、面向对象的特点

在了解其特点之前，咱们先谈谈对象，对象就是现实世界存在的任何事务都可以称之为对象，有着自己独特的个性

![mark](http://qiniu.wind-zhou.com/blog/210315/5aHB45Cbd0.png?imageslim)



**封装：**

封**装从字面上来理解就是包装的意思，专业点就是信息隐藏，**是指利用抽象数据类型将数据和基于数据的操作封装在一起，使其构成一个不可分割的独立实体，数据被保护在抽象数据类型的内部，尽可能地隐藏内部的细节，只保留一些对外接口使之与外部发生联系。系统的其他对象只能通过包裹在数据外面的已经授权的操作来与这个封装的对象进行交流和交互。也就是说用户是无需知道对象内部的细节，但可以通过该对象对外的提供的接口来访问该对象。

对于封装而言，**一个对象它所封装的是自己的属性和方法**，所以它是不需要依赖其他对象就可以完成自己的操作。使用封装有三大好处：



> 1、良好的封装能够减少耦合。
>
> 2、类内部的结构可以自由修改。
>
>
> 3、可以对成员进行更精确的控制。
>
> 4、隐藏信息，实现细节。



**继承：**

  继承是使用已存在的类的定义作为基础建立新类的技术，新类的定义可以增加新的数据或新的功能，也可以用父类的功能，但不能选择性地继承父类。通过使用继承我们能够非常方便地复用以前的代码，能够大大的提高开发的效率。

**多态：**

 **多态是同一个行为具有多个不同表现形式或形态的能力。**

所谓多态就是指程序中定义的引用变量所指向的具体类型和通过该引用变量发出的方法调用在编程时并不确定，而是在程序运行期间才确定，即一个引用变量倒底会指向哪个类的实例对象，该引用变量发出的方法调用到底是哪个类中实现的方法，必须在由程序运行期间才能决定。因为在程序运行时才确定具体的类，这样，不用修改源程序代码，就可以让引用变量绑定到各种不同的类实现上，从而导致该引用调用的具体方法随之改变，即不修改程序代码就可以改变程序运行时所绑定的具体代码，让程序可以选择多个运行状态，这就是多态性。




**属性**用来描述具体某个对象的特征。比如小志身高180M，体重70KG，这里身高、体重都是属性。
面向对象的思想就是把一切都看成对象，而对象一般都由属性+方法组成！

属性属于对象静态的一面，用来形容对象的一些特性，方法属于对象动态的一面，咱们举一个例子，小明会跑，会说话，跑、说话这些行为就是对象的方法！所以为动态的一面， 我们把属性和方法称为这个对象的成员！

**类**：具有同种属性的对象称为类，是个抽象的概念。比如“人”就是一类，期中有一些人名，比如小明、小红、小玲等等这些都是对象，类就相当于一个模具，他定义了它所包含的全体对象的公共特征和功能，对象就是类的一个实例化，小明就是人的一个实例化！我们在做程序的时候，经常要将一个变量实例化，就是这个原理！我们一般在做程序的时候一般都不用类名的，比如我们在叫小明的时候，不会喊“人，你干嘛呢！”而是说的是“小明，你在干嘛呢！”

面向对象有三大特性，分别是封装性、继承性和多态性，这里小编不给予太多的解释，因为在后边的博客会专门总结的！

###三、面向过程与面向对象的优缺点
很多资料上全都是一群很难理解的理论知识，整的小编头都大了，后来发现了一个比较好的文章，写的真是太棒了，通俗易懂，想要不明白都难!

用面向过程的方法写出来的程序是一份蛋炒饭，而用面向对象写出来的程序是一份盖浇饭。所谓盖浇饭，北京叫盖饭，东北叫烩饭，广东叫碟头饭，就是在一碗白米饭上面浇上一份盖菜，你喜欢什么菜，你就浇上什么菜。我觉得这个比喻还是比较贴切的。

蛋炒饭制作的细节，我不太清楚，因为我没当过厨师，也不会做饭，但最后的一道工序肯定是把米饭和鸡蛋混在一起炒匀。盖浇饭呢，则是把米饭和盖菜分别做好，你如果要一份红烧肉盖饭呢，就给你浇一份红烧肉；如果要一份青椒土豆盖浇饭，就给浇一份青椒土豆丝。

蛋炒饭的好处就是入味均匀，吃起来香。如果恰巧你不爱吃鸡蛋，只爱吃青菜的话，那么唯一的办法就是全部倒掉，重新做一份青菜炒饭了。盖浇饭就没这么多麻烦，你只需要把上面的盖菜拨掉，更换一份盖菜就可以了。盖浇饭的缺点是入味不均，可能没有蛋炒饭那么香。

到底是蛋炒饭好还是盖浇饭好呢？其实这类问题都很难回答，非要比个上下高低的话，就必须设定一个场景，否则只能说是各有所长。如果大家都不是美食家，没那么多讲究，那么从饭馆角度来讲的话，做盖浇饭显然比蛋炒饭更有优势，他可以组合出来任意多的组合，而且不会浪费。

盖浇饭的好处就是"菜"“饭"分离，从而提高了制作盖浇饭的灵活性。饭不满意就换饭，菜不满意换菜。用软件工程的专业术语就是"可维护性"比较好，“饭” 和"菜"的耦合度比较低。蛋炒饭将"蛋”“饭"搅和在一起，想换"蛋”"饭"中任何一种都很困难，**耦合度很高，以至于"可维护性"比较差**。软件工程追求的目标之一就是可维护性，可维护性主要表现在3个方面：**可理解性、可测试性和可修改性**。**面向对象的好处之一就是显著的改善了软件系统的可维护性。**
　　
看了这篇文章，简单的总结一下!

**面向过程**

> 优点：性能比面向对象高，因为类调用时需要实例化，开销比较大，比较消耗资源;比如单片机、嵌入式开发、 Linux/Unix等一般采用面向过程开发，性能是最重要的因素。
> 缺点：没有面向对象易维护、易复用、易扩展

**面向对象**

> 优点：易维护、易复用、易扩展，由于面向对象有封装、继承、多态性的特性，可以设计出低耦合的系统，使系统 更加灵活、更加易于维护
> 缺点：性能比面向过程低



> ————————————————
> 版权声明：本文为CSDN博主「光哥_帅」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
> 原文链接：https://blog.csdn.net/jerry11112/article/details/79027834

## 类与对象的关系

- 类(class)一个共享相同结构和行为的对象的集合。

- 类(Class) 定义了一件事物的抽象特点。通常来说，类定义了事物的属性和它可以做到的(它的行
  为)。举例来说，“狗"这个类会包含狗的一切基础特征，例如它的孕育、毛皮颜色和吠叫的能力。类
  可以为程序提供模版和结构。一个类的方法和属性被称为“成员"。

- **类是对象的抽象，而对象是类的具体事例**。类是抽象的，不占内存的，而对象是具体的占用存储空间
  的，类是用于创建对象的蓝图模板。
- 在面向对象编程语言当中，定义个类，使用class类名{}来定义
- 但是javascript是基于对象和事件驱动的脚本语言，他不是面向对象的编程语言，所有在javascript中
  没有类的概念，但是使用javascript可以模拟面向对象编程当中的类的概念

## js创建对象的方法

### 原始模式

#### 使用Object构造函数

**语法**：`var 对象名=new Object();`

**示例**：

```js
 <script>
        var obj = new Object(); //使用一个Object类实例化一个对象
        console.log(obj)

        obj.name = "zhouzheng";
        obj["age"] = "24"
        console.log(obj)


        var obj2 = new Object();

        obj2.name = "wind";
        obj2["age"] = "30"
        console.log(obj2)
    </script>
```

**输出**：

![mark](http://qiniu.wind-zhou.com/blog/210316/3E8hcdekA3.png?imageslim)



#### 字面量方式

就是使用json对象的方式，一种简写方式。

**语法**：`var person={"name":"zhou","age":24}`

**示例**：

```js

    <script>
        var person = { //使用字面量定义对象
            name: "zhouzheng",
            age: "24",
            hobby: "study",
            sayName: function() {
                console.log("I am " + this.name)

            }
        }

        console.log("年龄：" + person.name) //调用属性
        person.sayName(); //调用方法
    </script>
```



**输出：**

![mark](http://qiniu.wind-zhou.com/blog/210316/J1H7L9k81g.png?imageslim)





**关于一些优化：**

当多个对象有共同的方法时，可以将方法在对象外单独封装成一个函数，这样可以节省内存，因为如果不这样，每个对象

实例化时都会单独开辟这个方法的内存，造成浪费。



见下面例子：

(1)当单独在两个对象中都定义sayName方法时，让我们看一下他们的方法是否指向了同一个函数。



```js
    <script>
        var person = { //使用字面量定义对象
            name: "zhouzheng",
            age: "24",
            hobby: "study",
            sayName: function() {
                console.log("I am " + this.name)
            }
        }

        var dog = {
            name:"小黑",
            height: "20cm",
            color: "black",
            sayName: function() {
                console.log("I am " + this.name)
            }
        }
        person.sayName(); //调用方法
        dog.sayName()
        console.log(person.sayName == dog.sayName) //判断两个的方法是否指向同一个函数
    </script>
```



![mark](http://qiniu.wind-zhou.com/blog/210316/ghid9d9Cf8.png?imageslim)

输出为false，可见他们在不同的内存区域。



(2)将相同的方法拿到对象外单独定义



```js

    <script>
        function sayName() {
            console.log("I am " + this.name)
        }

        var person = { //使用字面量定义对象
            name: "zhouzheng",
            age: "24",
            hobby: "study",
            sayName: sayName
        }

        var dog = {
            height: "20cm",
            color: "black",
            sayName: sayName
        }

        console.log("年龄：" + person.name) //调用属性
        person.sayName(); //调用方法
        console.log(person.sayName == dog.sayName) //判断两个的方法是否指向同一个函数
    </script>
```

输出：![mark](http://qiniu.wind-zhou.com/blog/210316/6EAGklG6J5.png?imageslim)



可见，输出为true，两个确实指向了同一函数。

### 工厂模式

使用原始模式创建对象会存在一个问题，就是效率太低，每个对象的创建都需要重复的操作，因此为了提高创建对象的效率，出现了所谓的**工厂模式**。

顾名思义，就是通过一个工厂（**函数**），来批量的创建相同的对象。

**语法：**

```js

//创建工厂函数
function 函数名(参数1，参数2){
    
    var  对象名=new Object();
    对象名.属性名=参数1;
     对象名.属性名=参数2;
     对象名.方法名=fun();
    return 对象名；
}

//使用工厂函数创建对象

var 对象名=函数名(参数1,参数2);

//调用方法

对象名.方法名();

```

**示例：**



```js
<script>
    function person(name, age) { //创建工厂

        var ps = new Object();
        ps.name = name;
        ps.age = age;
        ps.sayName = function() {
            console.log("hello " + ps.name)
        }

        return ps;

    }

    var ps1 = person("zhouzheng", 24);
    var ps2 = person("trump", "70");
    console.log(ps1, ps2) //输出两个对象
    ps1.sayName();
    ps2.sayName();
</script>
```



![mark](http://qiniu.wind-zhou.com/blog/210316/g2eDChC9AK.png?imageslim)



**一些优化：**

和前面一样我们同样看一下两个对象的方法是不是同一个函数。

```js
<script>
    function person(name, age) { //创建工厂

        var ps = new Object();
        ps.name = name;
        ps.age = age;
        ps.sayName = function() {
            console.log("hello " + ps.name)
        }
        return ps;
    }

    var ps1 = person("zhouzheng", 24);
    var ps2 = person("trump", "70");

    console.log(ps1.sayName == ps2.sayName)
</script>
```

输出：

![mark](http://qiniu.wind-zhou.com/blog/210316/GfG2dFDJ6B.png?imageslim)



可见，存在和之前一样的问题，现在使用之前相同的方法对其进行优化。

```js
<script>
    function sayName() {
        console.log("hello " + this.name)
    }

    function person(name, age) { //创建工厂

        var ps = new Object();
        ps.name = name;
        ps.age = age;
        ps.sayName = sayName;

        return ps;

    }

    var ps1 = person("zhouzheng", 24);
    var ps2 = person("trump", "70");

    console.log(ps1.sayName == ps2.sayName)
</script>
```

此时输出：

![mark](http://qiniu.wind-zhou.com/blog/210316/d2ddcbAm4c.png?imageslim)

优化成功。



### 构造函数模式

使用工厂模式确实简化了对象的创建，但还遗留了一个问题：**对象的识别**。就是不知道一个对象的类型，因为使用工厂模式示例的对象类型全都是Object，不像Data，Array。



**构造函数语法：**



```js
//创建构造函数

function 函数名(参数1,参数2){
    this.属性名=参数1；
    this.属性名=参数2;
    this.方法名=fn();
}

//使用构造函数实例化

var 对象名=new 函数名(实参1,实参2);

//调用方法

对象名 .方法名();

```

**示例：**

```js
function Person(name, age) {  //创建构造哈数

    this.name = name;
    this.age = age;
    this.sayName = function() {
        console.log(this.name)
    }
}

var people1 = new Person("zhozuheng", 24);  //使用new实例化对象
console.log(people1 instanceof Object) //true  //object是个跟对象
console.log(people1 instanceof Person) //判断对象是否为person类型    //true
people1.sayName();  //调用方法   //zhouzheng
```



构造函数也有上述的内存优化的问题，解决方法也相同。



**几点注意：**

- 构造函数就是普通的函数，创建和普通函数没有区别，构造函数和普通函数的区别在于调用方式的不同，

  **普通函数直接调用**，构造函数需要使用new关键字来调用。

- 构造函数可以创建一类对象，构造函数可以看做一个类。



**构造函数和工厂模式的区别：**

1. 没有显式的创建对象
2. 直接将属性和方法赋值给this对象
3. 没有return语句



**构造函数的执行流程：**

1. 立刻创建一个对象
2. 将新创建的对象设置为函数中的this
3. 逐行执行函数中的代码
4. 将新创建的对昂作为返回值返回



![mark](http://qiniu.wind-zhou.com/blog/210315/BD8jC6JiHJ.png?imageslim)



### 原型模式

> #一、什么是原型
>
> 原型是Javascript中的继承的基础，JavaScript的继承就是基于原型的继承。
>
> ##1.1 函数的原型对象
>
> 在JavaScript中，我们创建一个函数A(就是声明一个函数), 那么浏览器就会在内存中创建一个对象B，而且每个函数都默认会有一个属性 prototype 指向了这个对象( 即：prototype的属性的值是这个对象 )。这个对象B就是函数A的原型对象，简称函数的原型。这个原型对象B 默认会有一个属性 constructor 指向了这个函数A ( 意思就是说：constructor属性的值是函数A )。
>
> ```js
> <body>
> <script type="text/javascript">
> 	/*
> 		声明一个函数，则这个函数默认会有一个属性叫 prototype 。而且浏览器会自动按照一定的规则
> 		创建一个对象，这个对象就是这个函数的原型对象，prototype属性指向这个原型对象。这个原型对象
> 		有一个属性叫constructor 执行了这个函数
> 
> 			注意：原型对象默认只有属性：constructor。其他都是从Object继承而来，暂且不用考虑。
> 		*/
> 	    function Person () {
> 
> 	    }	    
> </script>
> </body>
> 
> ```
>
> >下面的图描述了声明一个函数之后发生的事情：
>
> ![mark](http://qiniu.wind-zhou.com/blog/210316/BIC0DI2L4l.png?imageslim)
>
> ##1.2 使用构造函数创建对象
> 当把一个函数作为构造函数 (理论上任何函数都可以作为构造函数) 使用new创建对象的时候，那么这个对象就会存在一个默认的不可见的属性，来指向了构造函数的原型对象。 这个不可见的属性我们一般用 [[prototype]] 来表示，只是这个属性没有办法直接访问到。
>
> 看下面的代码：
>
> ```js
> <body>
> <script type="text/javascript">
> 	    function Person () {
> 
> 	    }	
> /*
> 	利用构造函数创建一个对象，则这个对象会自动添加一个不可见的属性 [[prototype]], 而且这个属性
> 	指向了构造函数的原型对象。
> */
> 	var p1 = new Person();
> </script>
> </body>
> 
> ```
>
> >观察下面的示意图：
>
> ![mark](http://qiniu.wind-zhou.com/blog/210316/K0EhH2Jiaa.png?imageslim)
>
> > 说明：
>
> 从上面的图示中可以看到，创建p1对象虽然使用的是Person构造函数，但是对象创建出来之后，这个p1对象其实已经与Person构造函数没有任何关系了，p1对象的[[ prototype ]]属性指向的是Person构造函数的原型对象。
> 如果使用new Person()创建多个对象，则多个对象都会同时指向Person构造函数的原型对象。
> **我们可以手动给这个原型对象添加属性和方法，那么p1,p2,p3…这些对象就会共享这些在原型中添加的属性和方法。**
> 如果我们访问p1中的一个属性name，如果在p1对象中找到，则直接返回。如果p1对象中没有找到，则直接去p1对象的[[prototype]]属性指向的原型对象中查找，如果查找到则返回。(如果原型中也没有找到，则继续向上找原型的原型—原型链。 后面再讲)。
> 如果通过p1对象添加了一个属性name，则p1对象来说就屏蔽了原型中的属性name。 换句话说：在p1中就没有办法访问到原型的属性name了。
> 通过p1对象只能读取原型中的属性name的值，而不能修改原型中的属性name的值。 p1.name = “李四”; 并不是修改了原型中的值，而是在p1对象中给添加了一个属性name。
>
> > 看下面的代码：
>
> ```js
> <body>
>     <script type="text/javascript">
> 	    function Person () {    	
> 	    }
>       	// 可以使用Person.prototype 直接访问到原型对象
> 	    //给Person函数的原型对象中添加一个属性 name并且值是 "张三"
> 	    Person.prototype.name = "张三";
> 	    Person.prototype.age = 20;
> 
> 	   	var p1 = new Person();
> 	   	/*
> 	   		访问p1对象的属性name，虽然在p1对象中我们并没有明确的添加属性name，但是
> 	   		p1的 [[prototype]] 属性指向的原型中有name属性，所以这个地方可以访问到属性name
> 	   		就值。
> 	   		注意：这个时候不能通过p1对象删除name属性，因为只能删除在p1中删除的对象。
> 	   	*/
> 	   	alert(p1.name);  // 张三
> 
> 	   	var p2 = new Person();
> 	   	alert(p2.name);  // 张三  都是从原型中找到的，所以一样。
> 
> 	   	alert(p1.name === p2.name);  // true
> 
> 	   	// 由于不能修改原型中的值，则这种方法就直接在p1中添加了一个新的属性name，然后在p1中无法再访问到
> 	   	//原型中的属性。
> 	   	p1.name = "李四";
> 	   	alert("p1：" + p1.name);
> 	   	// 由于p2中没有name属性，则对p2来说仍然是访问的原型中的属性。	
> 	   	alert("p2:" + p2.name);  // 张三  
>     </script>
> </body>
> 
> ```
>
> ![mark](http://qiniu.wind-zhou.com/blog/210316/41fmEA7B1h.png?imageslim)
>
> #二、与原型有关的几个属性和方法
> ##2.1 prototype属性
>  prototype 存在于构造函数中 (其实任意函数中都有，只是不是构造函数的时候prototype我们不关注而已) ，他指向了这个构造函数的原型对象。
>
>  参考前面的示意图。
>
> ##2.2 constructor属性
>  constructor属性存在于原型对象中，他指向了构造函数
>
> 看下面的代码：
>
> ```js
> <script type="text/javascript">
> 	function Person () {
> 	}
> 	alert(Person.prototype.constructor === Person);	// true
> 	var p1 = new Person();
>   	//使用instanceof 操作符可以判断一个对象的类型。  
>   	//typeof一般用来获取简单类型和函数。而引用类型一般使用instanceof，因为引用类型用typeof 总是返回object。
> 	alert(p1 instanceof Person);	// true
> </script>
> 
> ```
>
> 
>
> >我们根据需要，可以Person.prototype 属性指定新的对象，来作为Person的原型对象。
> >
> >但是这个时候有个问题，新的对象的constructor属性则不再指向Person构造函数了。
>
> 看下面的代码：
>
> ```js
> <script type="text/javascript">
> 	function Person () {
> 
> 	}
> 	//直接给Person的原型指定对象字面量。则这个对象的constructor属性不再指向Person函数
> 	Person.prototype = {
> 		name:"志玲",
> 		age:20
> 	};
> 	var p1 = new Person();
> 	alert(p1.name);  // 志玲
> 
> 	alert(p1 instanceof Person); // true
> 	alert(Person.prototype.constructor === Person); //false
>   	//如果constructor对你很重要，你应该在Person.prototype中添加一行这样的代码：
>   	/*
>   	Person.prototype = {
>       	constructor : Person	//让constructor重新指向Person函数
>   	}
>   	*/
> </script>
> 
> ```
>
> ##2.3` _ _proto_ _ `属性(注意：左右各是2个下划线)
>
>  用构造方法创建一个新的对象之后，这个对象中默认会有一个不可访问的属性 [[prototype]] , 这个属性就指向了构造方法的原型对象。
>
>  但是在个别浏览器中，也提供了对这个属性[[prototype]]的访问(chrome浏览器和火狐浏览器。ie浏览器不支持)。访问方式：p1.__proto__
>
> ```js
> <script type="text/javascript">
> 	function Person () {
> 
> 	}
> 	//直接给Person的原型指定对象字面量。则这个对象的constructor属性不再指向Person函数
> 	Person.prototype = {
> 		constructor : Person,
> 		name:"志玲",
> 		age:20
> 	};
> 	var p1 = new Person();
> 
> 	alert(p1.__proto__ === Person.prototype);	//true
> 
> </script>
> 
> ```
>
> ##2.4 hasOwnProperty() 方法
>  大家知道，我们用去访问一个对象的属性的时候，这个属性既有可能来自对象本身，也有可能来自这个对象的[[prototype]]属性指向的原型。
>
>  那么如何判断这个对象的来源呢？
>
>  hasOwnProperty方法，可以判断一个属性是否来自对象本身。
>
> ```js
> <script type="text/javascript">
> 	function Person () {
> 
> 	}
> 	Person.prototype.name = "志玲";
> 	var p1 = new Person();
> 	p1.sex = "女";
>   	//sex属性是直接在p1属性中添加，所以是true
> 	alert("sex属性是对象本身的：" + p1.hasOwnProperty("sex"));
>   	// name属性是在原型中添加的，所以是false
> 	alert("name属性是对象本身的：" + p1.hasOwnProperty("name"));
>   	//  age 属性不存在，所以也是false
> 	alert("age属性是存在于对象本身：" + p1.hasOwnProperty("age"));
> 
> </script>
> 
> ```
>
> >所以，**通过hasOwnProperty这个方法可以判断一个对象是否在对象本身添加的**，但是不能判断是否存在于原型中，因为有可能这个属性不存在。
> >
> >**也即是说，在原型中的属性和不存在的属性都会返回fasle。**
> >
> >如何判断一个属性是否存在于原型中呢？
>
> ## 2.5 in 操作符
>
>  **in操作符用来判断一个属性是否存在于这个对象中**。但是在查找这个属性时候，现在对象本身中找，如果对象找不到再去原型中找。换句话说，只要对象和原型中有一个地方存在这个属性，就返回true
>
> > 回到前面的问题，如果判断一个属性是否存在于原型中：
> >
> > **如果一个属性存在，但是没有在对象本身中，则一定存在于原型中。**
>
> ```js
> <script type="text/javascript">
> 	function Person () {
> 	}
> 	Person.prototype.name = "志玲";
> 	var p1 = new Person();
> 	p1.sex = "女";
> 
> 	//定义一个函数去判断原型所在的位置
> 	function propertyLocation(obj, prop){
> 		if(!(prop in obj)){
> 			alert(prop + "属性不存在");
> 		}else if(obj.hasOwnProperty(prop)){
> 			alert(prop + "属性存在于对象中");
> 		}else {
> 			alert(prop + "对象存在于原型中");
> 		}
> 	}
> 	propertyLocation(p1, "age");
> 	propertyLocation(p1, "name");
> 	propertyLocation(p1, "sex");
> </script
> 
> ```
>
> #三、组合原型模型和构造函数模型创建对象
>
> ##3.1 原型模型创建对象的缺陷
>
>  原型中的所有的属性都是共享的。也就是说，用同一个构造函数创建的对象去访问原型中的属性的时候，大家都是访问的同一个对象，如果一个对象对原型的属性进行了修改，则会反映到所有的对象上面。
>
>  但是在实际使用中，每个对象的属性一般是不同的。张三的姓名是张三，李四的姓名是李四。
>
>  **但是，这个共享特性对 方法(属性值是函数的属性)又是非常合适的。**所有的对象共享方法是最佳状态。这种特性在c#和Java中是天生存在的。
>
> ##3.2 构造函数模型创建对象的缺陷
>
>  在构造函数中添加的属性和方法，每个对象都有自己独有的一份，大家不会共享。这个特性对属性比较合适，但是对方法又不太合适。因为对所有对象来说，他们的方法应该是一份就够了，没有必要每人一份，造成内存的浪费和性能的低下。
>
> ```js
> <script type="text/javascript">
> 	function Person() {
> 	    this.name = "李四";
> 	    this.age = 20;
> 	    this.eat = function() {
> 	        alert("吃完东西");
> 	    }
> 	}
> 	var p1 = new Person();
> 	var p2 = new Person();
> 	//每个对象都会有不同的方法
> 	alert(p1.eat === p2.eat); //fasle
> </script>
> 
> ```
>
> > 可以使用下面的方法解决：
>
> ```js
> <script type="text/javascript">
> 	function Person() {
> 	    this.name = "李四";
> 	    this.age = 20;
> 	    this.eat = eat;
> 	}
>   	function eat() {
> 	    alert("吃完东西");
>     }
> 	var p1 = new Person();
> 	var p2 = new Person();
> 	//因为eat属性都是赋值的同一个函数，所以是true
> 	alert(p1.eat === p2.eat); //true
> </script>
> 
> ```
>
> 
>
> >**但是上面的这种解决方法具有致命的缺陷：封装性太差。使用面向对象，目的之一就是封装代码**，这个时候为了性能又要把代码抽出对象之外，这是反人类的设计。
>
> ##3.3 使用组合模式解决上述两种缺陷
>
>  **原型模式适合封装方法，构造函数模式适合封装属性**，综合两种模式的优点就有了组合模式。
>
> ```js
> <script type="text/javascript">
> 	//在构造方法内部封装属性
> 	function Person(name, age) {
> 	    this.name = name;
> 	    this.age = age;
> 	}
> 	//在原型对象内封装方法
> 	Person.prototype.eat = function (food) {
> 		alert(this.name + "爱吃" + food);
> 	}
> 	Person.prototype.play = function (playName) {
> 		alert(this.name + "爱玩" + playName);
> 	}
> 
> 	var p1 = new Person("李四", 20);
> 	var p2 = new Person("张三", 30);
> 	p1.eat("苹果");
> 	p2.eat("香蕉");
> 	p1.play("志玲");
> 	p2.play("凤姐");
> </script>
> 
> ```
>
> #四、动态原型模式创建对象
>
>  前面讲到的组合模式，也并非完美无缺，有一点也是感觉不是很完美。把构造方法和原型分开写，总让人感觉不舒服，应该想办法把构造方法和原型封装在一起，所以就有了动态原型模式。
>
>  动态原型模式把所有的属性和方法都封装在构造方法中，而仅仅在需要的时候才去在构造方法中初始化原型，又保持了同时使用构造函数和原型的优点。
>
> > 看下面的代码：
>
> ```js
> <script type="text/javascript">
> 	//构造方法内部封装属性
> 	function Person(name, age) {
> 		//每个对象都添加自己的属性
> 	    this.name = name;
> 	    this.age = age;
> 	    /*
> 	    	判断this.eat这个属性是不是function，如果不是function则证明是第一次创建对象，
> 	    	则把这个funcion添加到原型中。
> 	    	如果是function，则代表原型中已经有了这个方法，则不需要再添加。
> 	    	perfect！完美解决了性能和代码的封装问题。
> 	    */
> 	    if(typeof this.eat !== "function"){
> 	    	Person.prototype.eat = function () {
> 	    		alert(this.name + " 在吃");
> 	    	}
> 	    }
> 	}
> 	var p1 = new Person("志玲", 40);
> 	p1.eat();	
> </script>
> 
> ```
>
> > 说明：
>
> - 组合模式和动态原型模式是JavaScript中使用比较多的两种创建对象的方式。
> - 建议以后使用动态原型模式。他解决了组合模式的封装不彻底的缺点。
>
> 
>
> > ————————————————
> > 版权声明：本文为CSDN博主「做人要厚道2013」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
> > 原文链接：https://blog.csdn.net/u012468376/article/details/53121081



### 总结

**上面讲了几种js对象的创建模式，那么他们之间又有 怎样的联系和区别呢？**

- 首先**原始模式**是最基本的创建模式，但是他有固定的缺点，就是**实例化对象的效率太低**，每实例化一个对象都需要开发者手动的去输入属性和方法
- 由此诞生了**工厂模式**，工厂模式的设计目的是为了**提高对象实例化的效率**，每个工厂就是一个函数，里面封装了同一类对象的属性和方法，因此开发者在批量的实例化对象时，只需调用该函数，并传入对象的参数即可。但是工厂模式也有固定的缺陷，就是**对象类别的识别问题**，使用工厂模式创建的对象的种类都被笼统的规定为了Object，因此为了解决这个问题出现了构造函数模式
- **构造函数模式**可以创建不同类别的自定义的对象，例如Person类，Dog类，并且这些不同的可以被识别出来。
- 到了构造函数模式这，貌似目前的问题都被解决了，但是前面的几种方法都有一个固定的问题，就是同类对象里面的方法都仅属于当前被创建的对象，n个对象，里面的方法就会被创建n次，但是这些方法实现的功能相同，因此造成了**内存的浪费，**不过这种问题可以被解决，就是将相同的方法在外面定义，也就是声明称全局函数，这样每个对象里的方法只需要调用该方法即可，通过这种方式，相同的方法只开辟了一块内存空间，大大的节省了内存，但是（但是虽迟但到）又产生了新的问题，就是**全局变量的污染**，并且独立于构造函数之外定义方法也**不能很好的体现出oop的封装特性**，那么这个问题又该如何解决呢？请听下回。。。呸呸呸，就这次吧！接下来就到了我们的大名鼎鼎的原型模式。
- **原型模式**时利用函数对象内置的**prorotype对象**（原型对象）实现。这个东西厉害得很，他设计的目的是为了实现**继承**。他有一个很屌的性质，这个对象里可以存放一些属和方法，并且他里面的空间可以被子类共享并且不占内存。这就可以用来搞事情了，假入我们将构造函数（类）的方法在这个对象里定义，那么不就解决了前面的问题吗，首先封装性就不用说了，都定义在类内部了。当然符合了封装性，同时用户不占内存，那么内存浪费的问题也就迎刃而解了，到此，遇到的问题完美解决！



**关于原型对象：**

每个js函数都会js解释器内置一个属性就是**prototype**，他是函数对象里面的一个属性（key），他的值是指向了一个对象--**原型对象**，这个对象里存的是可以被**共享**（继承）的一些属性和方法。其中有一个固有属性是constructor，这个属性的值是该**构造函数本身**。

使用该构造函数实例化一个对象A时，A对象里会有一个默认的隐藏属性`_ _proto_ _`,这个属性也指向了原型对象。这个属性就将父类和子类构建了链接，举个例子，他爹有一笔遗产可以被继承，儿子想要继承的前提是他们要有关系，这个     `_ _proto_ _`就是起到了这么个作用。

原型对象里的属性和方法属于公共的属性和方法，他所有的子类都可以访问，假如要找一个子类的某个属性，首先从子类的对象里找，找不到则通过`_ _proto_ _`去父类的原型对象里去找。如果父类的原型对象里还没有则再次通过原型的`_ _proto_ _`去原型的原型去找（原型对象也是对象，因此也有`_ _proto_ _`），这样通过`_ _proto_ _`会构建一个**原型链**，那么问题来了，原型链有尽头吗？肯定是有的，要不然成无限套娃了。那么哪里是尽头呢？就是当找到头时，即最外层的父类，他的原型函数的`_ _proto_ _`指向了**Object**，这就是尽头，这个Object是js最基本的一个对象，里面有一些固有的属性和方法，这也是为什么任何的对象都有可以直接使用一些方法例如`in`,都是从老祖宗Object这继承过来的。

原型对象里的东西大家都可以访问和修改，**一般会把父类的属性在该构造函数里定义，公共的方法在原型对象里定义。**



![mark](http://qiniu.wind-zhou.com/blog/210316/cIffmAK7K8.png?imageslim)



![mark](http://qiniu.wind-zhou.com/blog/210315/JJ9474dA22.png?imageslim)





## 补充

### new关键字

**new的意义在于实现了JavaScript的继承。**

![时](http://qiniu.wind-zhou.com/blog/210316/kFi3AlkhjK.png?imageslim)





###this指向问题

> 指针有什么意义？
>
> 
>
> ## 什么是this
>
> this是一个指针
>
> ![mark](http://qiniu.wind-zhou.com/blog/210316/CBFlC9GkkJ.png?imageslim)
>
> 
>
> Arguements，参数对象，是一个数组（使用这个对象甚至函数声明时不用传形参）
>
> 
>
> ![mark](http://qiniu.wind-zhou.com/blog/210316/26m0JFb33D.png?imageslim)
>
> 
> 
>##**补充1：**
> 
>**this指针的指向问题：**
> 
>1、 当以函数的形式调用时，this是window
> 
>2、当以方法的形式调用时，谁调用this就是谁
> 
>3、当以构造函数形式调用时，this就是新创建的那个对象。
> 
>
> 
>**示例 ：**
> 
>```js
> <script>
> function a() {
>    console.log(this);
>    }
>  
> var obj = {
>    name: "zhouzheng",
>      age: 24,
>      fun: function() {
>          console.log(this)
>      }
>    }
>  
> function Dog(color, height) {
>    this.color = color;
>      this.height = height;
>      this.fun = function() {
>          console.log(this)
>      }
>    }
>  
> var dog1 = new Dog("黑色", "20cm");
>  
> 
> a();
>  obj.fun();
>  dog1.fun();
>  </script>
> ```
> 
>
> 
>![mark](http://qiniu.wind-zhou.com/blog/210316/i658Ced66E.png?imageslim)



### js检测对象类型的几种方法



>#js检测对象类型的几种方法：

>## 前言
>
>先说一下JavaScript中的数据类型有哪几类？
>主要分类两大类型，基本类型和引用类型。
>
>![clipboard.png](https://segmentfault.com/img/bVbsXYa?w=800&h=161)
>
>## 1.typeof
>
>先看一下用法：
>
>```js
>console.log(typeof "");
>console.log(typeof 1);
>console.log(typeof true);
>console.log(typeof null);
>console.log(typeof undefined);
>console.log(typeof []);
>console.log(typeof function(){});
>console.log(typeof {});
>```
>
>输出结果如下：
>
>> string
>> number
>> boolean
>> object
>> undefined
>> object
>> function
>> object
>
>### 小结
>
>**typeof可以用于检测基本类型，但碰到引用类型均返回为object。**
>
>## 2.instanceof
>
>看一下用法:
>
>```js
>console.log("1" instanceof String);
>console.log(1 instanceof Number);
>console.log(true instanceof Boolean);
>console.log([] instanceof Array);
>console.log(function(){} instanceof Function);
>console.log({} instanceof Object);
>```
>
>输出结果如下：
>
>> false
>> false
>> false
>> true
>> true
>> true
>
>### 小结
>
>不难看出，instanceof**可以用于引用类型的检测，**但对于基本类型是不生效的，另外，不能用于检测null和undefined。
>
>## 3.constructor
>
>对象的constructor属性用于返回创建该对象的函数，也就是我们常说的构造函数
>在js中，每个具有原型的对象都会自动获得constructor属性。
>
>先看一下用法：
>
>```js
>console.log(("1").constructor === String);
>console.log((1).constructor === Number);
>console.log((true).constructor === Boolean);
>console.log(([]).constructor === Array);
>console.log((function() {}).constructor === Function);
>console.log(({}).constructor === Object);
>```
>
>输出结果：
>
>> true
>> true
>> true
>> true
>> true
>> true
>
>撇去null和undefined，似乎说constructor能用于检测js的基本类型和引用类型。但当涉及到原型和继承的时候，便出现了问题，如下：
>
>```js
>function fun() {};
>
>fun.prototype = new Array();
>
>let f = new fun();
>
>console.log(f.constructor===fun);
>console.log(f.constructor===Array);
>```
>
>在这里，我们先是定义了一个函数fun，并将该函数的原型指向了数组，同时，声明了一个f为fun的类型，然后利用constructor进行检测时，结果如下：
>
>> false
>> true
>
>### 小结
>
>撇去null和undefined，constructor能用于检测js的基本类型和引用类型，但当对象的原型更改之后，constructor便失效了。
>
>## 4.Object.prototype.toString.call()
>
>用法：
>
>```js
>var test = Object.prototype.toString;
>
>console.log(test.call("str"));
>console.log(test.call(1));
>console.log(test.call(true));
>console.log(test.call(null));
>console.log(test.call(undefined));
>console.log(test.call([]));
>console.log(test.call(function() {}));
>console.log(test.call({}));
>```
>
>结果：
>
>> [object String]
>> [object Number]
>> [object Boolean]
>> [object Null]
>> [object Undefined]
>> [object Array]
>> [object Function]
>> [object Object]
>
>这样一看，似乎能满足js的所有数据类型，那我们看下继承之后是否能检测出来
>
>```js
>function fun() {};
>
>fun.prototype = new Array();
>
>let f = new fun();
>
>console.log(Object.prototype.toString.call(fun))
>console.log(Object.prototype.toString.call(f))
>```
>
>结果：
>
>> [object Function]
>> [object Object]
>
>### 小结
>
>可以看出，Object.prototype.toString.call()可用于检测js所有的数据类型。
>
>