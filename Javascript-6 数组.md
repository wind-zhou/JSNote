# lesson-6 数组

## 创建数组

- 直接创建(**最常用**)设施

  ```js
  语法：var 数组名 =[元素1，元素2，元素3，......];
  ```

- 指定数组元素

  ```js
  语法：
  var 数组名 =new Array();
  或
  var 数组名 =new Array(元素1，元素2，元素3，......);
  ```

- 指定数组长度

  ```js
  语法： var 数组名 =new Array(size);
  
  这个size指的是最小长度，数组赋值时可以超出，数组会自动加长。
  ```

>**注意：**
>
>没有必要使用 JavaScript 的内建数组构造器 new Array()。
>
>new 关键词只会使代码复杂化。它还会产生某些不可预期的结果：



JavaScript数组里的元素**可以是不同数据类型**。数组里的元素也可以是数组。

```js
   var arr1=[10,"zhou","周正",true]
    var arr2=new Array();
    var arr3=new Array("周正","100",true);
    var arr4=new Array(5);
```

先创建后赋值

```js
arr2[0]="你好"
```

空数组赋值时如果直接复制`arr[4]=10`,则arr[0],arr[1],arr[2],arr[3]都为空，类型是undefined。

**验证：**

```js
<script>
    var arr = new Array();
    arr[1] = "你好"
    arr[5] = 10
    document.write(arr)
</script>
```

输出：

