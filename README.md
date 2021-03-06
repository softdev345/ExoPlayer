# ExoPlayerFilter
[![Platform](https://img.shields.io/badge/platform-android-green.svg)](http://developer.android.com/index.html)
<img src="https://img.shields.io/badge/license-MIT-green.svg?style=flat">
[![API](https://img.shields.io/badge/API-16%2B-blue.svg?style=flat)](https://android-arsenal.com/api?level=16)

This library uses OpenGL Shaders to apply effects on [ExoPlayer](https://github.com/google/ExoPlayer) video at Runtime and <br> depends EXOPlayer core 2.10.2.<br>
<img src="art/art.gif" width="33.33%">

## Gradle
Step 1. Add the JitPack repository to your build file
```groovy
allprojects {
	repositories {
		...
		maven { url 'https://jitpack.io' }
	}
}
```
Step 2. Add the dependency
```groovy
    dependencies {
        implementation 'com.github.MasayukiSuda:ExoPlayerFilter:v0.2.4'
        implementation 'com.google.android.exoplayer:exoplayer-core:2.10.2'
    }
```
This library depends ExoPlayer core 2.10.2

## Sample Usage

### STEP 1
Create [SimpleExoPlayer](https://google.github.io/ExoPlayer/guide.html#creating-the-player) instance. 
In this case, play MP4 file. <br>
Read [this](https://google.github.io/ExoPlayer/guide.html#add-exoplayer-as-a-dependency) if you want to play other video formats. <br>
```JAVA
    // Produces DataSource instances through which media data is loaded.
    DataSource.Factory dataSourceFactory = new DefaultDataSourceFactory(context, Util.getUserAgent(this, "yourApplicationName"));

    // This is the MediaSource representing the media to be played.
    MediaSource videoSource = new ProgressiveMediaSource.Factory(dataSourceFactory)
           .createMediaSource(Uri.parse(Constant.STREAM_URL_MP4_VOD_LONG));

    // SimpleExoPlayer
    player = ExoPlayerFactory.newSimpleInstance(this);
    // Prepare the player with the source.
    player.prepare(videoSource);
    player.setPlayWhenReady(true);

```


### STEP 2
Create [EPlayerView](https://github.com/MasayukiSuda/ExpPlayerFilter/blob/master/epf/src/main/java/com/daasuu/epf/EPlayerView.java) and set SimpleExoPlayer to EPlayerView.

```JAVA
    ePlayerView = new EPlayerView(this);
    // set SimpleExoPlayer
    ePlayerView.setSimpleExoPlayer(player);
    ePlayerView.setLayoutParams(new RelativeLayout.LayoutParams(ViewGroup.LayoutParams.MATCH_PARENT, ViewGroup.LayoutParams.MATCH_PARENT));
    // add ePlayerView to WrapperView
    ((MovieWrapperView) findViewById(R.id.layout_movie_wrapper)).addView(ePlayerView);
    ePlayerView.onResume();
```
### STEP 3
Set Filter. Filters is [here](https://github.com/MasayukiSuda/ExpPlayerFilter/tree/master/epf/src/main/java/com/daasuu/epf/filter).<br>
Custom filters can be created by inheriting [GlFilter.java](https://github.com/MasayukiSuda/ExpPlayerFilter/blob/master/epf/src/main/java/com/daasuu/epf/filter/GlFilter.java).
```JAVA
    ePlayerView.setGlFilter(new GlSepiaFilter());
```


## Special Thanks to
* [android-gpuimage](https://github.com/CyberAgent/android-gpuimage)
