# Android-SDK

List of all releases can be found here

[https://github.com/feedfm/Android-SDK/releases](https://github.com/feedfm/Android-SDK/releases)


### To Build with maven add any one of the following dependencies in your build file depending on which Exoplayer version you want to use.
   `implementation fm.feed.android:player-sdk:X.X.X
    implementation fm.feed.android:player-sdk-exo260:X.X.X
    implementation fm.feed.android:player-sdk-exo261:X.X.X
    implementation fm.feed.android:player-sdk-exo281:X.X.X`


### To build with AAR file instead of Maven add following dependencies to your app.

  `implementation 'com.google.code.gson:gson:2.8.2'
   implementation 'com.squareup.retrofit2:retrofit:2.3.0'
   implementation 'com.squareup.retrofit2:converter-gson:2.3.0'
   implementation 'com.android.support:support-v4:27.1.1'
   implementation 'com.google.android.exoplayer:exoplayer-core:2.X.X'

   Replace X.X with version of exoplayer you are using, and use corresponding aar.
