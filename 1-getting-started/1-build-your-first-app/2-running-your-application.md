
Running Your Application
========================

Before you run your app, you should be aware of a few directories and files in the InAiR project.

### `AndroidManifest.xml`
>The manifest file describes the fundamental characteristics of the app and defines each of its components. It mostly follows Google's [Android](http://developer.android.com/guide/topics/manifest/manifest-intro.html) declarations except for some few minor details.

>InAiR App requires a special `inair.application` permission, manifest files without this permission won't be recognized by InAiR Launcher.

> ```xml
<manifest xmlns:android="http://schemas.android.com/apk/res/android" ... >
  <uses-permission android:name="inair.application" />
  ...
</manifest>
```

### `src/`
>Directory for your app's main source files.

###`res/`
>Contains several sub-directories for app resources same as in an Android app. Here are just a few:
####`layout/`
>>Directory for files that define your app's user interface.
>
####`drawable/`
>>Directory for drawable objects (such as bitmaps) to be used within InAiR App, including the logo for the app.
>
####`values/`
>>Directory for other various XML files that contain a collection of resources, such as string and color definitions.
>

Run on a Real Device
--------------------
If you have an InAiR device, here's how to install and run your app.

###Set up your device
Plug in your device to your development machine with a USB cable. If you're developing on Windows, you might need to install the appropriate USB driver for your device. For help installing drivers, see the [OEM USB Drivers](http://developer.android.com/tools/extras/oem-usb.html) document.

### Run the app from Android Studio
1. Select one of your project's files and click __Run__ ![Run](http://developer.android.com/images/tools/as-run.png) from the toolbar.
2. In the __Choose Device__ window that appears, select the __Choose a running device__ radio button, select your device, and click __OK__.
Android Studio installs the app on your connected device and starts it.

### Run the app from a command line
Open a command-line and navigate to the root of your project directory. Use Gradle to build your project in debug mode, invoke the `assembleDebug` build task using the Gradle wrapper script (`gradlew assembleRelease`).

This creates your debug `.apk` file inside the module `build/` directory, named `HelloWorld-debug.apk`.

On Windows platforms, type this command:

```
> gradlew.bat assembleDebug
```

On Mac OS and Linux platforms, type these commands:

```
$ chmod +x gradlew
$ ./gradlew assembleDebug
```

After you build the project, the output APK for the app module is located in `app/build/outputs/apk/`

>__Note__: The first command (chmod) adds the execution permission to the Gradle wrapper script and is only necessary the first time you build this project from the command line.

Make sure the Android SDK `platform-tools/` directory is included in your `PATH` environment variable, then execute:

```
adb install app/build/outputs/HelloWorld-debug.apk
```

On your device, locate `HelloWorld` and open it.

That's how you build and run your InAiR app on a device! To start developing, continue to the [next lesson](3-build-a-simple-slideshow.md).

Run on the Emulator
-------------------

Not supported, yet.