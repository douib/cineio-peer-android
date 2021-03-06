# Android peer client

[![Build Status](https://travis-ci.org/cine-io/cineio-peer-android.svg?branch=master)](https://travis-ci.org/cine-io/cineio-peer-android)

The android library for [cine.io peer](https://www.cine.io/products/peer).


## Installation

Add the following to your `build.gradle`.

```groovy
dependencies {
  compile 'io.cine:cineio-peer-android-sdk:0.0.6'
}
```

Ensure [Maven central](http://search.maven.org/) is included in your `build.gradle`. This should happen by default when building a project with Google's recommended Android IDE, [Android Studio](https://developer.android.com/sdk/installing/studio.html).

```
apply plugin: 'android'
buildscript {
  repositories {
    mavenCentral()
  }
}
repositories {
  mavenCentral()
}
```

Download cineio-peer-android-sdk to your application with `./gradlew build`.

## Example App

The best way to see it in action is to run the example app locally. There's some trickiness around rendering the peer videos. You can find the example Activity here: https://github.com/cine-io/cineio-peer-android/blob/master/CineIOPeerExampleApp/src/main/java/io/cine/cineiopeerclientexampleapp/exampleapp/MainActivity.java

### Running Locally

1. Clone to your local machine:

  ```
  git clone git@github.com:cine-io/cineio-peer-android.git
  cd cineio-peer-android
  ```
* Register for a public and secret key at [cine.io][cine-io]
* Open Android Studio
  * Using the Quick Start panel:
    1. click "Import project (Eclipse ADT, Gradle, etc.)"
    * Navigate to the project on your file system. It should show the Android Studio logo.
  * Using Menu:
    1. Click "File:"
    * Click "Import Project…"
    * Navigate to the project on your file system. It should show the Android Studio logo.
* Update `PUBLIC_KEY` in [MainActivity][main-activity-public-key]
* Click Run CineIOPeerExampleApp. Gradle should automatically download the dependencies and build your project.
* Select your device from the "Choose Device" panel. Click "OK"
* The app automatically connects to cine.io, starts the camera, and puts you in a room called `example`.


## Usage

### Initialization

```java
import io.cine.peerclient.CinePeerClient;

// Some other potential imports:
// import java.util.ArrayList;
// import org.webrtc.MediaStream;
```

```java
public class MainActivity extends Activity implements CinePeerCallback {
    CinePeerClient cinePeerClient;
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        //initialize the client
        String PUBLIC_KEY = "YOUR_PUBLIC_KEY";
        CinePeerClientConfig config = new CinePeerClientConfig(PUBLIC_KEY, this);
        config.setVideo(true);
        config.setAudio(true);
        //config.setSecretKey(CINEIO_SECRET_KEY); //optional
        cinePeerClient = CinePeerClient.init(config);

        //initialize the view
        CinePeerView vsv = cinePeerClient.createView();
        Runnable eglContextReadyCallback = null;
        VideoRendererGui.setView(vsv, eglContextReadyCallback);
    }
}
```

<!-- external links -->
[cine-io]:https://www.cine.io/
[main-activity-public-key]:CineIOPeerExampleApp/src/main/java/io/cine/cineiopeerclientexampleapp/exampleapp/MainActivity.java#L27
