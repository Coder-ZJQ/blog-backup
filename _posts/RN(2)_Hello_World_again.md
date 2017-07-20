---
title: RN(2) Hello World again
date: 2016-10-02 20:42:26
categories: 
- Technology
- Programming
- React Native
tags: 
- React Native
---
### Hello World again
``` JavaScript
import React, { Component } from 'react';
import { AppRegistry, Text } from 'react-native';

class MyFirstReactNativeProject extends Component {
  render() {
    return (
        <Text>
          Hello World!
        </Text>
    );
  }
}

AppRegistry.registerComponent('MyFirstReactNativeProject', () => MyFirstReactNativeProject);

```
<!-- more -->
![21:27:02.jpg](http://ww3.sinaimg.cn/large/801b780agw1f8feglfjvwj20af0j574g.jpg)