## Mon 06/07/20
### Didn't find class "com.google.firebase.provider.FirebaseInitProvider" on path: DexPathList (on KitKat/ API 16)
#### React-Native-0.62 & Android

##### # App level build.gradle
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

##### # App level build.gradle
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
