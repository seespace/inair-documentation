# Present/Dismiss

## Overview
Present/Dismiss is designed to display more information about something (for example, showing the contents of an article) by presenting a new view into the screen with translating animation from the right edge of the screen.

## Implement
**Prerequisite.**
A presenting view - The parent view which contains the information you want to show more about.
A presented view - The child view which contains the detail information.

If you want to present the presented view, simply call **present(presentedView)** on the presenting view.
If you want to dismiss, simply call **dismiss()** on the presented view to hide it and return to the presenting view.

>Notice: If not set, the x, y and z position of the presented view will all be 0px, which is the top left of the screen. You can set the x and y position according to your app design but for the z-position, it should be set to 700 for better view in 3D mode. (For now, changing the z-position will also affect the x and y position when look at 2D).

## Sample code
Create a view named PresentWithSingleView - which represents the presenting view and a presented view also named PresentedSingleContentView.

Call **present(new PresentedSingleContentview())** on doubleTapListener will display the according view with animation from the right side of the screen to the position that is set to the view.

```java
  Event.Listener<TouchEventArgs> doubleTapPresentListener = new Event.Listener<TouchEventArgs>() {
    @Override
    public void onTrigger(Object o, TouchEventArgs touchEventArgs) {
      present(new PresentedSingleContentView());
    }
  };
```

By default, swipe right will dismiss the presented view. In case of you want to dismiss manually, just call **dismiss()** on the presented view whenever you want. For example if you want to dismiss the presented view after 10 seconds after presenting:

```java
  @Override
  public void onRootViewDidAppear() {
    new Handler().postDelayed(new Runnable() {
      @Override
      public void run() {
        dismiss();
      }
    }, 10000);
  }
```