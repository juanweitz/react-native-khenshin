
# react-native-khipu

## Getting started

`$ npm install react-native-khenshin --save`

### Mostly automatic installation (RN < 0.6)

`$ react-native link react-native-khipu-browser2app`

### Manual installation

#### iOS

1. In XCode, in the project navigator, right click `Libraries` ➜ `Add Files to [your project's name]`
2. Go to `node_modules` ➜ `react-native-khenshin` and add `RNKhipu.xcodeproj`
3. In XCode, in the project navigator, select your project. Add `libRNKhipu.a` to your project's `Build Phases` ➜ `Link Binary With Libraries`
4. Run your project (`Cmd+R`)

#### Android

1. Append the following lines to `android/settings.gradle`:
```
include ':react-native-khenshin'
project(':react-native-khenshin').projectDir = new File(rootProject.projectDir, 	'../node_modules/react-native-khenshin/android')
```
2. Insert the following lines inside the dependencies block in `android/app/build.gradle`:
```
implementation 'com.browser2app:khenshin:5.4.2'
implementation project(':react-native-khenshin')
```

3. Open up `android/app/src/main/java/[...]/MainActivity.java` and add these imports at the top of the file
```
import com.browser2app.khenshin.KhenshinApplication;
import com.browser2app.khenshin.KhenshinInterface;
import com.browser2app.rn.RNKhenshinPackage;
```

4. Added The following lines / modifications in your MainApplication.java (**react-native >= 0.60.0**)

```

// IMPORTANT!!!: Added ", KhipuApplication" to the implements list
public class MainApplication extends Application implements ReactApplication, KhipuApplication {
  // --> Add the following code 
  private MainApplication mainApp;
  private RNKhipuPackage khipuPackage;

  public MainApplication() {
    mainApp = this;
  }
  
  @Override
  public KhenshinInterface getKhenshin() {
    return khipuPackage.getKhenshin();
  }
  // --> End
  
  ... 
}

```

5. Add the following code inside the `getPackages()` method
  
```
@Override
protected List<ReactPackage> getPackages() {
    ...
    khipuPackage = new RNKhipuPackage(mainApp);
    packages.add(khipuPackage);
    return packages;
}
```

6. Added **react-native.config.js** if your using **react-native > 0.60.0**

```
// react-native.config.js
module.exports = {
  dependencies: {
    'react-native-khenshin': {
      platforms: {
        android: null, // disable Android platform, other platforms will still autolink if provided
      },
    },
  },
};

```

## Usage
```javascript
import Khipu from 'react-native-khenshin';

Khipu.startPaymentById('paymentId').then(payment => console.log(payment));

```
