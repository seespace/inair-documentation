Binding Data
============

InAiR SDK uses [data-binding](https://msdn.microsoft.com/en-us/library/ms752347%28v=vs.100%29.aspx) to connect between properties and layouts. This lesson will teach you the basic of creating a binding within InAiR SDK.

The View Model
--------------
1. In Android Studio, in the java directory, select the package, __com.example.helloworld__, right-click, and select __New__ > __Java Class__.
2. In the __Create New Class__ window, set the class name `MainViewModel` and click __OK__
3. Open the MainViewModel.java file.
4. To use InAiR `ViewModel` APIs, our class must extend InAiR abstract class `ViewModel`. Create the required constructor with only one argument `IAContext`

Your class should read as follows:

```java
package com.example.helloworld;

import inair.app.IAContext;
import inair.data.ViewModel;

public class MainViewModel extends ViewModel {
  public MainViewModel(IAContext context) {
    super(context);
  }
}
```

Now you have a barebone `ViewModel` with no properties. 

Our layout has 3 elements that will be changed prediodically: the _photo_, the _photo's title_, and its _description_. Let's create 3 properties that will be used to bind to our layout:

```java
  private BitmapDrawable photoSrc;
  private String photoTitle;
  private String photoDescription;
```

Add Setters & Getters:

```java
  // Getters & Setters
  public BitmapDrawable getPhotoSrc() {
    return photoSrc;
  }

  public void setPhotoSrc(BitmapDrawable photoSrc) {
    this.photoSrc = photoSrc;
    notifyPropertyChanged("photoSrc");
  }

  public String getPhotoTitle() {
    return photoTitle;
  }

  public void setPhotoTitle(String photoTitle) {
    this.photoTitle = photoTitle;
    notifyPropertyChanged("photoTitle");
  }

  public String getPhotoDescription() {
    return photoDescription;
  }

  public void setPhotoDescription(String photoDescription) {
    this.photoDescription = photoDescription;
    notifyPropertyChanged("photoDescription");
  }
```

Notice the function `notifyPropertyChanged("<property's name>");` that is being used on every setters? This function will tell the system that the corresponding property has changed and the layout should refresh to update with the new value.

Set default value to each property inside the class' constructor.

```java
  // Constructor
  public MainViewModel(IAContext context) {
    super(context);

    setPhotoSrc(((BitmapDrawable) getResources().getDrawable((R.drawable.photo1))));
    setPhotoTitle("Amazing Photo");
    setPhotoDescription("Lorem Ipsum Vivamus sagittis lacus vel augue laoreet rutrum faucibus dolor auctor. Donec sed odio dui.");
  }
```

The Layout XML
--------------

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

