---
title: RN(7) Layout With Flexbox
date: 2016-10-07 20:42:26
categories: 
- Technology
- Programming
- React Native
tags: 
- React Native
---
## Layout with Flexbox
### 1. Flex Direction
``` js
import React, { Component } from 'react';
import { AppRegistry, StyleSheet, View } from 'react-native';

class MyFirstReactNativeProject extends Component {
  render() {
    return (
      // Try setting `flexDirection` to `column`.
      <View style={{flex : 1, flexDirection : 'row'}}>
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
        width : 50,
        height : 50
    },
    bigBlue : {
        backgroundColor : 'steelblue',
        width : 50,
        height : 50
    }

});
AppRegistry.registerComponent('MyFirstReactNativeProject', () => MyFirstReactNativeProject);
```

<!-- more -->
![20:52:04.jpg](http://ww3.sinaimg.cn/large/801b780agw1f8gj2ieztoj20ad034dfw.jpg)

### 2. Justify Content
``` js
import React, { Component } from 'react';
import { AppRegistry, StyleSheet, View } from 'react-native';

class MyFirstReactNativeProject extends Component {
  render() {
    return (
      // Try setting `justifyContent` to `center`.
      // Try setting `flexDirection` to `row`.
      <View style={{flex : 1, flexDirection : 'row', justifyContent : 'space-between'}}>
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
        width : 50,
        height : 50
    },
    bigBlue : {
        backgroundColor : 'steelblue',
        width : 50,
        height : 50
    }

});
AppRegistry.registerComponent('MyFirstReactNativeProject', () => MyFirstReactNativeProject);
```
![20:54:00.jpg](http://ww1.sinaimg.cn/large/801b780agw1f8gj4j08nej20ad03ot8s.jpg)

### 3. Align Items
``` js

import React, { Component } from 'react';
import { AppRegistry, StyleSheet, View } from 'react-native';

class MyFirstReactNativeProject extends Component {
  render() {
    return (
      // Try setting `alignItems` to 'flex-start'
      // Try setting `justifyContent` to `flex-end`.
      // Try setting `flexDirection` to `row`.
      <View style={{flex : 1, flexDirection : 'column', justifyContent : 'center', alignItems : 'center'}}>
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
        width : 50,
        height : 50
    },
    bigBlue : {
        backgroundColor : 'steelblue',
        width : 50,
        height : 50
    }

});
AppRegistry.registerComponent('MyFirstReactNativeProject', () => MyFirstReactNativeProject);

```
![21:01:40.jpg](http://ww3.sinaimg.cn/large/801b780agw1f8gjcieq98j20af0j5mxc.jpg)

More info: [Layout Props](http://facebook.github.io/react-native/docs/layout-props.html)