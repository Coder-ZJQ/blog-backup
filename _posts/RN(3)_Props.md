---
title: RN(3) Props
date: 2016-10-03 20:42:26
categories: 
- Technology
- Programming
- React Native
tags: 
- React Native
---
## Props

### Bananas
``` js
import React, { Component } from 'react';
import { AppRegistry, Image } from 'react-native';

class MyFirstReactNativeProject extends Component {
  render() {
    let pic = {
        uri : 'https://upload.wikimedia.org/wikipedia/commons/d/de/Bananavarieties.jpg'
    };
    return (
        <Image source={pic} style={{width: 193, height: 110}}/>
    );
  }
}

AppRegistry.registerComponent('MyFirstReactNativeProject', () => MyFirstReactNativeProject);

```
<!-- more -->
![21:31:45.jpg](http://ww4.sinaimg.cn/large/801b780agw1f8felhoiq7j20ad064wes.jpg)

### LotsOfGreetings
``` js
import React, { Component } from 'react';
import { AppRegistry, Text, View } from 'react-native';

class MyFirstReactNativeProject extends Component {
  render() {
    return (
        <View style={{alignItems:'center'}}>
        <Greeting name='Joker'/>
        <Greeting name='Peter'/>
        <Greeting name='Mike'/>
        </View>
        );
  }
}
class Greeting extends Component {
    render() {
        return (
            <Text>
            Hello {this.props.name}! 
            </Text>
            );
    }
}

AppRegistry.registerComponent('MyFirstReactNativeProject', () => MyFirstReactNativeProject);

```
![22:02:07.jpg](http://ww1.sinaimg.cn/large/801b780agw1f8ffh3akxfj20ac043q32.jpg)