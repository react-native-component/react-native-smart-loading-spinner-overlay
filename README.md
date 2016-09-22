# react-native-smart-loading-spinner-overlay

[![npm](https://img.shields.io/npm/v/react-native-smart-loading-spinner-overlay.svg)](https://www.npmjs.com/package/react-native-smart-loading-spinner-overlay)
[![npm](https://img.shields.io/npm/dm/react-native-smart-loading-spinner-overlay.svg)](https://www.npmjs.com/package/react-native-smart-loading-spinner-overlay)
[![npm](https://img.shields.io/npm/dt/react-native-smart-loading-spinner-overlay.svg)](https://www.npmjs.com/package/react-native-smart-loading-spinner-overlay)
[![npm](https://img.shields.io/npm/l/react-native-smart-loading-spinner-overlay.svg)](https://github.com/react-native-component/react-native-smart-loading-spinner-overlay/blob/master/LICENSE)

A smart loading spinner overlay for React Native apps, written in JS for cross-platform support.
It works on iOS and Android.

This component is compatible with React Native 0.25 and newer.

## Preview

![react-native-smart-loading-spinner-overlay-preview-ios][1]
![react-native-smart-loading-spinner-overlay-preview-android][2]

## Installation

```
npm install react-native-smart-loading-spinner-overlay --save
```

## Full Demo

see [ReactNativeComponentDemos][0]

## Usage

Install the loading-spinner-overlay from npm with `npm install react-native-smart-loading-spinner-overlay --save`.
Then, require it from your app's JavaScript files with `import loading-spinner-overlay from 'react-native-smart-loading-spinner-overlay'`.

```js

import React, {
    Component,
} from 'react'
import {
    View,
} from 'react-native'

import Button from 'react-native-smart-button'
import TimerEnhance from 'react-native-smart-timer-enhance'
import Toast from 'react-native-smart-loading-spinner-overlay'

class LoadingSpinnerOverLayDemo extends Component {

    constructor(props) {
        super(props)
        this.state = {}
    }

    render() {
        return (
            <View style={{ paddingTop: 64, flex: 1, backgroundColor: '#fff',}}>
                <Button
                    onPress={this._showModalLoadingSpinnerOverLay}
                    touchableType={Button.constants.touchableTypes.fadeContent}
                    style={{margin: 10, height: 40, backgroundColor: 'red', borderRadius: 3, borderWidth: StyleSheet.hairlineWidth, borderColor: 'red', justifyContent: 'center',}}
                    textStyle={{fontSize: 17, color: 'white'}}
                >
                    show modal loading spinner (模态)
                </Button>
                <Button
                    onPress={this._showPartModalLoadingSpinnerOverLay}
                    touchableType={Button.constants.touchableTypes.highlight}
                    underlayColor={'#C90000'}
                    style={{margin: 10, justifyContent: 'center', height: 40, backgroundColor: 'red', borderRadius: 3, borderWidth: StyleSheet.hairlineWidth, borderColor: 'red', justifyContent: 'center',}}
                    textStyle={{fontSize: 17, color: 'white'}}
                >
                    [part modal]can click header (导航栏允许点击)
                </Button>
                <Button
                    onPress={this._showNoModalLoadingSpinnerOverLay}
                    touchableType={Button.constants.touchableTypes.blur}
                    style={{margin: 10, justifyContent: 'center', height: 40, backgroundColor: 'red', borderRadius: 3, borderWidth: StyleSheet.hairlineWidth, borderColor: 'red', justifyContent: 'center',}}
                    textStyle={{fontSize: 17,  color: 'white'}}
                >
                    show no modal loading spinner (非模态)
                </Button>

                <Button
                    onPress={this._showImmediateLoadingSpinnerOverLayAndImmediateHide}
                    touchableType={Button.constants.touchableTypes.fade}
                    style={{margin: 10, justifyContent: 'center', height: 40, backgroundColor: 'red', borderRadius: 3, borderWidth: StyleSheet.hairlineWidth, borderColor: 'red', justifyContent: 'center',}}
                    textStyle={{fontSize: 17,  color: 'white'}}
                >
                    show and hide immediately (无渐变)
                </Button>

                <Button
                    onPress={this._showModal_2_LoadingSpinnerOverLay}
                    touchableType={Button.constants.touchableTypes.fadeContent}
                    style={{margin: 10, height: 40, backgroundColor: 'red', borderRadius: 3, borderWidth: StyleSheet.hairlineWidth, borderColor: 'red', justifyContent: 'center',}}
                    textStyle={{fontSize: 17, color: 'white'}}
                >
                    custom content (自定义内容)
                </Button>

                <LoadingSpinnerOverlay
                    ref={ component => this._modalLoadingSpinnerOverLay = component }/>
                <LoadingSpinnerOverlay
                    ref={ component => this._partModalLoadingSpinnerOverLay = component }
                    modal={true}
                    marginTop={64}/>
                <LoadingSpinnerOverlay
                    ref={ component => this._LoadingSpinnerOverLay = component }
                    modal={false}/>
                <LoadingSpinnerOverlay
                    ref={ component => this._modalImmediateLoadingSpinnerOverLay = component }/>
                <LoadingSpinnerOverlay
                    ref={ component => this._modal_2_LoadingSpinnerOverLay = component }>
                    {this._renderActivityIndicator()}
                </LoadingSpinnerOverlay>
            </View>
        )
    }




    _showModalLoadingSpinnerOverLay = () => {
        this._modalLoadingSpinnerOverLay.show()
        //simulate http request
        this.setTimeout( () => {
            this._modalLoadingSpinnerOverLay.hide()
        }, 3000)
    }

    _showPartModalLoadingSpinnerOverLay = () => {
        this._partModalLoadingSpinnerOverLay.show()
        //simulate http request
        this.setTimeout( () => {
            this._partModalLoadingSpinnerOverLay.hide()
        }, 3000)
    }

    _showNoModalLoadingSpinnerOverLay = () => {
        this._LoadingSpinnerOverLay.show()
        //simulate http request
        this.setTimeout( () => {
            this._LoadingSpinnerOverLay.hide()
        }, 3000)
    }

    _showImmediateLoadingSpinnerOverLayAndImmediateHide = () => {
        this._modalImmediateLoadingSpinnerOverLay.show({
            duration: 0,
            children: this._renderActivityIndicator(),
        })
        //simulate http request
        this.setTimeout( () => {
            this._modalImmediateLoadingSpinnerOverLay.hide({
                duration: 0,
            })
        }, 3000)
    }

    _showModal_2_LoadingSpinnerOverLay = () => {
        this._modal_2_LoadingSpinnerOverLay.show()
        //simulate http request
        this.setTimeout( () => {
            this._modal_2_LoadingSpinnerOverLay.hide()
        }, 3000)
    }

    _renderActivityIndicator() {
        return ActivityIndicator ? (
            <ActivityIndicator
                animating={true}
                color={'#ff0000'}
                size={'small'}/>
        ) : Platform.OS == 'android' ?
            (
                <ProgressBarAndroid
                    color={'#ff0000'}
                    styleAttr={'small'}/>

            ) :  (
            <ActivityIndicatorIOS
                animating={true}
                color={'#ff0000'}
                size={'small'}/>
        )
    }

}


export default TimerEnhance(LoadingSpinnerOverLayDemo)
```

## Props

Prop             | Type   | Optional | Default          | Description
---------------- | ------ | -------- | ---------------- | -----------
style            | style  | Yes      |                  | see [react-native documents][3]
overlayStyle     | style  | Yes      |                  | see [react-native documents][3]
duration         | number | Yes      | 255              | determine the duration of loading-spinner-overlay animation
delay            | number | Yes      | 0                | determine the delay of loading-spinner-overlay animation
marginTop        | number | Yes      | 0                | determine the marginTop of the root container view, it is used when the modal prop is false
modal            | bool   | Yes      | true             | determine if the modal will be used

## Method

* show({modal, marginTop, children, duration, easing, delay, animationEnd,})

    * modal: determine if the modal will be used
    * marginTop: determine the marginTop of the root container view, it is used when the modal prop is false
    * children: determine the children of loading-spinner-overlay
    * duration: determine the duration of animation
    * easing: determine the easing of animation
    * delay: determine the delay of animation
    * animationEnd: determine the callback when animation is end

* hide({duration, easing, delay, animationEnd,})

    * duration: determine the duration of animation
    * easing: determine the easing of animation
    * delay: determine the delay of animation
    * animationEnd: determine the callback when animation is end

[0]: https://github.com/cyqresig/ReactNativeComponentDemos
[1]: http://cyqresig.github.io/img/react-native-smart-loading-spinner-overlay-preview-ios-v1.0.0.gif
[2]: http://cyqresig.github.io/img/react-native-smart-loading-spinner-overlay-preview-android-v1.0.0.gif
[3]: https://facebook.github.io/react-native/docs/style.html
[4]: http://facebook.github.io/react-native/docs/text.html#style