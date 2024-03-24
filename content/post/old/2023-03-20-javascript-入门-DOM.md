+++
title = "Javascript 入门-DOM"
description = ""
date = 2023-03-20T21:50:30+08:00
featured = false
comment = true
toc = true
reward = true
categories = [
  ""
]
tags = [
  "js"
]
series = []
images = []
+++

dom 元素的定位、修改、创建、删除、指定位置插入等操作
<!--more-->

### dom
```js
// 获取id为myDiv的元素
var myDiv = document.getElementById("myDiv");⭐️

// 修改元素文本内容
myDiv.innerHTML = "<p>Hello, DOM!</p>";

// 创建新元素并添加到myDiv中
var newElement = document.createElement("p");
newElement.innerHTML = "This is a new paragraph.";
myDiv.appendChild(newElement);

```



#### 定位

以下是一些常用的getElementBy...()方法：

`getElementById() `- 通过元素ID获取某个元素节点


```
var element = document.getElementById("myElementId");
```


`getElementsByClassName()` - 通过class名称获取一组元素节点


```
var elements = document.getElementsByClassName("myClassName");
```


`getElementsByTagName() `- 通过标签名获取一组元素节点


```
var elements = document.getElementsByTagName("div");
```


⭐️`querySelector()` - 通过CSS选择器查找第一个匹配的元素节点


```
var element = document.querySelector(".myClass");
```


`querySelectorAll() `- 通过CSS选择器查找所有匹配的元素节点


```
var elements = document.querySelectorAll("p.myClass");
```


这些方法可以帮助我们在页面中快速地获取需要操作的元素节点。它们在JavaScript编程中非常常见，掌握它们可以提高我们的开发效率。


#### 获取内容

获取元素文本内容⭐️

```js
var element = document.getElementById("myElementId");
var text = element.innerHTML;
```

获取元素属性值⭐️

```js
var image = document.getElementById("myImageId");
var src = image.src;
```

#### 修改操作
以下是一些常用的JavaScript操作HTML内容的代码示例：

修改元素文本内容 `innerHTML`⭐️

```js
var element = document.getElementById("myElementId");
element.innerHTML = "Hello, World!";
``` 

修改元素属性值

```js
var image = document.getElementById("myImageId");
image.src = "new-image.png";
//oneliner
document.getElementById("myImageId").setAttribute("src", "new-image.png");

```

删除元素的某个属性⭐️

```js
var image = document.getElementById("myImageId");
image.removeAttribute("src");
```


设置元素的css

```js
var element = document.getElementById("myElementId");
element.style.color = "red";
element.style.fontSize = "20px";
//onliner
document.getElementById("myElementId").style.color = "red";
```


创建新元素并添加到成子节点⭐️

```js
var newElement = document.createElement("div");
newElement.innerHTML = "This is a new element.";
document.body.appendChild(newElement);

```

移除某个元素⭐️

```js
var elementToRemove = document.getElementById("removeMe");
elementToRemove.parentNode.removeChild(elementToRemove);
```

#### insert Adjacent HTML⭐️

`insertAdjacentHTML()`方法可以在指定位置插入HTML代码。它接收两个参数，第一个参数是指定的位置，第二个参数是要插入的HTML代码。它有以下几个位置参数：

`beforebegin` - 在元素之前插入HTML代码

`afterbegin` - 在元素内部的开始位置插入HTML代码

`beforeend` - 在元素内部的结束位置插入HTML代码

`afterend` - 在元素之后插入HTML代码

```js
var element = document.getElementById("myElementId");
element.insertAdjacentHTML("beforebegin", "<p>Hello, World!</p>");
element.insertAdjacentHTML("afterbegin", "<p>Hello, World!</p>");
element.insertAdjacentHTML("beforeend", "<p>Hello, World!</p>");
element.insertAdjacentHTML("afterend", "<p>Hello, World!</p>");
```

一个例子（点击按钮，插入Paragraph）

```js
function a(){
    var img = document.getElementsByTagName("img")[0];
    img.insertAdjacentHTML("afterend", "<p>Hello, World!</p>");
}

// html
<button onclick="a()"> aaa </button>
<img src="" alt="asdfsadf">
```
