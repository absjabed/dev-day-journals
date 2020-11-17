## Tue 17/11/2020
### ./gradlew command not found or ./gradlew clean execution permission denied
#### React-Native Android on Ubuntu

##### On Ubuntu Following this guide work for me `cd android` -> `chmod +x gradlew` -> `./gradlew clean` -> `cd .. && react-native run-android`

 [./gradlew command not found](https://stackoverflow.com/a/64278631/5277438)
 
---

## Tue 17/11/2020
### adb server version (41) doesn’t match this client (39); killing
#### React-Native Android on Ubuntu

##### Check current adb version in available Sdk
```sh
$ adb –-version
Android Debug Bridge version 1.0.39
Version 1:8.1.0+r23-5~18.04
Installed as /usr/lib/android-sdk/platform-tools/adb
```
##### To fix:
```sh
root@super:/home/jbd$ /home/jbd/Android/Sdk/platform-tools/adb --version
 Android Debug Bridge version 1.0.41
 Version 29.0.6-6198805
 Installed as /home/jbd/Android/Sdk/platform-tools/adb
 
 root@super:/home/jbd$ cp /home/jbd/Android/Sdk/platform-tools/adb /usr/bin/adb
 root@super:/home/jbd$ adb --version
 Android Debug Bridge version 1.0.41
 Version 29.0.6-6198805
 Installed as /usr/bin/adb

#adb devices
 List of devices attached
 330061df2d92b225    device
 emulator-5554    device

#adb -s 330061df2d92b225 shell
 OnePlus6:/
```

---

## Wed 08/07/20
### Custom Fonts in React Native
#### React Native version > 0.60

##### You might get warning like below if you use `rnpm` on react native version > 0.60
  ```
  warn Your project is using deprecated "rnpm" config that will stop working from next release. 
  Please use a "react-native.config.js" file to configure the React Native CLI.
  ```
  - create an `assets` folder in the root of your project. Then create a `fonts` folder inside it. 
    Finally, copy your font files into the `fonts` folder.
  - Create a file in the root folder of your project called `react-native.config.js`, and add the following:
  
    ```
    module.exports = {
      assets: ['./assets/fonts/']
    };
    
    //Then, run the following command in your terminal:
    // # react-native link
    ```
   - On Android, it will copy the font files to `/android/app/src/main/assets/fonts`. 
      On iOS, it will modify your Info.plist file to include references to your fonts, similar to this:
    
      ```
        <key>UIAppFonts</key>
        <array>
           <string>Ubuntu-Bold.ttf</string>
        </array>
      ```
    
   - Use the Font
   
      ```
      const styles = StyleSheet.create({
          custom: {
              fontFamily: 'Ubuntu-Bold',
              fontSize: 32
          }
        });
      ```
      
   - To reduce the risk of confusion, try to name your file the same way as it shows up in FontBook (macOS) when you double-click on it. Failing that, you can always use platform specific code, like this:
   
      ```
        const styles = StyleSheet.create({
            custom: {
                fontFamily: Platform.OS === "ios" ? 'AsCalledByFontBook' : 'some_filename.ttf',
                fontSize: 32
            }
        });
      ```
   - Done 🎉🎉🎉
   
 [Using Custom Fonts in React Native](https://www.youtube.com/watch?v=60XGVZffPeE)

---

## Mon 06/07/20
### Didn't find class "com.google.firebase.provider.FirebaseInitProvider" on path: DexPathList (on KitKat/ API 16)
#### React-Native-0.62 & Android

##### # App level build.gradle at `/android/app/build.gradle`
```sh
  android{
    ...
    defaultConfig{
          applicationId "com.ReactNativeApp_proj"
          minSdkVersion rootProject.ext.minSdkVersion
          targetSdkVersion rootProject.ext.targetSdkVersion
          versionCode 1
          versionName "1.0"
          multiDexEnabled true // <- Add this line
    }
    ...
  }
  
  dependencies{
    ...
    implementation 'com.android.support:multidex:1.0.3' // <- And this line
    ...
  }
```

##### # Change `MainApplication.java` at `src/main/java/com/yourapp/MainApplication.java`
```java
  ...
  import androidx.multidex.MultiDex;
  ...
  
  public class MainApplication extends Application implements ReactApplication {
    ...
    
      @Override 
      protected void attachBaseContext(Context base) {
          super.attachBaseContext(base);
          MultiDex.install(this);
      }
      
    ...
  
  }
  
```

[solving app crash at start with android4.*](https://github.com/invertase/react-native-firebase/issues/2147#issue-446576717)

[App crashing in 4.4.4 and Working fine in 6.0.1](https://github.com/firebase/quickstart-android/issues/105#issuecomment-449877090)

[Didn't find class "com.google.firebase.provider.FirebaseInitProvider"](https://stackoverflow.com/a/43318117/5277438)

---

### Unable to create application com.app.MainApplication: java.lang.RuntimeException: Requested enabled DevSupportManager, but DevSupportManagerImpl class was not found or could not be created.
#### React-Native-0.62 & Android
#### Flipper related issue

##### # App level build.gradle at `/android/app/build.gradle`
```sh
  dependencies{
  
    implementation fileTree(dir: "libs", include: ["*.jar"])
    //noinspection GradleDynamicVersion
    implementation "com.facebook.react:react-native:+"
    implementation 'androidx.appcompat:appcompat:1.1.0-rc01'

    debugImplementation("com.facebook.flipper:flipper:${FLIPPER_VERSION}") {
      exclude group:'com.facebook.fbjni'
    }

    debugImplementation("com.facebook.flipper:flipper-network-plugin:${FLIPPER_VERSION}") {
        exclude group:'com.facebook.flipper'
        exclude group:'com.squareup.okhttp3', module:'okhttp'     // <- Add this line
    }
    
    debugImplementation("com.facebook.flipper:flipper-fresco-plugin:${FLIPPER_VERSION}") {
        exclude group:'com.facebook.flipper'
    }
    ...
  }
```

[0.62.0 Android API level 16 broken: Flipper](https://github.com/facebook/react-native/issues/28481#issuecomment-645546195)

---
