
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

####`res/`
>Contains several sub-directories for app resources same as in an Android app. Here are just a few:
#####`layout/`
>>Directory for files that define your app's user interface.
>
#####`drawable/`
>>Directory for drawable objects (such as bitmaps) to be used within InAiR App, including the logo for the app.
>
#####`values/`
>>Directory for other various XML files that contain a collection of resources, such as string and color definitions.
>

Congratulation, you've built your first InAir app.