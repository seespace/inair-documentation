Routed Event
============

This topic describes the concept of routed events in InAiR Framework. The topic defines routed events terminology, describes how routed events are routed through a tree of elements, summarizes how you handle routed events, and introduces how to create your own custom routed events.

## Prerequisites
This topic assumes that you have basic knowledge of InAiR `Event` and object-oriented programming, as well as the concept of how the relationships between InAiR UI elements can be conceptualized as a tree.  

## What is a Routed Event?
A routed event is a type of event that can invoke handlers on multiple listeners in an element tree, rather than just on the object that raised the event.

A typical application contains many elements. Whether created in code or declared in XML, these elements exist in an element tree relationship to each other. The event route can travel in one of two directions depending on the event definition, but generally the route travels from the source element and then "bubbles" upward through the element tree until it reaches the element tree root. This bubbling concept might be familiar to you if you have worked with the DHTML object model previously.

Consider the following simple element tree:

```html
<box>
  <group>
    <button type="button" id="yes">Yes</button>
    <button type="button" id="no">No</button>
    <button type="button" id="cancel">Cancel</button>
  </group>
</box>
```

This element tree produces something like the following:
![buttons](http://developer.inair.tv/upload_file/attachment/buttons.png "Buttons")

In this simplified element tree, the source of a `click` event is one of the `button` elements, and whichever `button` was clicked is the first element that has the opportunity to handle the event. But if no handler attached to the `button` acts on the event, then the event will bubble upwards to the `button` parent in the element tree, which is the `group`. Potentially, the event bubbles to `box`, and then beyond to the page root of the element tree (not shown).

In other words, the event route for this `click` event is: `button -> group -> box -> ...`

## How Routed Events are Implemented

A routed event is an event that is backed by an instance of the [`RoutedEvent`][RoutedEvent] class and registered with the event system. The [`RoutedEvent`][RoutedEvent] instance obtained from registration is typically retained as a public static readonly field member of the class that registers and thus "owns" the routed event.

The following example shows the declaration for a custom `Swipe` routed event, including the registration and exposure of the [`RoutedEvent`][RoutedEvent] identifier field and the add and remove implementations for the `Swipe` event.

```java
public static final RoutedEvent SwipeEvent = EventManager.registerRoutedEvent(
    "Swipe", 
    RoutingStrategy.Bubble, 
    Gesture.class
);
```

## Routing Strategies

Routed events use one of three routing strategies:

- **Bubbling:** Event handlers on the event source are invoked. The routed event then routes to successive parent elements until reaching the element tree root. Most routed events use the bubbling routing strategy. Bubbling routed events are generally used to report input or state changes from distinct controls or other UI elements.

- **Direct:** Only the source element itself is given the opportunity to invoke handlers in response. Unlike a standard event, direct routed events support class handling (class handling is explained in an upcoming section).

- **Tunneling:** Initially, event handlers at the element tree root are invoked. The routed event then travels a route through successive child elements along the route, towards the node element that is the routed event source (the element that raised the routed event). Tunneling routed events are often used or handled as part of the compositing for a control, such that events from composite parts can be deliberately suppressed or replaced by events that are specific to the complete control. Input events often come implemented as a tunneling/bubbling pair. `Tunneling` events are also sometimes referred to as `Preview` events, because of a naming convention that is used for the pairs.

## Adding and Implementing an Event Handler for a Routed Event

Routed event listeners can always be added through `UIView` method `addEventListener`.

```java
  void makeImageView() {
    UIImageView imageView = new UIImageView();
    imageView.addEventListener(UIView.DoubleTapEvent, onImageDoubleTap);
  }

  private Event.Listener<TouchEventArgs> onImageDoubleTap = new Event.Listener<TouchEventArgs>() {
    @Override
    public void onTrigger(Object sender, TouchEventArgs args) {
      ...
    }
  };
```

## The Concept of Handled

All routed events share a common event data base class, [`RoutedEventArgs`][RoutedEventArgs]. [`RoutedEventArgs`][RoutedEventArgs] defines the `handled` property, which takes a `Boolean` value. The purpose of the `handled` property is to enable any event handler along the route to mark the routed event as handled, by setting the value of `handled` to true. After being processed by the handler at one element along the route, the shared event data is again reported to each listener along the route.

The value of `handled` affects how a routed event is reported or processed as it travels further along the route. If `handled` is true in the event data for a routed event, then handlers that listen for that routed event on other elements are generally no longer invoked for that particular event instance. For most common handler scenarios, marking an event as handled by setting `handled` to true will "stop" routing for either a tunneling route or a bubbling route, and also for any event that is handled at a point in the route by a class handler.

In addition to the behavior that `handled` state produces in routed events, the concept of `handled` has implications for how you should design your application and write the event handler code. You can conceptualize `handled` as being a simple protocol that is exposed by routed events. Exactly how you use this protocol is up to you, but the conceptual design for how the value of `handled` is intended to be used is as follows:

- If a routed event is marked as handled, then it does not need to be handled again by other elements along that route.

- If a routed event is not marked as handled, then other listeners that were earlier along the route have chosen either not to register a handler, or the handlers that were registered chose not to manipulate the event data and set `handled` to true. (Or, it is of course possible that the current listener is the first point in the route.) Handlers on the current listener now have three possible courses of action:
  - Take no action at all; the event remains unhandled, and the event routes to the next listener.
  - Execute code in response to the event, but make the determination that the action taken was not substantial enough to warrant marking the event as handled. The event routes to the next listener.
  - Execute code in response to the event. Mark the event as handled in the event data passed to the handler, because the action taken was deemed substantial enough to warrant marking as handled. The event still routes to the next listener, but with `handled=true` in its event data.

In applications, it is quite common to just handle a bubbling routed event on the object that raised it, and not be concerned with the event's routing characteristics at all. However, it is still a good practice to mark the routed event as handled in the event data, to prevent unanticipated side effects just in case an element that is further up the element tree also has a handler attached for that same routed event.

## Class Handlers

If you are defining a class that derives in some way from [DependencyObject][DependencyObject], you can also define and attach a class handler for a routed event that is a declared or inherited event member of your class. Class handlers are invoked before any instance listener handlers that are attached to an instance of that class, whenever a routed event reaches an element instance in its route.

Some controls have inherent class handling for certain routed events. This might give the outward appearance that the routed event is not ever raised, but in reality it is being class handled, and the routed event can potentially still be handled by your instance handlers if you use certain techniques. Also, many base classes and controls expose virtual methods that can be used to override class handling behavior.