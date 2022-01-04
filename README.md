# Android-SDK


## Including FeedMedia Library in your project

[Get the latest release version from here](https://github.com/feedfm/Android-SDK/releases)

#### Jitpack (Recommend)
[![](https://jitpack.io/v/fm.feed/AndroidSDK.svg)](https://jitpack.io/#fm.feed/AndroidSDK)


Add jitpack repository to you root build.gradle file 

```
allprojects {
 repositories {
  ...
  maven { url 'https://jitpack.io' }
 }
}
```
Then add the feed SDK to your project's build.gradle. Add **any one** of the following dependencies in your build file depending on which Exoplayer version you want to use. If you do not have any other modules using exoplayer, use the default player-sdk.

```
implementation 'fm.feed.AndroidSDK:player-sdk:6.2.0'         //contains exoplayer-core:2.16.1
implementation 'fm.feed.AndroidSDK:player-sdk-exoAmzn:6.2.0' //contains exoplayer-core:2.13.3 compatible with Amazon fire tv
implementation 'fm.feed.AndroidSDK:player-sdk-exo2118:6.2.0' //contains exoplayer-core:2.11.8
implementation 'fm.feed.AndroidSDK:player-sdk-exo2131:6.2.0' //contains exoplayer-core:2.13.1
implementation 'fm.feed.AndroidSDK:player-sdk-exo2151:6.2.0' //contains exoplayer-core:2.15.1
```


####  Maven Central 
To Build with maven central add **any one** of the following dependencies in your build file depending on which Exoplayer version you want to use. If you do not have any other modules using exoplayer, use the default player-sdk.
``` 
implementation 'fm.feed.android:player-sdk:X.X.X'           //contains exoplayer-core:2.16.1
implementation 'fm.feed.android:player-sdk-exo2118:X.X.X'  //contains exoplayer-core:2.11.8
implementation 'fm.feed.android:player-sdk-exo2131:X.X.X'  //contains exoplayer-core:2.13.1
implementation 'fm.feed.android:player-sdk-exo2151:X.X.X'  //contains exoplayer-core:2.15.1
implementation 'fm.feed.android:player-sdk-exoAmzn:x.x.x' //contains exoplayer-core:2.13.2 compatible with Amazon fire tv
```


#### To build with AAR file instead

 Add following dependencies to your app in addition to the latest AAR file from here.

```
implementation 'com.google.code.gson:gson:2.8.6'
implementation 'com.squareup.okhttp3:logging-interceptor:4.9.0'
implementation 'com.squareup.retrofit2:retrofit:2.9.0'
implementation 'com.squareup.retrofit2:converter-gson:2.9.0'
implementation 'androidx.legacy:legacy-support-v4:1.0.0'
implementation 'org.jetbrains.kotlinx:kotlinx-coroutines-core:1.5.1'
implementation 'org.jetbrains.kotlinx:kotlinx-coroutines-android:1.3.3'
```
Replace X.X with version of exoplayer you are using, and use corresponding aar.

## Getting started

#### Set credentials

To set credentials, following method should be called form the application class.

`FeedPlayerService.initialize(getApplicationContext(),"demo", "demo",false);`

    Parameters

    context - Use Application context
    token  - Your feed.fm Token
    secret - your feed.fm Secret
    useBackgroundThread - Should the library run and provide callbacks on a Background thread

#### Playing the music

To play music you will need reference to FeedAudioPlayer. To get reference to the shared instance you should call static method `getInstance` in `FeedPlayerService`
Once you have initialized the library it takes some time to contact the servers and get the music you can be notified of when the library is initialized but passing in an `AvailabilityListener`.


```Java
FeedPlayerService.getInstance(new FeedAudioPlayer.AvailabilityListener() {
           @Override
           public void onPlayerAvailable(final FeedAudioPlayer player) {

           // Set play settings in player
           // Enable crossfading
           feedAudioPlayer.setCrossFadeInEnabled(true);
           feedAudioPlayer.setSecondsOfCrossfade(4.0f);

           // Add listeners
           feedAudioPlayer.addPlayListener(MainActivity.this);
           feedAudioPlayer.addUnhandledErrorListener(MainActivity.this);
           feedAudioPlayer.addStateListener(MainActivity.this);
           feedAudioPlayer.addLikeStatusChangeListener(MainActivity.this);
           feedAudioPlayer.addOutOfMusicListener(MainActivity.this);

           player.getStationList();  // Get list of stations available
           player.play();   // Play current station


           //   optionally customize the notification style // No longer works above Api 26
            NotificationStyle ns = new NotificationStyle()
                 .setColor(Color.RED)
                 .setSmallIcon(R.drawable.my_funky_icon);
            player.setNotificationStyle(ns);

           }

           @Override
          public void onPlayerUnavailable(Exception e) {

            // No internet connection, reinitialize the library to retry
            // Music not available in this region due to copyrights. Hide music player.

          }

}
```

## Bugs!

If you find a bug, please send an email to support@feed.fm with a description
and any information you have to help us reproduce it.


