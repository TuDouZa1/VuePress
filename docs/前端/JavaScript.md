---
title: JavaScript
createTime: 2025/07/08 17:03:15
permalink: /article/dii4y3nj/
---
# JavaScript

## 变量的定义

```js
let a;
```



## 函数的定义

```javascript
function add(a, b) {
    return a + b;
}
                    
var add = function(a, b) {
    return a + b;
}
```

## 数组

### 数组的创建

```javascript
var arr = new Array();
var arr = new Array(10);
var arr = [1, 2, 3];
var arr = ["apple", "banana", "orange"];
```

### 数组方法

push: 向数组末尾添加元素

pop: 删除数组末尾的元素

shift: 删除数组开头的元素

unshift: 向数组开头添加元素

splice: 在数组中添加或删除元素

sort: 对数组元素进行排序

reverse: 反转数组元素的顺序

join: 将数组元素转换为字符串

```javascript
var arr = [1, 3, 2];
arr.push(4); // [1, 3, 2, 4]
arr.pop(); // 4
arr.shift(); // 1
arr.unshift(0); // [0, 3, 2]
arr.splice(1, 1, "apple"); // [0, "apple", 2]
arr.sort(); // [0, 2, "apple"]
arr.reverse(); // ["apple", 2, 0]
arr.join("-"); // "apple-2-0"
```

### 遍历数组

for...in: 遍历数组的键值

forEach: 遍历数组的元素

```javascript
var arr = [1, 2, 3];
// for...in
for (var i in arr) { console.log(arr[i]); }
// forEach
arr.forEach(function(e) { console.log(e); });
// 箭头函数
arr.forEach((e) => { console.log(e); });
```

## 字符串

### 字符串的创建

```javascript
var str = "Hello, world!";
var str = new String("Hello, world!");
var str = String("Hello, world!");
```

### 字符串方法

charAt: 获取指定位置的字符

charCodeAt: 获取指定位置的字符的ASCII码

concat: 连接两个或多个字符串

indexOf: 查找指定字符串的位置

lastIndexOf: 从后向前查找指定字符串的位置

localeCompare: 比较两个字符串

match: 匹配字符串

replace: 替换字符串

search: 查找字符串

slice: 截取字符串

split: 分割字符串

substring: 截取字符串

toLowerCase: 转换为小写

toUpperCase: 转换为大写

trim: 去除字符串两端的空白字符

```javascript
var str = "Hello, world!";
console.log(str.charAt(0)); // "H"
console.log(str.charCodeAt(0)); // 72
console.log(str.concat(" How are you?")); // "Hello, world! How are you?"
console.log(str.indexOf("l")); // 2
console.log(str.lastIndexOf("l")); // 9
console.log(str.localeCompare("hello")); // 1
console.log(str.match(/l/g)); // ["l", "l"]
console.log(str.replace("l", "L")); // "HeLLo, world!"
console.log(str.search("l")); // 2
console.log(str.slice(2, 5)); // "llo"
console.log(str.split(" ")); // ["Hello,", "world!"]
console.log(str.substring(2, 5)); // "llo"
console.log(str.toLowerCase()); // "hello, world!"
console.log(str.toUpperCase()); // "HELLO, WORLD!"
console.log(str.trim()); // "Hello, world!"
```

## JSON

> ###### JSON(JavaScript Object Notation)是一种轻量级的数据交换格式，它基于ECMAScript的一个子集。它是一种基于文本的、可读性高的、占用空间小的的数据交换格式。

### JSON的创建

```javascript
var obj = {name: "John", age: 30, city: "New York"};
var json = JSON.stringify(obj);
console.log(json); // {"name":"John","age":30,"city":"New York"}
```

### JSON的解析

```javascript
var json = '{"name":"John","age":30,"city":"New York"}';
var obj = JSON.parse(json);
console.log(obj.name); // "John"
```

JSON.stringify()方法用于将JavaScript对象转换为JSON字符串。

JSON.parse()方法用于将JSON字符串转换为JavaScript对象。

```javascript
var obj = {name: "John", age: 30, city: "New York"};
var json = JSON.stringify(obj);
console.log(json); // {"name":"John","age":30,"city":"New York"}
var obj2 = JSON.parse(json);
console.log(obj2.name); // "John"
```

### value的数据类型

数字：整数或浮点数

字符串：用双引号或单引号括起来的任意文本

布尔值：true或false

数组：用方括号括起来的元素列表，元素之间用逗号分隔

对象：用花括号括起来的键-值对列表，键和值之间用冒号分隔

null：表示一个空值

## BOM

> ###### BOM(Browser Object Model)是W3C组织制定的一套Web浏览器对象模型，提供了独立于内容而与浏览器窗口进行交互的接口。BOM定义了与浏览器窗口进行交互的对象，如window、navigator、location、history、screen、document等。

window: 全局对象

navigator: 浏览器信息

location: 页面地址

history: 历史记录

screen: 屏幕信息

document: 文档对象

### 示例

```html
<script>
    console.log(window.innerWidth); // 窗口宽度
    console.log(location.href); // 页面地址
    console.log(history.length); // 历史记录数
    console.log(screen.width); // 屏幕宽度
    console.log(document.title); // 文档标题
</script>
```

效果：(在控制台看)

## DOM

> ###### DOM是Document Object Model的缩写，它是W3C组织推荐的处理可扩展置标语言的标准编程接口。DOM定义了处理网页内容的模型，并提供了对文档的各种功能的访问。

document: 整个HTML文档

createElement: 创建元素

createTextNode: 创建文本节点

getElementById: 获取指定元素

getElementsByTagName: 获取指定标签的所有元素

getElementsByName: 获取指定名称的所有元素

getElementsByClassName: 获取指定类名的所有元素

appendChild: 向元素添加子元素

removeChild: 从元素移除子元素

innerHTML: 获取或设置元素的innerHTML

style: 获取或设置元素的样式

### 获取元素对象

```html
<div id="box"></div>
<script>
    var box = document.getElementById("box");
    box.innerHTML = "Hello, world!";
    box.style.backgroundColor = "red";
</script>
```

效果：

Hello, world!

## 事件

### 事件类型

click: 鼠标点击事件

dblclick: 鼠标双击事件

mousedown: 鼠标按下事件

mouseup: 鼠标松开事件

mousemove: 鼠标移动事件

mouseover: 鼠标移入事件

mouseout: 鼠标移出事件

keydown: 键盘按下事件

keyup: 键盘松开事件

keypress: 键盘输入事件

### 事件绑定

```html
<input type="button" id="btn" value="按钮">
<script>
    var btn = document.getElementById("btn");
    btn.onclick = function() {
        console.log("按钮被点击了！");
    };
</script>
<input type="button" onclick="click_me()" value="按钮">
<script>
    function click_me() {
        console.log("按钮被点击了！");
    }
</script>
```

## 定时器

setTimeout: 延迟执行函数

setInterval: 循环执行函数

```html
<script>
    setTimeout(function() {
        console.log("3秒后执行");
    }, 3000);
    setInterval(function() {
        console.log("每隔1秒执行");
    }, 1000);
</script>   
```