# Android-SDK


## Including FeedMedia Library in your project

[Get the latest release version from here](https://github.com/feedfm/Android-SDK/releases)


####  Maven Central (Recommend)
To Build with maven central add the following dependencie in your build file.
``` 
implementation 'fm.feed.android:player-sdk:7.0.0'           //contains Media3 version 1.4.0
```

### Exoplayer versions 

The older releases for our Android SDK contained different exoplayer versions including one for fireTV. 

All the older versions can be [found here](https://central.sonatype.com/search?q=g%3Afm.feed.android++&smo=true)

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


