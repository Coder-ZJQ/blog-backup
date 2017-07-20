---
title: The let keyword in ES6
date: 2016-10-08 20:42:26
categories: 
- Technology
- Programming
- ES6
tags: 
- ES6
- let
---
### The let keyword in ES6

* `let` 命令声明的变量只在其所在的代码块内有效：

  ``` javascript
  {
    let a = 10;
    var b = 20;
  }
  a;	// a is not defined
  b;
  ```

  ``` javascript
  // use var
  var fs = [];
  for (var i = 0; i < 10; i++) {
    fs.push(() => console.log(i));
  }
  fs.forEach(f => f());
  // the log is:
  // 10
  // 10
  // 10
  // 10
  // 10
  // 10
  // 10
  // 10
  // 10
  // 10

  // use let
  var fs = [];
  for (let i = 0; i < 10; i++) {
    fs.push(() => console.log(i));
  }
  fs.forEach(f => f());
  // the log is:
  // 0
  // 1
  // 2
  // 3
  // 4
  // 5
  // 6
  // 7
  // 8
  // 9
  ```

<!-- more -->

* 不允许重复声明：

  ``` javascript
  // 1.
  function () {
    let a = 10;
    var a = 1; // 报错
  }

  // 2.
  function () {
    let a = 10;
    let a = 1; // 报错
  }

  // 3.
  function func(arg) {
    let arg; // 报错
  }

  // 4.
  function func(arg) {
    {
      let arg; // 不报错
    }
  }
  ```

  ​

``` js
// 1. 
var message = "hi";
{
  var message = "bye";
}
// "bye"
console.log(message);

// 2.
var message = "hi";
function greet(){
  var message = "bye";
}
// "hi"
console.log(message);

// 3. 
let message = "hi";
{
  let message = "bye";
}
// "hi"
console.log(message);
```

<!-- more -->

``` js
var fs = [];
for (var i = 0; i < 10; i++) {
  fs.push(() => console.log(i));
}
fs.forEach(f => f());
// 10
// 10
// 10
// 10
// 10
// 10
// 10
// 10
// 10
// 10

var fs = [];
for (let i = 0; i < 10; i++) {
  fs.push(() => console.log(i));
}
fs.forEach(f => f());
// 0
// 1
// 2
// 3
// 4
// 5
// 6
// 7
// 8
// 9
```
``` js
function varFunction() {
  var previous = 0;
  var current = 1;
  var i;
  var temp;
  for(i = 0; i < 10; i += 1) {
    temp = previous;
    previous = current;
    current = temp + current;
  }
}

// safe way
function letFunction() {
  let previous = 0;
  let current = 1;
  for(let i =0; i < 10; i += 1){
    let temp = previous;
    previous = current;
    current = temp + current;
  }
}
```
参考：[let和const命令](http://es6.ruanyifeng.com/#docs/let)

