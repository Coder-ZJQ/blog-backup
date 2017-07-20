---
title: RN(4) State
date: 2016-10-04 20:42:26
categories: 
- Technology
- Programming
- React Native
tags: 
- React Native
---
### State
``` js
import React, { Component } from 'react';
import { AppRegistry, Text, View } from 'react-native';
class Blink extends Component {
    constructor(props) {
        super(props);
        this.state = {showText: true};
        setInterval(() => {
            this.setState({showText: !this.state.showText});
        }, 1000);
    }
    render() {
        let display = this.state.showText ? this.props.text : '';
        return (
            <Text>{display}</Text>
            );
    }
}
class MyFirstReactNativeProject extends Component {
  render() {
    return (
      <View>
        <Blink text='I love to blink' />
        <Blink text='Yes blinking is so great' />
        <Blink text='Why did they ever take this out of HTML' />
        <Blink text='Look at me look at me look at me' />
      </View>
    );
  }
}
AppRegistry.registerComponent('MyFirstReactNativeProject', () => MyFirstReactNativeProject);
```
<!-- more -->
![animation.gif](http://ww2.sinaimg.cn/large/801b780agw1f8fgfoemvsg20ac03yaa4.gif)