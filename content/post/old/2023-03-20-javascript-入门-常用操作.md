+++
title = "Javascript 入门-常用操作"
description = ""
date = 2023-03-20T21:49:07+08:00
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

console.log 、 alert 、 prompt 、 confirm 、 location.href 、 setinterval 、 settimeout 、addEventListener
<!--more-->
## 常用操作
#### console log

```js
console.log('hello world');
```

#### 定时

内置函数 setinterval()、settimeout()

每秒钟打印一次hello world
```js
var timer = setInterval(function(){
    console.log('hello world');
},1000);

//停止打印
clearInterval(timer);
```

3秒钟后打印hello world
```js
setTimeout(function(){
    console.log('hello world');
},3000);
```

#### 弹窗等

```js
alert('hello world'); //弹窗
confirm('hello world'); //弹窗，点击确定返回true，点击取消返回false
prompt('hello world'); //弹窗，输入框
```


#### 重定向

location 对象用于获得当前页面的地址（URL）并把浏览器重定向到新的页面。

```js
location.href //返回当前页面的URL
location.href = 'https://cornradio.github.io'//重定向到新的页面
location.reload() //重新加载当前文档
```

#### 通过js绑定onclick事件

给btn绑定onclick事件，点击btn时打印 hello world

```js
//js 风格
var btn = document.getElementById('btn');
btn.onclick = function(){
    console.log('hello world');
}
//老派java风格
btn.addEventListener('click',function(){
    console.log('hello world');
})
//执行
btn.click();
```

注意需要将script标签放在body标签的最后面，否则会找不到元素。或者可以使用等待加载listener。

```js
//等待加载dom元素后再执行（较快速）
document.addEventListener("DOMContentLoaded", function() {
    const button = document.querySelector('button');
    button.onclick = function(){
        console.log('hello world');
    }
});

//等待将图片加载后再执行（较好写）
window.onload = function(){
    const button = document.querySelector('button');
    button.onclick = function(){
        console.log('hello world');
    }
}
```