![mark](http://qiniu.wind-zhou.com/blog/201209/C9f81eGCHB.png?imageslim)

当单独输出arr[4]时，输出undefined

```js
document.write(arr[4])
```

![mark](http://qiniu.wind-zhou.com/blog/201209/f8F2D6FDhL.png?imageslim)

## 数组的遍历

（1）传统for循环

```js
<script>
    var arr = [10, 34, 22, 52, 66]
    for (var i = 0; i < arr.length; i++) {
        arr[i] = arr[i] * 2
    }
    document.write(arr)
</script>
```

（2）for in 遍历

```js
<script>
    var arr = [10, 23, 55, 1, 335, 79, 43]
    for (var i in arr) {
        arr[i] = arr[i] * 2
    }
    document.write(arr)
</script>
```

> fo循环和for in的区别?
>
> ...



###冒泡排序

```js
<script>
    var arr = [10, 1, 35, 61, 89, 36,55];
    for (i = 0; i < arr.length - 1; i++) { //外层需要排序的数字个数
        for (j = 0; j < arr.length - 1 - i; j++) { //每次循环时，需要交换的次数
            if (arr[j] > arr[j + 1]) {
                var tmp = arr[j];
                arr[j] = arr[j + 1];
                arr[j + 1] = tmp;
            }
        }
    }
    document.write(arr)
</script>
```

![mark](http://qiniu.wind-zhou.com/blog/201209/Hkc38kjGd9.png?imageslim)



**算法分析：**

两层循环
（1）外层是需要排序的数字个数

​		如果有n个数，则只需将n-1个数进行排序即可。因此外层循环`arr.length-1`次。

（2）内层循环是每次排序时需要交换的次数

| 第 i 次排序 | 此时需要的交换次数  j |
| :---------: | :-------------------: |
|      0      |           6           |
|      1      |           5           |
|      2      |           4           |
|      3      |           3           |
|      4      |           2           |
|      5      |           1           |
|     ...     |          ...          |
|      i      |    arr.length-1-i     |

时间复杂度o(n<sup>2</sup>)

冒泡排序其实就是将每次将 最大（或最小）的数放到最后面的位置，属于从后往前排，选择排序是从前到后排。



###选择排序

```js
<script>
    var arr = [10, 1, 35, 61, 89, 36, 55];

    for (var i = 0; i < arr.length - 1; i++) {
        for (var j = i + 1; j < arr.length; j++) {

            if (arr[i] > arr[j]) {
                var tmp
                tmp = arr[i]
                arr[i] = arr[j]
                arr[j] = tmp
            }

        }
    }
    document.write(arr)
</script>
```

**算法分析：**

两层循环：

（1）第一层循环和冒泡一样，是需要排序位置（从前往后）

​		n个数子，则需排序n-1个数，因此循环`arr.length-1`次

（2）内层循环是每次需要比较的次数

​		循环体内做的是当前位置的数和后面的所有数进行比较，如果后面的数比当前位置的数大（或小），就进行换位。



选择排序是从前往后，给各个位置上一次放上相应大小得数，例如，升序排列时，第一个位置便应放最小的数，因此在内层循环时，将arr[0]和后面的数arr[j]一次比较，有比他小的就换位，当磁层内循环结束时，第一位置行放置的就是最小的数，外层第i个位置上的数同理，此时需要把arr[i]和后面的arr[j]进行比较，此时的j也有讲究，j应该从i+1开始，

直到`arr.lrngth-1`。

选择排序**其实有类似山寨选领导，采用攻擂的模式，某人先是擂主，接下来不断有挑战者，输了就换位，直到打败所有挑战者，就放在大当家位置，接下来选二当家、三当家、依次类推。**

 时间复杂度： O(N2)。 

### sort()排序

注：如果数组里面的不全是数字，则按编码号进行编码(如：**英文用ASCALL码**)，默认升序。

```js
//升序
<script>
    var arr = [10, 1, 35, 61, 89, 36, 55];
    arr.sort(function(a, b) {
        return a - b;
    })
    console.log(arr)
</script>

//输出：[1, 10, 35, 36, 55, 61, 89]


//降序
<script>
    var arr = [10, 1, 35, 61, 89, 36, 55];

    arr.sort(function(a, b) {
        return b - a;
    })
    console.log(arr)
</script>

//输出：[89, 61, 55, 36, 35, 10, 1]
```

**注释：**当sort()没有参数时，默认为升序。

## 数组对象

数组元素部分：属性和方法

### 数组属性

- constructor

  　对创建数组对象的Array构造函数的引用,

- **length (最常用)**

　　 　数组的长度

-  prototype

　　　我们创建的每一个函数都有一个prototype（原型）属性，这个属性是一个指针，指向一个对象，而这个对象的用途是包含可以由特定类型的所有实例共享的属性和方法。

​	    	**prototype方法能让我们有能力向对象添加属性和方法。**



###数组的方法

#### (1)push()

**作用：在尾部添加元素**

```js
<body>
    <button onclick="add()">点击添加数组元素</button>
</body>

<script>
    var arr = [1,46,23]
    function add() {
        arr.push("你好")
        console.log(arr)
    }
</script>
//输出：[13, 55, 20, "你好"]
```

#### (2)unshift()

**作用：在数组的头部添加元素**

用法同上

```js
<body>
    <button onclick="unshift()">点击添t头部加数组元素</button>
</body>

<script>
       var arr = [1, 46, 23]
       function unshift() {
        arr.unshift("你好")
        console.log(arr)
    }
</script>
//输出：["你好"13, 55, 20,]
```



#### (3)delete()

**作用：删除指定下标的元素**

语法 `delete 数组名[index]`

**注：只删除元素，不删除位置**

#### (4)pop()

**作用：删除数组最后一个元素**

语法： `数组名.pop()`

#### (5) shift()

**作用：删除数组头部元素·**

语法  ``数组名.shift()``

**注：shift删除使连同位置一起删除**

#### (6)indexOf()

**作用：查询数组中是否有指定元素**

输出首次查询到的索引值，找不到返回-1

**应用：数组去重**

```js
<script>
    var arr = [39, 10, 2, 55, 23, 54, 7, 22, 43, 22, 55, 39]
    //去重
    var arr2 = []
    for (var i in arr) {
        if (arr2.indexOf(arr[i]) == -1) {
            arr2.push(arr[i])
        }
    }
    alert(arr2)
</script>

//输出：[39, 10, 2, 55, 23, 54, 7, 22, 43]
```

#### (7) revese()

**作用：颠倒数组的元素**

```js
<script>
    var arr = [39, 10, 2, 55, 23, 54, 7, 22, 43, 22, 55, 39]
    arr.reverse()
    document.write(arr)
</script>
//输出：[39, 55, 22, 43, 22, 7, 54, 23, 55, 2, 10, 39]
```

**注释：**会改变原数组的结构。

#### (8)concat（）

**作用：合并数组** 

var newarr=数组名.concat(数组名1，数组名2，...)

```js
<script>
    var arr1 = [39, 10, 2, 55, 23, 54, 7, 22, 43, 22, 55, 39]
    var arr2 = [13, 55, 20]
    var arr3 = arr2.concat(arr1)
    console.log(arr3)
</script>

//输出：[13, 55, 20, 39, 10, 2, 55, 23, 54, 7, 22, 43, 22, 55, 39]
```

**注释：不会改变原数组结构，会返回一个新数组**

#### (9)toString（）

**作用：数组转成字符串， toString 将数组的元素转为字符串**

​	js中是个对象都有这种方法

简单来说就是在数组外部加了个引号

**没什么用!**

document.write本身就有一个隐式转换，会输出字符串

#### (10)   join ()（常用）

**作用：数组转为字符串**

使用join可以指定分隔符样式，当输入为`“”`时，便去掉了了都逗号。

```js
<script>
    var arr2 = [13, 55, 20, 65, 11]
    var str1 = arr2.join(" ")
    var str2 = arr2.join("#")
    console.log(str1)    //输出：13 55 20 65 11
    console.log(str2)    //输出： 13#55#20#65#11
</script>
```

**注释：不会改变原数组**

#### (11)splice()

**作用：更新移动数据**

**语法：**

`数组名.splice(删除元素的起始位置,删除元素的个数，插入元素1,插入元素2,...) `

从一个数组中移除一个或多个元素，剩下的元素组成一个新数组，移除的元素单独组成一个数组返回。

**注释：会改变元素组的结构**

```js
<script>
    var arr1 = ["周", "正", "我", "爱"]
    var newarr = arr1.splice(1, 2, "欧巴", "baba")
    console.log(arr1)
</script>
```

![mark](http://qiniu.wind-zhou.com/blog/201214/JKkmAA7gD4.png?imageslim)

#### (12) slice()

**作用：截取数组元素**

截取一段元素，并将截取的元素组成一个新数组。**（原数组不受影响）**

语法：

`数组名.slice(开始截取下标，结束的位置下标)`

```js
<script>
    var arr1 = ["周", "正", "我", "爱", "你", "哦"]
    var newarr = arr1.slice(3, -1)
    console.log(newarr)
    console.log(arr1)
</script>
```

![mark](http://qiniu.wind-zhou.com/blog/201214/5D793jDlIB.png?imageslim)

注：截取时不包含结束位置，因此要向下多写一位。

#### (13) forEach()

**作用：对数组进行遍历循环，对数组每一项给定指定的函数**

```js
<script>
    var arr = [2, 4, 6, 2, 5, 7, 11, 52, 7]
        // for (var i = 0; i < arr.lenght; i++) {
        //     if (arr[i] % 2 == 0) {
        //         arr[i] *= 2;
        //     }

    // }

    arr.forEach(function(value, index, arr) {
         arr[index] = value * 2;
    })

    console.log(arr)
</script>

//输出：[[4, 8, 12, 4, 10, 14, 22, 104, 14]
```

注意：函数体里不能直接写``value*=2；``,此时值不会改变。因为这时属于值传递，只有使用到arr，才算是地址传递。

**注释：会改变原数组。**

####(14) map( )映射

**作用：遍历数组时会对每一个进行操作，并将运算结果返回并组成一个新数组。**

```js
<script>
    var arr = [2, 4, 6, 2, 5, 7, 11, 52, 7]
    var newarr = arr.map(function(value) {
        var tmp;
        tmp = value * value;
        return tmp;
    })
    document.write(newarr)
        //原数组不会改变
</script>
//输出：[4, 16, 36, 4, 25, 49, 121, 2704, 49]
```

注：**内层函数体里要有个返回值**，因为要返回构成新数组，而之前的forEach不需要，因为是直接对原数组进行操作。

**注：原数组不会改变**

####(15)filter()  过滤

**作用：遍历数组，并对每个元素进行操作（运行一个函数），返回满足过滤条件的值，并组成一个新数组。**

```js
<script>
    var arr = [2, 4, 6, 2, 5, 7, 11, 52, 7]
    var newarr = arr.filter(function(value, index) {
        return value % 2 != 0 && value > 5;
    })
    document.write(newarr)
</script>
//输出：[7, 11, 7]
```

|           作用类型           |                             方法                             |
| :--------------------------: | :----------------------------------------------------------: |
|           增删元素           | pop()----尾部删元素<br />unshift()----头部加 元素 <br />delete()----删元素<br />push()----尾部加元素<br />shift()----头部删元素<br /> |
|           查找数据           |                    indexOf()----返回索引                     |
|           操作数组           |    reverse()----颠倒顺序  <br />concat()---拼接数组<br />    |
|    转换数组（转为字符串）    |     toString()----转换成字符串<br />join()----转为字符串     |
|         更改数组元素         | splice()----替换元素<br />slice()----选取指定元素，单独构成数组 |
| 遍历数组并对每个元素施加函数 | forEach()----对每个元素机进行操作，并改变原数组<br />map()----对每个元素进行操作，并返回映射<br />filter()----对数组元素进行条件过滤 |

