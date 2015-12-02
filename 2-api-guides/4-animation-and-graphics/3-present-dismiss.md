# Present/Dismiss

## Overview
Present/Dismiss is designed to display more information about something (for example, showing the contents of an article) by presenting a new view into the screen with animation.

## Implement
Prequisite.

A presenting view - The parent view which contains the information you want to show more about.
A presented view - The child view which contains the detail information.

If you want to present the presented view, simply call **present(presentedView)** on the presenting view.
If you want to dismiss, simply call **dismiss()** on the presented view to hide it and return to the presenting view.

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

By default, swipe right will dismiss the presented view. In case of you want to dismiss manually, just call **dismiss()* on the presented view whenever you want. For example if you want to dismiss the presented view after 10 seconds after presenting:

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