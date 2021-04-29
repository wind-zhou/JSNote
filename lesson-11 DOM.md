# lesson-11 DOM

## 浏览器架构

![mark](http://qiniu.wind-zhou.com/blog/201222/2DkB9b3dhI.png?imageslim)



## DOM概述

文档对象模型：当前载入页面所拥有的对象（代表当前文档）。（**w3c发布的标准**，不属于ecmascript）

## DOM树

![mark](http://qiniu.wind-zhou.com/blog/201222/0AjL2gLlbi.png?imageslim)



HTML里每个元素都是一个节点，DOM规定如下：

1. 整个文档是一个文档节点
2. 每个html标签是**元素节点**
3. html元素中的文本是**文本节点**
4. 每个html属性是一个**属性节点**
5. 注释属于注释节点



## Document 对象

每个载入页面的html都对转换为Document 对象

### document获取文档元素

**找节点，并且找到的是元素节点。**

#### 1、通过ID获取文档节点

``document.getElementById("id");``

**不能重复。**

```js
<body>
    <ul>
        <li id="one"></li>
        <li id="one"></li>
        <li id="one"></li>
        <li id="one"></li>
        <li id="one"></li>
    </ul>

</body>

<script>
    var contentById = document.getElementById("one");
    console.log(contentById);
    contentById.style.background = "pink";
</script>
```

![mark](http://qiniu.wind-zhou.com/blog/201222/kEFD3CjEkJ.png?imageslim)



**id只能使用一次，如果多个标签设置了一样的id，只返回第一个元素。**

#### 2、通过name获取文档节点集合

**会返回一个数组**

`document.getElementsByName(name);`

返回值得一个**类数组**。之所以称为类数组是因为他没有数组的一些方法。

**示例1：**

用for in遍历类数组

```js
<body>
    <ul>
        <li id="one"></li>
        <li name="zhou"></li>
        <li name="zhou"></li>
        <li name="zhou"></li>
        <li name="zhou"></li>
    </ul>
</body>

<script>
    var resultByName = document.getElementsByName("zhou");
    console.log(resultByName);
</script>
```

输出：返回一个类数组

![mark](http://qiniu.wind-zhou.com/blog/201222/aDmD3klKKf.png?imageslim)



**示例2：**

```js
<body>
    <ul>
        <li id="one"></li>
        <li name="zhou"></li>
        <li name="zhou"></li>
        <li name="zhou"></li>
        <li name="zhou"></li>
    </ul>

</body>
<script>
    var resultByName = document.getElementsByName("zhou");
    console.log(resultByName);
    for (var i = 0; i < resultByName.length; i++) {
        resultByName[i].style.background = "green";
    }
</script>
```

输出：

![mark](http://qiniu.wind-zhou.com/blog/201222/0i0Ee1LHEH.png?imageslim)



**注意：**得到结果可以用循环遍历，但不能用for in循环，因为for in是用来遍历对象的，用来遍历这种类数组次数会增多。

for in会遍历对象里的都有属性，真正的数组是特殊的对象，只会遍历索引值。

**标准的for循环中的i是number类型,表示的是数组的下标,但是for in循环中的i表示的是数组的key是string类型,因为js中一切皆为对象。**

下面看一下如果使用for in循环会发生什么？

**示例3：**

```js
<body>
    <ul>
        <li id="one"></li>
        <li name="zhou"></li>
        <li name="zhou"></li>
        <li name="zhou"></li>
        <li name="zhou"></li>
    </ul>
</body>

<script>
    var resultByName = document.getElementsByName("zhou");
    // console.log(resultByName);
    for (var i in resultByName) {
        console.log(i)
    }
</script>
```

输出：

![mark](http://qiniu.wind-zhou.com/blog/201222/Dg4BA2EG3E.png?imageslim)

> 参考链接:[js中数组遍历for与for in区别(强烈建议不要使用for in遍历数组)](https://www.cnblogs.com/pinganzi/p/5671462.html)

#### 3、通TagName标记名称获取文档节点集合

`document.getElementByTagName(TagName);`

**示例：**

```js

<script>
    var list2 = document.getElementsByTagName("li");
    for (var i = 0; i < list2.length; i++) {
        list2[i].style.background = "purple"
    }
</script>
```

输出：![mark](http://qiniu.wind-zhou.com/blog/201222/76ge8dH52F.png?imageslim)

**相当于css里的标签选择器。**

#### 4、通过ClassName 标记获取文档节点集合（常用）

IE8及以下不支持。

**示例：**

```js
<body>
    <ul>
        <li id="one"></li>
        <li class="zhou"></li>
        <li class="zhou"></li>
        <li class="zhou"></li>
        <li class="zhou"></li>
    </ul>
</body>

<script>
    var list2 = document.getElementsByClassName("zhou");
    for (var i = 0; i < list2.length; i++) {
        list2[i].innerHTML = "hello world"
    }
</script>
```

输出：![mark](http://qiniu.wind-zhou.com/blog/201222/f4H4faEdbc.png?imageslim)

**相当于css的类别选择器。**

#### 5、document.querySelect()

**css选择器模式**。返回与该元素匹配的**第一个元素**。

**示例：**

```js
<body>
    <ul>
        <li id="one"></li>
        <li class="zhou"></li>
        <li class="zhou"></li>
        <li class="zhou"></li>
        <li class="zhou"></li>
    </ul>
</body>

<script>
    var list2 = document.querySelector(".zhou");

    list2.innerHTML = "hello world"
</script>
```

输出：![mark](http://qiniu.wind-zhou.com/blog/201222/Ck116EKGdE.png?imageslim)



#### 6、document.querySelectAll()

**css选择器模式**。返回与该元素匹配的**所有元素**。

**示例：**

```js
<body>
    <ul>
        <li id="one"></li>
        <li class="zhou"></li>
        <li class="zhou"></li>
        <li class="zhou"></li>
        <li class="zhou"></li>
    </ul>
</body>

<script>
    var list2 = document.querySelectorAll(".zhou");
    for (var i = 0; i < list2.length; i++) {
        list2[i].innerHTML = "hello world"
    }
</script>
```

输出：

![mark](http://qiniu.wind-zhou.com/blog/201222/aCi182G81g.png?imageslim)



### 文档节点的内容处理

- innerText  设置或获取元素文本内容
- textContent 获取或设置元素文本内容（基本不用了）
- innerHTML **（常用）**

**注释:这几个属性都可以进行设置或读取。**

**innerHTML与innerText的区别：**

innerHTML可以获取标记内的所有内容，而innerText只能获取文本。当设置时innertext内部的标记会原样输出。

**示例1：**

```js
<body>
    <div id="one"></div>
    <div id="two"></div>
</body>

<script>
    var x = document.getElementById("one");
    var y = document.getElementById("two");

    x.innerHTML = "<h1>hello world</h1>";
    y.innerText = "<h1>hello world</h1>";
</script>

```

输出:![mark](http://qiniu.wind-zhou.com/blog/201222/m52hKAd5mj.png?imageslim)

**这几个属性可以设置也可以读取，下面演示读取**。

**示例2：**

```js
<body>
    <div id="one">
        <h1>zhouzheng</h1>
    </div>
    <div id="two">
        <h1>周正</h1>
    </div>
</body>

<script>
    var x = document.getElementById("one");
    var y = document.getElementById("two");


    console.log("one里面的内容是：" + x.innerHTML)//连嵌套的元素都读出来
    console.log("two里面的内容是：" + y.innerText)  //只读文本
</script>
```

输出:![mark](http://qiniu.wind-zhou.com/blog/201222/16B2d8ghea.png?imageslim)



### 查看节点信息

![mark](http://qiniu.wind-zhou.com/blog/201224/eh77lFDE6I.png?imageslim)

(1)节点名称

- **元素节点的nodeName就是标签的名称（大写）  重点**
- 属性节点的nodeName就是属性的名称（id）（获取属性节点对象名。Attribute[下标]）
- 文本节点的nodeName永远都是#text
- 文档节点的nodeName都是从#document
- 注释节点的nodeName都是#comment

(2)nodeValue

1. 对文本节点，nodeValue属性包含文本
2. 对于属性节点，nodeValue属性值包含属性值
3. 对于**文档节点**和**元素节点**不可用（返回NULL）
4. 对注释节点返回注释内容

(3)节点类型 nodetype

| 元素类型 | 节点类型 |
| :------: | :------: |
|   元素   |    1     |
|   属性   |    2     |
|   文本   |    3     |
|   注释   |    8     |
|   文档   |    9     |

**示例：**

```js
<body>
    <!-- 这是一个注释节点 -->
    <div id="one">hello ,This is an element node!</div>

</body>

<script>
    //1、拿到元素节点
    var divNode = document.getElementById("one");
    console.log("元素节点的nodeName和nodeValue和nodeType分别为：\t\t" + divNode.nodeName + "/" + divNode.nodeValue + "/" + divNode.nodeType)
        //2、拿到属性节点(通过元素节点)
    var attrNode = divNode.attributes[0];
    console.log("属性节点的nodeName和nodeValue和nodeType分别为：\t\t" + attrNode.nodeName + "/" + attrNode.nodeValue + "/" + attrNode.nodeType)
        //3、拿到文本节点
    var textNode = divNode.firstChild;
    console.log("文本节点的nodeName和nodeValue和nodeType分别为：\t\t" + textNode.nodeName + "/" + textNode.nodeValue + "/" + textNode.nodeType)
        //4、拿到注释节点

    var commentNode = document.body.childNodes[1];
    console.log("注释节点的nodeName和nodeValue和nodeType分别为：\t\t" + commentNode.nodeName + "/" + commentNode.nodeValue + "/" + commentNode.nodeType)
        //输出文档节点
    console.log("文档节点的nodeName和nodeValue和nodeType分别为：\t\t" + document.nodeName + "/" + document.nodeValue + "/" + document.nodeType)
</script>
```

**输出：**

![mark](http://qiniu.wind-zhou.com/blog/201224/D1J2CDmKcg.png?imageslim)

上面的例子中包含了各种节点的找法，注，属性节点的找法略有不同，**因为属性节点不是元素节点的子节点**。

### 创建、添加、移动节点

**接下来的内容就是对节点的增删改查。**

创建、删除、移动、替换、复制、检测是否有子节点

（1）创建节点
- **createElement()** 创建一个**元素节点**
- createTextNode()创建文本节点  **没什么用**

（2）移动节点
- **appendChild(node)**
  **添加节点到当前节点内部的后面**
  
- **insertBefore（**要移动的节点，参考节点）

  **移动到当前节点内部的参考节点的前面。**

**示例1：**创建节点，并添加到指定位置

（3）删除节点

- remove() 

  **删除当前节点  -------IE不支持**

- removeChild（node） 

  删除当前节点的子节点

（4）复制节点

- cloneNode（true）----深拷贝**（常用）**

​        除了复制节点。还复制所有的子节点

- cloneNode(false) ----浅复制

  只复制节点，内部子元素为空。

（5）替换（移动）节点

- **replaceChild**(新节点，要替换的节点)

  **移动原来的节点并替换指定节点**

（6）判断是否有子节点

- **hasChildNodes（）**

  如果有返回true
  没有返回false

  **注：里面有空格，也会算文本节点。**

（6）判断是否包含某节点

- contains(node)

  判断是否包含某节点

**示例：**

```js
<body>
    <div id="one">
        <h1>hello world!</h1>
    </div>
</body>


<script>
    //创建节点
    var nodeDiv = document.createElement("div");
    nodeDiv.innerHTML = "你好！";
    console.log(nodeDiv);
    //添加到指定位置
    var one = document.getElementById("one");
    one.appendChild(nodeDiv);
</script>
```

输出：

![mark](http://qiniu.wind-zhou.com/blog/201222/CDcajAHGDI.png?imageslim)



**示例2：**

移动节点,将和和h3移动到div内部的h1节点前面。

```js
<body>
    <h3 id="zhou">周正</h3>
    <div id="one">
        <h1>hello world</h1>
    </div>

    <button onclick="move()"> 点击移动</button>
</body>

<script>
    function move() {
        var h = document.getElementById("zhou");
        // document.getElementById("one").appendChild(h); 
        document.getElementById("one").insertBefore(h, document.getElementsByTagName("h1")[0])
    }
</script>
```

**示例3：**

下面对以上的方法进行汇总

```js
<!DOCTYPE html>
<html>

<head>
    <meta charset="utf-8">
    <title></title>
</head>

<body>
    <div id="one">
        <h1 id="two">hello world!</h1>
    </div>

    <button onclick="appendNode()">点击使用append添加节点</button> <br>
    <button onclick="insertNode()">点击使用insertBefore添加节点</button> <br>

    <button onclick="removeNode()">删除添加节点</button> <br>
    <button onclick="copyNode()">点击复制节点</button> <br>

    <button onclick="replaceNode()">点击替换节点</button> <br>

    <button onclick="isExistNode()">判断是否存在指定元素</button> <br>

</body>

<script>
    function appendNode() {
        //1、创建新节点
        var newNode = document.createElement("p");
        newNode.innerHTML = "<h1>周正（使用append添加）</h1>";
        console.log(newNode);
        //2、添加节点到末尾 appendChild
        var divNode = document.getElementById("one");
        divNode.append(newNode);
    }

    //插入节点
    function insertNode() {
        //1、创建新节点
        var newNode = document.createElement("p");
        newNode.innerHTML = "<h1>周正 （使用insert添加）</h1>";
        console.log(newNode);
        //2、添加节点指定节点前面
        var divNode = document.getElementById("one");
        divNode.insertBefore(newNode, document.getElementsByTagName("h1")[0])
    }

    //移除节点
    function removeNode() {
        var deleteNum = prompt("输入你想删除的p标签个数");
        console.log("接收到的值为" + deleteNum)

        var divNode = document.getElementById("one");

        //divNode.remove(); 使用remove删除

        for (var i = 0; i < parseInt(deleteNum); i++) {
            console.log(i)
            divNode.removeChild(document.getElementsByTagName("p")[0]); //注意这里的每次下标为0
        }

    }
    //复制节点
    function copyNode() {
        var divNode = document.getElementById("one");
        var copyNodes = divNode.cloneNode(true)
        console.log(copyNodes);
    }
    //替换节点
    function replaceNode() {
        var divNode = document.getElementById("one");

        var newNode = document.createElement("p");
        newNode.innerHTML = "<h1>周正 （使用insert添加）</h1>";
        //替换之前的h标签
        var oldNode = document.getElementById("two");
        divNode.replaceChild(newNode, oldNode);
    }

    //判断某节点是否存在
    function isExistNode() {
        var elementType = prompt("输入你想判断的元素");
        console.log(elementType)

        var divNode = document.getElementById("one");
        var state = divNode.contains(document.getElementsByTagName(elementType)[0]); //注意，这里面的elementType不能加""
        document.write(state);

    }
</script>

</html;
```

结果不再输入，需要时自行调试即可。（里面还有一些bug，以后有时间在改进）。

### 节点访问（查找）

**研究的就是通过父子兄弟关系等来回的找节点。**

#### 更改为父节点

-  parentNode

  子节点可以调用此**属性**，找到他的父节点。

- parentElement

  返回当前元素的**父元素节**点  （IE9一下不兼容）

  实际使用时一样。
  
  

#### 通过父节点更改为子节点

- firstChild  更改为当前对象的**第一个**子节点

  **注意：**使用此方法时，不能有空格，负责找到的是**第一个文本文本节点。**

- firstElementChild 

   **//返回的是第一个元素节点**    

- lastElementChild  

   **//返回最后一个元素节点**    （IE9以下不兼容）

#### 以集合方式更改子节点

- childNodes 

  更改为子节点的集合（下标从0开始）

- children

  更改为子元素的集合（下标从0开始）

> 二者区别：他们的区别就是**childNodes**包括元素节点和文本节点，而**children**只包括元素节点。

#### 更改为兄弟节点

- nextSibling

  更改为下一个兄弟

- nextElementSibling

  更改为下一个元素兄弟

- previousSibling

  更改为上一个兄弟

- previousElementSibling

  更改为上一个元素兄弟

### 属性操作

节点属性：

- getAttribute("属性名")  获得节点属性
- setAttribute("属性名"，：值)  设置节点属性
- removeAttribute(“属性名”)  删除节点属性

**示例：**

**用在页面的样式切换**

```js
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <style>
        .con {
            width: 100px;
            height: 100px;
            background: pink;
            margin: 50px 0 0 100px;
            transition: transform 500ms;
        }
        
        .cons {
            transform: scale(2)
        }
    </style>
</head>

<body>
    <div class="con" id="one" onclick="scale()">
    </div>
</body>
<script>
    function scale() {
        var con1 = document.getElementById("one");
        if (con1.getAttribute("class") == "con") {
            con1.setAttribute("class", "con cons")
        } else {
            con1.setAttribute("class", "con")
        }
    }
</script>
</html>
```

注释:这种方法是通过绑定事件，在事件里实现属性样式的切换。

## 样式设置

控制的行内样式，获取和设置的都是行内。

style.cssText属性。

注：若遇到类似font-size这种带连接符的，样式名称要转成驼峰命名法。



**className属性。只是来控制class类型的。**

示例：用className重写点击变换样式



```js
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <style>
        .con {
            width: 100px;
            height: 100px;
            background: pink;
            margin: 50px 0 0 100px;
            transition: transform 500ms;
        }
        
        .cons {
            transform: scale(2)
        }
    </style>
</head>

<body>
    <div class="con" id="one" onclick="scale()">
    </div>
</body>
<script>
    function scale() {
        var con1 = document.getElementById("one");
        
        if (con1.className == "con") {
            con1.className = "con cons";
        } else {
            con1.className = "con";
        }
    }

</script>

</html>
```





![mark](http://qiniu.wind-zhou.com/blog/201227/e1cHiL7Kad.png?imageslim)















