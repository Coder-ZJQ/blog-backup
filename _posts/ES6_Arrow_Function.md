---
title: Arrow Function => in ES6
date: 2016-10-01 20:42:26
categories: 
- Technology
- Programming
- ES6
tags: 
- ES6
- Arrow Function
---

## Arrow Function => in ES6
### Arrow Function syntax
``` js
var greet = function (message, name) {
  return message + name;
}

// arrow function

var arrowGreet1 = (message, name) => {
  return message + name;
}

var arrowGreet2 = (message, name) => message + name;

var square = x => x ^ 2;
```
<!-- more -->
### `this` in Arrow Function syntax
``` js
var deliveryBoy = {
  name: "Joker",
  handleMessage: function (message, handler) {
    return handler(message);
  },
  receive: function () {
    var that = this;
    this.handleMessage("Hello, ", function (message) {
      that.name;   
      console.log(message + that.name);
    })
  }
}
deliveryBoy.receive();

// arrow function

var arrowDelieveryBoy = {
  name: "Joker",
  handleMessage:  (message, handler) => handler(message),
  receive: function () {
    this.handleMessage("Hello, ", message => console.log(message + this.name));
  }
}
arrowDelieveryBoy.receive();
```