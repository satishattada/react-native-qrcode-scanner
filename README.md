# react-native-infy-qrcode-scanner

[![npm version](https://badge.fury.io/js/react-native-infy-qrcode-scanner.svg)](https://badge.fury.io/js/react-native-infy-qrcode-scanner) [![Backers on Open Collective](https://opencollective.com/react-native-infy-qrcode-scanner/backers/badge.svg)](#backers) [![Sponsors on Open Collective](https://opencollective.com/react-native-infy-qrcode-scanner/sponsors/badge.svg)](#sponsors)

QR code scanner component is used for React Native applications, built on top of [react-native-infy-camera by Satish Attada](https://github.com/satishattada/react-native-camera)

This prototype will used as barcode scanner and was built for QR code scanning

## Getting started

### Requirements

#### Android 10

With Android 10 and higher you should add "Vibration" permission on your AndroidManifest.xml of your project. This should be found in your `android/app/src/main/AndroidManifest.xml` Add the following:

```
<uses-permission android:name="android.permission.VIBRATE"/>
```
You should add "missingDimensionStrategy" defaultConfig to the 'react-native-infy-camera' by placing it  to 'general', this should be found in `android/app/build.gradle` of your project, 
please add the following:
```
android {
  ...
  defaultConfig {
    ...
    missingDimensionStrategy 'react-native-infy-camera', 'general' 
  }
}
```

#### react-native-infy-camera
There is a dependency with react-native-infy-camera to this package.
Install [react-native-infy-camera](https://github.com/satishattada/react-native-camera) 

1. `npm install react-native-infy-camera --save`
2. `react-native link react-native-infy-camera`


### To install and start react-native-infy-qrcode-scanner:

1. `npm i react-native-infy-qrcode-scanner`
2. `react-native link react-native-infy-qrcode-scanner`

_**Please note**: If you are using react-native version 0.60 or above, then please ignore react-native link._

#### react-native-permissions

You should also need to install react-native-permissions to handle camera related permissions

1. `npm install react-native-permissions --save`
2. `react-native link react-native-permissions`

_**Please note**: If you are using react-native version 0.60 or above, then please ignore react-native link._

_**Please note**: You may also need to reset your simulator/emulator data after adding the permissions `Device -> Erase All Content and Settings...` ._

## Usage

To use react-native-infy-qrcode-scanner, `import` the `react-native-infy-qrcode-scanner` module and use the `<QRCodeScanner />` tag. 
Here is an example of basic usage:

```js
'use strict';

import React, { Component } from 'react';

import {
  AppRegistry,
  StyleSheet,
  Text,
  TouchableOpacity,
  Linking
} from 'react-native';

import QRCodeScanner from 'react-native-infy-qrcode-scanner';
import { RNCamera } from 'react-native-infy-camera';

class ScanQRComponent extends Component {
  onSuccess = e => {
    Linking.openURL(e.data).catch(err =>
      console.error('Error', err)
    );
  };

  render() {
    return (
      <QRCodeScanner
        onRead={this.onSuccess}
        flashMode={RNCamera.Constants.FlashMode.torch}
        topContent={
          <Text style={styles.centerText}>
            Go to{' '}
            <Text style={styles.textBold}>https://www.qr-code-generator.com/</Text> 
            and add some TEXT QR code generator on
            your computer and scan the QR code.
          </Text>
        }
        bottomContent={
          <TouchableOpacity style={styles.buttonTouchable}>
            <Text style={styles.buttonText}>Confirm</Text>
          </TouchableOpacity>
        }
      />
    );
  }
}

const styles = StyleSheet.create({
  centerText: {
    flex: 1,
    fontSize: 16,
    padding: 20,
    color: '#eee'
  },
  textBold: {
    fontWeight: '600',
    color: '#000'
  },
  buttonText: {
    fontSize: 21,
    color: '#009b00'
  },
  buttonTouchable: {
    padding: 10
  }
});

AppRegistry.registerComponent('default', () => ScanQRComponent);
```

## Methods

#### `reactivate()`

To enable the scan again, use this method
`<QRCodeScanner ref={(node) => { this.scanner = node }}>` and call `this.scanner.reactivate()`

## Props

#### `onRead` (required)

propType: `func.isRequired`
default: `(e) => (console.log('QR code scanned!', e))`
After scanning the QR code, onRead method is used to read the QR code and this method is required.

#### `fadeIn`

propType: `bool`
default: `true`

Camera view fades after scanning, it is like animation fading.

#### `reactivate`

propType: `bool`
default: `false`

After scanning the `QRCodeScanner`, You cannot scan another, if set to `false`
if set to `true` it will reactivate the scanning

#### `reactivateTimeout`

propType: `number`
default: `0`

reactivate with some time (in milliseconds). `reactivateTimeout` is used, by default it is `0`

#### `cameraTimeout`
propType: `number`
default: `0`

This is used to take some time ( in milliseconds) before the `QRCodeScanner` displayed.

#### `cameraTimeoutView`

propType: `element`

Pass component to show when the camera is inactive in `cameraTimeout` (another prop) milliseconds. If the `cameraTimeout` is 0 or not specified, this prop will be never used.

#### `flashMode`

propType: `RNCamera.Constants.FlashMode`
default: `RNCamera.Constants.FlashMode.auto`

**Flash modes**

- `RNCamera.Constants.FlashMode.off` turns it to off.
- `RNCamera.Constants.FlashMode.on` means camera flash will be used for all photos.
- `RNCamera.Constants.FlashMode.auto` used to flash automatically based on lightening conditions.
- `RNCamera.Constants.FlashMode.torch` on camera open, light will be opened for scanning.


#### `topContent`

propType: `oneOfType([ PropTypes.element, PropTypes.string, ])`

This us used to render any additional content at the top of the camera view.

#### `bottomContent`

propType: `oneOfType([ PropTypes.element, PropTypes.string, ])`

This us used to render any additional content at the bottom of the camera view.

#### `containerStyle`

propType: `any`

This us used pass styling for the outermost container. Useful for adding margin/padding to account for navigation bar.

#### `cameraStyle`

propType: `any`

This us used to pass or overwrite styling for the camera window rendered.

#### `cameraContainerStyle`

propType: `any`

This us used to pass or overwrite styling for the camera container (view) window rendered.

#### `topViewStyle`

propType: `any`

This us used to pass or overwrite styling for the `<View>` that contains the `topContent` prop.

#### `bottomViewStyle`

propType: `any`

This us used to pass or overwrite styling for the `<View>` that contains the `bottomContent` prop.

#### `showMarker`

propType: `boolean`
default: `false`

This us used to show marker on the camera scanning window.

#### `customMarker`

propType: `element`

This us used for custom marker.

#### `markerStyle`

propType: `any`

This us used to add custom styling to the default marker.

#### `notAuthorizedView`

propType: `element`

Pass a RN element/component to use it when no permissions given to the camera (iOS only).

#### `cameraType`

propType: `oneOf(['front', 'back'])`
default: `'back'`

This us used to control which camera to use for scanning QR codes, defaults to rear camera.

#### `checkAndroid6Permissions`

propType: `bool`
default: `false`

This us used to enable permission checking on Android 6

#### `permissionDialogTitle`

propType: `string`
default: `'Info'`

This us used to set permission dialog title (Android only).

#### `permissionDialogMessage`

propType: `string`
default: `'Need camera permission'`

This us used to set permission dialog message (Android only).

#### `buttonPositive`

propType: `string`
default: `'OK'`

This us used to set permission dialog button text (Android only).

#### `cameraProps`

propType: `object`

Properties to be passed to the `Camera` component.


## License

See [LICENSE.md](LICENSE.md)

