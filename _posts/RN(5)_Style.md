---
title: RN(5) Style
date: 2016-10-05 20:42:26
categories: 
- Technology
- Programming
- React Native
tags: 
- React Native
---
### Style
``` js
import React, { Component } from 'react';
import { AppRegistry, StyleSheet, Text, View } from 'react-native';

class MyFirstReactNativeProject extends Component {
  render() {
    return (
      <View>
      <Text style={styles.justRed}>just red text</Text>
      <Text style={styles.bigGreen}>just big green text</Text>
      <Text style={[styles.bigGreen, styles.justRed]}>big green then red text</Text>
      <Text style={[styles.justRed, styles.bigGreen]}>red then big green text</Text>
      </View>
    );
  }
}

const styles = StyleSheet.create({
    bigGreen : {
        color : '#00ff00',
        fontWeight : 'bold',
        fontSize : 25
    },
    justRed : {
        color : 'red',
    },

});
AppRegistry.registerComponent('MyFirstReactNativeProject', () => MyFirstReactNativeProject);

```
<!-- more -->
More info about Text style: [Text component reference](http://facebook.github.io/react-native/docs/text.html)

![20:15:56.jpg](http://ww4.sinaimg.cn/large/801b780agw1f8gi0x8d5jj20ae03yjru.jpg)