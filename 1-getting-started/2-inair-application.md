# InAiR Application

## Overview
Just like [Android Application](http://developer.android.com/guide/components/fundamentals.html#Components), InAiR application also has four different types of app components. [ContentProvider](http://developer.android.com/reference/android/content/ContentProvider.html) component and [BroadcastReceiver](http://developer.android.com/reference/android/content/BroadcastReceiver.html) component are the same as Android's but [Activity](http://developer.android.com/reference/android/app/Activity.html) component and [Service](http://developer.android.com/reference/android/app/Service.html) component are slightly different. With InAiR SDK, you must use [IAActivity](#iaactivity) and [IAService](#).

In InAiR system, each IAActivity is an InAiR application. Because of this, InAiR application also contains many [IAFragment](#iafragment) as sub activities and modular components. The foreground IAActivity is also the ***current running application***, all InAiR control events will be dispatched only to this IAActivity.

## IAActivity
As InAiR's IAActivity subclasses Android's Activity, understanding Android [Activity](http://developer.android.com/guide/components/activities.html) is mandatory.

Similar to Android's Activity, IAActivity also has activity's lifecycle callbacks, but you can not access Android activity's callback methods. IAActivity provides others callback methods to manage it's own lifecycle. The two most important callback methods are:

- `onInitialize()`
You must implement this method. The system calls this when creating your IAActivity. Within your implementation, you should initialize the essential components of your IAActivity. Most importantly, this is where you must call `setRootContentView()` to define the layout for the IAActivity's user interface.

- `onFinalize()`    
The system calls this method right before IAActivity instance is completely destroyed. This is where you should commit any change you want to persist and release any remaining resource before your application is closed.

Besides being InAiR Activity, IAActivity also has its own application lifecycle callbacks:

- `onLaunch()`
The system calls this method when IAActivity is completely initialized. It means all layouts are created and displayed on screen. User control events are now dispatched directly to this IAActivity.

- `onApplicationWillTerminate()`
The system calls this method when IAActivity is preparing to be destroyed or your InAiR Application will be terminated. Since being an InAiR application, IAActivity can be terminated by manually call [IAActivity.finish()](#) or by receiving the ***terminating application event*** from system.

- `onApplicationDidTerminate()`
The system calls this method when IAActivity is completely terminated and will be destroyed soon.

IAActivity is also subclass of [IANavigation](#), it has all [Navigation callbacks](#navigation-callbacks) too.

## IAFragment
As InAiR `IAFragment` subclasses Android Fragment, therefore understanding Android [Fragment](http://developer.android.com/guide/components/fragments.html) is mandatory.

Since IAFragment can be seen as sub activity, it has it's own lifecycle callback methods. Although IAFragment is Android's Fragment, you can not access to Android fragment's callback methods.

Just like IAActivity, IAFragment also has callback method like `onApplicationWillTerminate()` and `onApplicationDidTerminate()` where you can hook your actions on terminating application process. Besides, it also has two most important callback methods:

 - `onInitialize()`
You must implement this method. The system calls this when creating the IAFragment. Within your implementation, you should initialize essential components of the IAFragment. Most importantly, this is where you must call `setRootContentView()` to define the layout for the IAFragment's user interface.

 - `onFinalize()`
 The system calls this method when IAFragment is completely destroyed. This is usually where you should commit any change and release your IAFragment resources.

IAFragment is also subclass of [IANavigation](#), it has all [Navigation callbacks](#navigation-callbacks) too.

## Navigation callbacks
Both IAActivity and IAFragment can display more detail information through child IAFragment. You can use [Present - Dismiss](../2-api-guides/4-animation-and-graphics/3-present-dismiss.md) feature to do that.

- `onChildLayoutWillPresent(IAFragment child)`
The system calls this method when IAFragment is preparing to present `child` IAFragment.

- `onChildLayoutDidPresent(IAFragment child)`
The system calls this method when IAFragment presented `child` IAFragment.

- `onChildLayoutWillDismiss(IAFragment child)`
The system calls this method when `child` IAFragment is preparing to be dismissed.

- `onChildLayoutDidDismiss(IAFragment child)`
The system calls this method when `child` IAFragment is completely dismissed and current IAFragment has control back.

- `onLayoutWillPresent(IAFragment parent)`
The system calls this method when IAFragment will be presented from `parent` IAFragment. Since IAActivity is InAiR application, this callback is available only in IAFragment.

- `onLayoutDidPresent(IAFragment parent)`
The system calls this method when IAFragment is presented from `parent` IAFragment. Since IAActivity is InAiR application, this callback is available only in IAFragment.

- `onLayoutWillDismiss(IAFragment parent)`
The system calls this method when IAFragment will be dismissed and return to `parent` IAFragment. Since IAActivity is InAiR application, this callback is available only in IAFragment.

- `onLayoutDidDismiss(IAFragment parent)`
The system calls this method when IAFragment is dismissed. After this, control and return to `parent` IAFragment. Since IAActivity is InAiR application, this callback is available only in IAFragment.
