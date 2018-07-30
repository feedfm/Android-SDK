# Android-SDK


## Including FeedMedia Library in your project

[Get the latest release version from here](https://github.com/feedfm/Android-SDK/releases)

####  Maven
To Build with maven add ** any one ** of the following dependencies in your build file depending on which Exoplayer version you want to use. If you do not have any other modules using exoplayer, use the default player-sdk.
```
implementation fm.feed.android:player-sdk:X.X.X
implementation fm.feed.android:player-sdk-exo260:X.X.X
implementation fm.feed.android:player-sdk-exo261:X.X.X
implementation fm.feed.android:player-sdk-exo281:X.X.X
```


#### To build with AAR file instead of Maven

 Add following dependencies to your app in addition to the latest AAR file from here.

```
  implementation 'com.google.code.gson:gson:2.8.2'
  implementation 'com.squareup.retrofit2:retrofit:2.3.0'
  implementation 'com.android.support:support-v4:27.1.1'
  implementation 'com.google.android.exoplayer:exoplayer-core:2.X.X'
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
