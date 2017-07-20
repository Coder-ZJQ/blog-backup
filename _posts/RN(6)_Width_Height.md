---
title: RN(6) Width Height
date: 2016-10-06 20:42:26
categories: 
- Technology
- Programming
- React Native
tags: 
- React Native
---
## Width & Height
### 1. Fixed Dimensions
``` js

import React, { Component } from 'react';
import { AppRegistry, StyleSheet, Text, View } from 'react-native';

class MyFirstReactNativeProject extends Component {
  render() {
    return (
      <View>
      <View style={styles.smallBlue} />
      <View style={styles.middleBlue} />
      <View style={styles.bigBlue} />
      </View>
    );
  }
}

const styles = StyleSheet.create({
    smallBlue : {
        backgroundColor : 'powderblue',
        width : 50,
        height : 50
    },
    middleBlue : {
        backgroundColor : 'skyblue',
        width : 100,
        height : 100
    },
    bigBlue : {
        backgroundColor : 'steelblue',
        width : 150,
        height : 150
    }

});
AppRegistry.registerComponent('MyFirstReactNativeProject', () => MyFirstReactNativeProject);

```

<!-- more -->
![20:26:58.jpg](http://ww1.sinaimg.cn/large/801b780agw1f8giceqwifj20ae09n3yn.jpg)

### 2. Flex Dimensions
``` js
import React, { Component } from 'react';
import { AppRegistry, StyleSheet, Text, View } from 'react-native';

class MyFirstReactNativeProject extends Component {
  render() {
    return (
      <View style={{flex : 1}}>
        <View style={styles.smallBlue} />
        <View style={styles.middleBlue} />
        <View style={styles.bigBlue} />
      </View>

    );
  }
}

const styles = StyleSheet.create({
    smallBlue : {
        backgroundColor : 'powderblue',
        flex : 1
    },
    middleBlue : {
        backgroundColor : 'skyblue',
        flex : 2
    },
    bigBlue : {
        backgroundColor : 'steelblue',
        flex : 3
    }

});
AppRegistry.registerComponent('MyFirstReactNativeProject', () => MyFirstReactNativeProject);

```
![20:48:39.jpg](http://ww2.sinaimg.cn/large/801b780agw1f8giyymu6fj20af0j53yp.jpg)