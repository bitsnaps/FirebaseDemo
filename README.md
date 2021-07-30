# Firebase Demo

1- Create Firebase account on google
2- Create a new project (set name, options...)
3- Download the json from Firebase console to your `app/google-services.json`
4- Configure your app with the following:

In `build.gradle` of your Project:
```groovy
buildscript {
    ...
    dependencies {
        classpath 'com.android.tools.build:gradle:3.3.1' // the last working version with Gradle v4.1
        classpath 'com.google.gms:google-services:4.3.3' // This will parse firebase json downloaded file
    }
}
```
In `app/build.gradle` of your App:
```groovy

// Add at the top
apply plugin: 'com.google.gms.google-services'

android {
    compileSdkVersion 28 // or higher
    defaultConfig {
        ...
        minSdkVersion 16 // or higher
        // If your minSdkVersion >= 21 , MultiDex is enabled by default and you do not need the multidex library.
        multiDexEnabled true
        ...
    }
 }

dependencies {
    // Add your firebase features...
    implementation 'com.google.firebase:firebase-auth:21.0.1'
    implementation 'com.google.firebase:firebase-firestore:23.0.3'
    implementation 'com.google.firebase:firebase-storage:20.0.0'
    implementation 'com.google.firebase:firebase-database:20.0.1'

    // or if you're using Gradle >= 5 use "Bill of Materials" you won't need to specify firebase-version after that
    //    implementation platform('com.google.firebase:firebase-bom:28.3.0')
    //    implementation 'com.google.firebase:firebase-auth'
    //    implementation 'com.google.firebase:firebase-firestore'

    // MultiDex required for Android 5.0 (API <= 21) or lower
    implementation 'com.android.support:multidex:2.0.1'

    //...
}

```

5- Now you can start using Firebase:
```
import com.google.firebase.FirebaseApp;
...

// This can be done in onCreate() of your MainActivity

FirebaseApp app = FirebaseApp.getInstance();
String appName = app.getOptions().getProjectId();
Log.d(getApplicationContext().getPackageName(), "Application Name: "  +appName);

```
