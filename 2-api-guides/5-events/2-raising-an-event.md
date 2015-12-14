Raising an Event
================

If you want your class to raise an event, you must provide the following three elements:

- A class that provides event data (The Data)
- An event listener (The Event Listener)
- A class that raises the event (The Event Owner)

## Defining a Class to Provide Event Data

By convention in the InAiR Framework, when an event is raised, it passes event data to its event handlers. The event data is provided by the `EventArgs` class or by a class that is derived from it.

An event often has no custom data; the fact that the event was fired provides all the information that event handlers require. In this case, the event can pass an `EventArgs` object to its handlers.

If an event does have custom data, it can pass an instance of a class derived from `EventArgs` to event handlers. Depending on the precise data the event passes to handlers, you may be able to use an existing event data class in the InAiR Framework. For example, if your event handler processes touches, you can use the `TouchEventArgs` class.

When you need to provide custom data to handlers and an existing class is not available, you can define your own event data class. It must derive from `EventArgs`. By convention, this class is named _EventName_**EventArgs**. The following example illustrates such a custom event data class. It defines a class named `AlarmEventArgs` that provides two items of data to event handlers: the read-only `alarmTime` property, which indicates when the alarm went off; and the `snoozeOn` property, which indicates whether the alarm should go off again after a designated interval or whether future alarms should be canceled.

```java
public class AlarmEventArgs extends EventArgs {
  public Date alarmTime;
  public boolean snoozeOn = true;

  public static AlarmEventArgs obtain(Date alarmTime, boolean snoozeOn) {
    AlarmEventArgs args = EventArgs.obtain(AlarmEventArgs.class);
    args.alarmTime = alarmTime;
    args.snoozeOn = snoozeOn;
    return args;
  }
}
```

## Constructing a Listener for the Event

A particular event listener typically corresponds to a particular event data class. By convention, event listener in the InAiR Framework named `onEventName` and have the following signature:
```java
Event.Listener<EventNameEventArgs> onEventName = new Event.Listener<EventNameEventArgs>() {
    @Override
    public void onTrigger(Object sender, EventNameEventArgs args) {
      ...
    }
};
```

where `sender` is an Object that provides a reference to the class or structure that fired the event, and `args` is an `EventArgs` object or an object derived from `EventArgs` that provides event data.

The following example constructs an event listener named `onAlarmEvent`.

```java
Event.Listener<AlarmEventArgs> onAlarmEvent = new Event.Listener<AlarmEventArgs>() {
    @Override
    public void onTrigger(Object sender, AlarmEventArgs args) {
      ...
    }
};
```

## Defining a Class to Raise the Event

The class that raises the event must provide the event declaration. In addition, it must provide some logic to raise the event in a class property or method.

The following example declares an event named `alarmEvent`.
```java
public final Event<AlarmEventArgs> alarmEvent = new Event<AlarmEventArgs>();
```

Once you have defined your event implementation, you must determine when to raise the event. You raise the event by calling the event's `raise` method.
```java
alarmEvent.raise(this, args);
```

The following example defines a method named `set` that contains the logic to fire the event. If the hours and the minutes of the alarm time equal the hours and minutes of the current time, the `set` method instantiates an `AlarmEventArgs` object and provides it with the time that the alarm went off. After the event handlers execute, it checks the value of the `snoozeOn` member. If `snoozeOn` is `false`, no more alarm events should be raised, so the `set` method can end. If `snoozeOn` is `true`, the time the alarm is to go off is incremented by the value of the `interval` member.

```java
  Date alarmTime = new Date(2016, 10, 9);
  boolean snooze = true;
  int interval = 60 * 10;

  public void set() {
    while (true) try {
      Thread.sleep(2000);
      Date currentTime = new Date();
      if (currentTime.getHours() == alarmTime.getHours() && currentTime.getMinutes() == alarmTime.getMinutes()) {
        AlarmEventArgs args = AlarmEventArgs.obtain(alarmTime, snooze);
        alarmEvent.raise(this, args);
        if (!args.snoozeOn) {
          return;
        } else {
          this.alarmTime.setTime(this.alarmTime.getTime() + this.interval);
        }
      }
    } catch (InterruptedException e) {
      e.printStackTrace();
    }
  }
```

> **Note**: An Event Owner can listen to its own event.