---
title: Using a ListView
date: 2016-10-25 13:57:17
categories: 
- Technology
- Programming
- React Native
tags: 
- React Native
- ListView
---
``` jsx
import React, { Component } from 'react';
import {
  AppRegistry,
  View,
  Text,
  Image,
  ScrollView
} from 'react-native';
export default class AwesomeProject extends Component {
  render() {
    return (
      <ScrollView style={{marginTop:20}}>
      <Text style={{fontSize:20}}>
      哈哈，我在上面。。。
      </Text>
      <Image source={require("./icon.png")}/>
      <Image source={require("./icon.png")}/>
      <Image source={require("./icon.png")}/>
      <Image source={require("./icon.png")}/>
      <Image source={require("./icon.png")}/>
      <Image source={require("./icon.png")}/>
      <Image source={require("./icon.png")}/>
      <Image source={require("./icon.png")}/>
      <Image source={require("./icon.png")}/>
      <Image source={require("./icon.png")}/>
      <Image source={require("./icon.png")}/>
      <Image source={require("./icon.png")}/>
      <Image source={require("./icon.png")}/>
      <Image source={require("./icon.png")}/>
      <Text style={{fontSize:20}}>
      哈哈，我在中间。。。
      </Text>
      <Image source={require("./icon.png")}/>
      <Image source={require("./icon.png")}/>
      <Image source={require("./icon.png")}/>
      <Image source={require("./icon.png")}/>
      <Image source={require("./icon.png")}/>
      <Image source={require("./icon.png")}/>
      <Image source={require("./icon.png")}/>
      <Image source={require("./icon.png")}/>
      <Image source={require("./icon.png")}/>
      <Image source={require("./icon.png")}/>
      <Image source={require("./icon.png")}/>
      <Image source={require("./icon.png")}/>
      <Image source={require("./icon.png")}/>
      <Image source={require("./icon.png")}/>
      <Image source={require("./icon.png")}/>
      <Image source={require("./icon.png")}/>
      <Image source={require("./icon.png")}/>
      <Image source={require("./icon.png")}/>
      <Text style={{fontSize:20}}>
      哈哈，我在下面。。。
      </Text>
      </ScrollView>
    );
  }
}
AppRegistry.registerComponent('AwesomeProject', () => AwesomeProject);
```
<!-- more -->

![14:01:53.jpg](http://ww3.sinaimg.cn/large/801b780agw1f94h878nkij20af0j5t9c.jpg)