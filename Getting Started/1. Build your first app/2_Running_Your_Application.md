Before you run your app, you should be aware of a few directories and files in the InAir project.

####`AndroidManifest.xml`
>The manifest file describes the fundamental characteristics of the app and defines each of its components. It mostly follows Google's Android declarations except for some few minor details. Learn more about various declarations in this file from Google's [Manifest file](http://developer.android.com/guide/topics/manifest/manifest-intro.html) guide.

>InAir App requires a special `inair.application` permission, manifest files without this permission won't be regconized by InAir Launcher.

>```xml
      <manifest xmlns:android="http://schemas.android.com/apk/res/android" ... >
          <uses-permission android:name="inair.application" />
          ...
      </manifest>
```

####`src/`
>Directory for your app's main source files. If you are and Android developer, you will now realize that InAir doesn't have an Activity Class. In contrast, it includes an [ViewLayout](#link_to_ViewLayout) class that runs when your app is launched.

####`res/`
>Contains several sub-directories for app resources same as in an Android app. Here are just a few:
#####`layout/`
>>Directory for files that define your app's user interface.
>
#####`drawable/`
>>Directory for drawable objects (such as bitmaps) to be used within InAir App, including the logo for the app.
>
#####`values/`
>>Directory for other various XML files that contain a collection of resources, such as string and color definitions.
>

## Running From InAiR Emulator
InAir can be emulated by running a special build of Android Emulator. Please follow [Installing InAiR Emulator](#) to get your emulator running.
Once you have the emulator running, you can build and run your app by:

1. Select **Run > Run 'app'**.
2. Select InAir-x.x as your target device.
3. Wait for your app view to appear on screen. In this example, you will see the text "Hello world" appeared somewhere on the screen.

Congratulation, you've built your first InAir app.

## Running on an InAiR Device
Coming soon!