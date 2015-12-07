# InAiR Application

## Overview
Just like [Android Application](http://developer.android.com/guide/components/fundamentals.html#Components), InAiR application also has four different types of app components. The `Content providers` component and `Broadcast receivers` component are same as normal ones but `Activities` component and `Services` component are slightly different. With InAiR SDK, you must use [IAActivity](#iaactivity) and [IAService](link).

In InAiR system, each **IAActivity** is an InAiR application. Because of this, InAiR application also contains many of [IAFragment](#iafragment) as sub activities and modular components. The foreground **IAActivity** is also the ***current running application***, all InAiR control events will be dispatched only to this **IAActivity**.

## IAActivity
As InAiR Activity (`IAActivity`) subclasses Android Activity, understanding [Android Activity](http://developer.android.com/guide/components/activities.html) is mandatory.

Such as `Android Activity`, **IAActivity** also has activity's lifecycle callbacks, but you can not access those Android activity's callback methods. **IAActivity** provides others callback methods to manage it's own lifecycle. The two most important callback methods are:

- `onInitialize()`
You must implement this method. The system calls this when creating your **IAActivity**. Within your implementation, you should initialize the essential components of your **IAActivity**. Most importantly, this is where you must call **setRootContentView()** to define the layout for the IAActivity's user interface.

- `onFinalize()`
The system calls this method when **IAActivity** is completely destroyed. This is usually where you should commit any changes that should be release your application resources.

Besides being InAiR application, **IAActivity** has InAiR application's own lifecycle callback methods:

- `onLaunch()`
The system calls this method when **IAActivity** is completely initialized. It means all layouts is created and displayed on screen. User control events are now dispatched directly to this **IAActivity**.

- `onApplicationWillTerminate()`
The system calls this method when **IAActivity** is preparing to destroyed or your InAiR Application will be terminated. Since being an InAiR application, **IAActivity** can be terminated by manually call [IAActivity.finish()](link) or by receiving the ***terminating application event*** from system.

- `onApplicationDidTerminate()`
The system calls this method when **IAActivity** is completely terminated and will be destroyed soon.

**IAActivity** is also subclass of [IANavigation](link), it has all [Navigation callbacks](#navigation-callback) too.

## IAFragment
As InAiR Fragment (`IAFragment`) subclasses Android Fragment, understanding [Android Fragment](http://developer.android.com/guide/components/fragments.html) is mandatory.



**IAFragment** is also subclass of [IANavigation](link), it has all [Navigation callbacks](#navigation-callback) too.

## Navigation callbacks
[Present - Dismiss](../2-api-guides/4-animation-and-graphics/3-present-dismiss.md)

- `onChildLayoutWillPresent(IAFragment child)`

- `onChildLayoutDidPresent(IAFragment child)`

- `onChildLayoutWillDismiss(IAFragment child)`

- `onChildLayoutDidDismiss(IAFragment child)`

- `onLayoutWillPresent(IAFragment parent)`

- `onLayoutDidPresent(IAFragment parent)`

- `onLayoutWillDismiss(IAFragment parent)`

- `onLayoutDidDismiss(IAFragment parent)`
