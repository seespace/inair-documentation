Overview
========
This section contains topics that describe the delegate model, show how to consume events in applications, and describe how to raise events from your class.

## Events and Event Listeners
An event is a message sent by an object to signal the occurrence of an action. The action could be caused by user interaction, such as a tap, or it could be triggered by some other program logic. The object that raises the event is called the event sender. The object that captures the event and responds to it is called the event receiver.

The InAiR framework maintains an event queue as first-in, first-out (FIFO) basis. You can capture these events in your program and take appropriate action as per requirements.

Similar to Android, there are following three concepts related to InAiR Event Management:

* **Event Listeners** − An event listener is an interface in the `Event` class that contains a single callback method. These methods will be called by the InAiR framework when the `Event` to which the listener has been registered is triggered by user interaction or some other program logic.

* **Event Listeners Registration** − Event Registration is the process by which an Event Handler gets registered with an Event Listener so that the handler is called when the Event Listener fires the event.

* **Event Handlers** − When an event happens and we have registered an event listener for the event, the event listener calls the Event Handlers, which is the method that actually handles the event.

The following example shows an Event Listener registration within an `IAActivity`:
```java
  @Override
  public void onInitialize(Bundle bundle) {
    // Listen to double tap event
    addViewEventListener(UIView.DoubleTapEvent, onDoubleTap);
  }
  
  // `onTrigger(Object o, TouchEventArgs args)` will be called when user performs double tap
  private Event.Listener<TouchEventArgs> onDoubleTap = new Event.Listener<TouchEventArgs>() {
    @Override
    public void onTrigger(Object o, TouchEventArgs args) {
      ...
    }
  };
```

The following example shows an Event Handler within an `UIView`:

```java
  @Override
  protected void onDoubleTap(TouchEventArgs args) {
    super.onDoubleTap(args);
  }
```