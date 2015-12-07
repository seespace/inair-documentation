Build a Simple Slideshow
========================

Same as Android, InAiR app is built using a hierarchy of `UIView` and `UIViewGroup`. InAiR provides an XML vocabulary that corresponds to the subclasses of `UIView` and `UIViewGroup` so you can define your UI in XML using a hierarchy of UI elements.

Continue from where we left off, this lesson will guide you through building a simple Photo Gallery App.

Let's assume we want to try something like the following design:

![App Design](../../images/gallery_design.png "App Design")


Updating the Layout
-------------------

The __BlankApp__ template we selected at the begining of this tutorial includes a `activity_main.xml` file with a __`UIViewGroup`__ and a __`UITextView`__ child view.

1. In Android Studio, from the `res/layout` directory, open the `activity_main.xml` file.

2. In the Preview pane, there will be 2 panes at the bottom (__Design__ & __Text__). Select __Text__ pane.
    > In Android Studio, when you open a layout file, you’re first shown the Preview pane. Since InAiR uses a different view system, it's not possible to use WYSIWYG tools. You're going to work directly with the XML.

3. Delete the `<UITextView>` element.
4. Add attributes defining layout's size & position:

| Attribute    | Value |
| -------------| ----- |
| ui:width     | 840   |
| ui:height    | 1000  |
| ui:positionX | 1000  |
| ui:positionY | 40    |
| ui:positionZ | 0     |

The result looks like this:

`res/layout/activity_main.xml`
```xml
<?xml version="1.0" encoding="utf-8"?>
<UIViewGroup xmlns:ui="http://schemas.android.com/apk/res-auto"
             ui:width="840"
             ui:height="1000"
             ui:positionX="1000"
             ui:positionY="40"
             ui:positionZ="0"
  >

</UIViewGroup>
```

The attributes `ui:width`, `ui:height`, `ui:positionX` and `ui:positionY` define the boundings of the view group.

For more information about layout properties, see the [Layout]() guide.

> **Notes:** The pixel resolution of the screen is always 1920x1080. There's no other resolution in InAiR.

Add a photo
-----------

1. In the `activity_main.xml` file, within the `<UIViewGroup>` element, define an `<UIImageView>` element with the id attribute set to `@+id/main_photo`
2. Define the `ui:width` and `ui:height` attributes as 800 and 500, respectively.
3. Save the following images to your __`res/drawable`__ folder: [photo1](../../images/photo1.jpg), [photo2](../../images/photo2.jpg), [photo3](../../images/photo3.jpg), [photo4](../../images/photo4.jpg), [photo5](../../images/photo5.jpg).

The `<UIImageView>` element should read as follows:

`res/layout/activity_main.xml`
```xml
<UIImageView
    ui:width="800"
    ui:height="500"
    ui:id="@+id/main_photo"
    ui:src="@drawable/photo1"
    />
```
 
Now run your application again, you would get something like this.

![InAiR App With a Photo](../../images/running.jpg "InAiR App With a Photo")

Proceed to the next lesson to learn how you can use *Binding* to make the Slideshow.