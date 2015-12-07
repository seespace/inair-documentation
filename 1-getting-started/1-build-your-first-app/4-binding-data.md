Binding Data
============

InAiR SDK uses variable-binding as a method to connect between properties and layouts. In short, it means that layout can change the appearance automatically when binded properties were changed. Refer to [InAir MVVM & Binding articles](#article) if you want to learn more.

This lesson will teach you the basic of creating a binding within InAiR SDK.

##The Model View
The __Model View Class__ is the brain of our InAir Application and it's linked very closely with the __Layout__.

Open the file `TestModelView` inside the `modelview` package. You should see the following content:

```java
package com.example.helloworld.app.modelview;

import ...

/**
 * Implementation of view model
 * Should be used to declare all properties which are using to bind in layout
 * Logic code to manipulate data must be declare here
 *
 * <p>Copyright (c) 2014 SeeSpace.co. All rights reserved.</p>
 */
public class TestModelView extends ViewModel {

  // Constructor
  public TestModelView() {

  }

}
```

Now, Our layout has 3 elements that will be changed prediodically: the _photo_, the _photo's name_, and it's _description_. Let's create 3 properties that shall be used to bind to our layout:

```java
  private BitmapDrawable imageSrc;
  private String photoName;
  private String photoDescription;
```

And we create the Setters & Getters for them:

```java

  //Getters & Setters

  public String getPhotoName() {
    return photoName;
  }

  public void setPhotoName(String photoName) {
    this.photoName = photoName;
    notifyPropertyChanged("photoName");
  }

  public String getPhotoDescription() {
    return photoDescription;
  }

  public void setPhotoDescription(String photoDescription) {
    this.photoDescription = photoDescription;
    notifyPropertyChanged("photoDescription");
  }

  public BitmapDrawable getImageSrc() {
    return imageSrc;
  }

  public void setImageSrc(BitmapDrawable imageSrc) {
    this.imageSrc = imageSrc;
    notifyPropertyChanged("imageSrc");
  }
```
Notice the function `notifyPropertyChanged("<property's name>");` that is being used on every setters? This function will tell the system that the corresponding property has changed and the layout should refresh to update with the new value.

Let's give some random content to each property inside the class' constructor.

```java
  // Constructor
  public TestModelView() {
    setImageSrc(((BitmapDrawable) resources.getDrawable((R.drawable.photo1))));
    setPhotoName("Amazing Photo");
    setPhotoDescription("Lorem Ipsum Vivamus sagittis lacus vel augue laoreet rutrum faucibus dolor auctor. Donec sed odio dui.");
  }

```

##The Layout XML

Open our previous created xml `test_layout.xml`.
There're 3 properties inside this XML we need to change in order to bind with our Model View properties declared previously:

- `ui:src` of __`UIImageView`__
- `ui:text` of the two __`UITextView`__

```xml
<?xml version="1.0" encoding="utf-8"?>
<UIViewGroup
  xmlns:tools="http://schemas.android.com/tools"
  xmlns:ui="http://schemas.android.com/apk/res-auto"
  tools:context=".TestLayout"
  ui:width="840"
  ui:height="1000"
  ui:positionX="1000"
  ui:positionY="40">


  <UIImageView
      ui:width="800"
      ui:height="500"
      ui:src="{Binding Path: 'imageSrc'}"
      />
  <UITextView
      ui:height="60.0"
      ui:width="800.0"
      ui:text="{Binding Path: 'photoName'}"
      ui:textColor="@color/white"
      ui:textSize="40.0"
      ui:textStyle="bold"
      ui:alpha="1.0"
      ui:positionY="540.0"/>
  <UITextView
      ui:height="400.0"
      ui:width="800.0"
      ui:text="{Binding Path: 'photoDescription'}"
      ui:textColor="@color/white"
      ui:textSize="20.0"
      ui:textStyle="normal"
      ui:alpha="1.0"
      ui:positionY="600.0"/>

</UIViewGroup>
```

The syntax `{Binding Path: <property name>}` will tell the layout to look for the corresponding variable inside the model view and listen for changes produced by the binding property's setter.

