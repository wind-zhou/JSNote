# lesson-16 json

##简介

JSON: **J**ava**S**cript **O**bject **N**otation(JavaScript 对象表示法)

JSON 是存储和交换文本信息的语法，类似 XML。

JSON 比 XML 更小、更快，更易解析。

## JSON 实例

```json
{
    "sites": [
    { "name":"菜鸟教程" , "url":"www.runoob.com" }, 
    { "name":"google" , "url":"www.google.com" }, 
    { "name":"微博" , "url":"www.weibo.com" }
    ]
}
```

这个 sites 对象是包含 3 个站点记录（对象）的数组。

------

## 什么是 JSON ？

- JSON 指的是 JavaScript 对象表示法（**J**ava**S**cript **O**bject **N**otation）
- JSON 是轻量级的文本数据交换格式
- JSON 独立于语言：JSON 使用 Javascript语法来描述数据对象，但是 JSON 仍然独立于语言和平台。JSON 解析器和 JSON 库支持许多不同的编程语言。 目前非常多的动态（PHP，JSP，.NET）编程语言都支持JSON。
- JSON 具有自我描述性，更易理解



## 与 XML 相同之处

- JSON 是纯文本
- JSON 具有"自我描述性"（人类可读）
- JSON 具有层级结构（值中存在值）
- JSON 可通过 JavaScript 进行解析
- JSON 数据可使用 AJAX 进行传输

------

## 与 XML 不同之处

- 没有结束标签
- 更短
- 读写的速度更快
- 能够使用内建的 JavaScript eval() 方法进行解析
- 使用数组
- 不使用保留字

>**最大的不同是**：XML 需要使用 XML 解析器来解析，JSON 可以使用标准的 JavaScript 函数来解析。
>
>- [JSON.parse()](https://www.runoob.com/js/javascript-json-parse.html): 将一个 JSON 字符串转换为 JavaScript 对象。
>- [JSON.stringify()](https://www.runoob.com/js/javascript-json-stringify.html): 于将 JavaScript 值转换为 JSON 字符串。

------

## 为什么使用 JSON？

对于 AJAX 应用程序来说，JSON 比 XML 更快更易使用：

#### 使用 XML

- 读取 XML 文档
- 使用 XML DOM 来循环遍历文档
- 读取值并存储在变量中

#### 使用 JSON

- 读取 JSON 字符串
- 用 eval() 处理 JSON 字符串



## JSON 语法规则

JSON 语法是 JavaScript 对象表示语法的子集。

- 数据在名称/值对中
- 数据由逗号分隔
- 大括号 **{}** 保存对象
- 中括号 **[]** 保存数组，数组可以包含多个对象



## JSON 文件

- JSON 文件的文件类型是 **.json**
- JSON 文本的 MIME 类型是 **application/json**



## JSON.parse()

JSON 通常用于与服务端交换数据。

在接收服务器数据时一般是字符串。

我们可以使用 JSON.parse() 方法将数据转换为 JavaScript 对象。

### 语法

```json
JSON.parse(text[, reviver])
```

**参数说明：**

- **text:**必需， 一个有效的 JSON 字符串。
- **reviver:** 可选，一个转换结果的函数， 将为对象的每个成员调用此函数。



##JSON.stringify()

JSON 通常用于与服务端交换数据。

在向服务器发送数据时一般是字符串。

**我们可以使用 JSON.stringify() 方法将 JavaScript 对象转换为字符串。**

### 语法

```json
JSON.stringify(value[, replacer[, space]])
```

**参数说明：**

- value:

  必需， 要转换的 JavaScript 值（通常为对象或数组）。

- replacer:

  可选。用于转换结果的函数或数组。

  如果 replacer 为函数，则 JSON.stringify 将调用该函数，并传入每个成员的键和值。使用返回值而不是原始值。如果此函数返回 undefined，则排除成员。根对象的键是一个空字符串：""。

  如果 replacer 是一个数组，则仅转换该数组中具有键值的成员。成员的转换顺序与键在数组中的顺序一样。当 value 参数也为数组时，将忽略 replacer 数组。

- space:

  可选，文本添加缩进、空格和换行符，如果 space 是一个数字，则返回值文本在每个级别缩进指定数目的空格，如果 space 大于 10，则文本缩进 10 个空格。space 也可以使用非数字，如：\t。



## json语法规则

（1）json数据

```json
"name":"zhouzzheng","age":"18","sex":"男"
```

（2）json对象

```json
{"name":"zhouzzheng","age":"18","sex":"男"}
```

（3）json数组

```json
[
    {"name":"zhouzzheng","age":"18","sex":"男"}，
	{"name":"wind","age":"30","sex":"女"} 
]
```











