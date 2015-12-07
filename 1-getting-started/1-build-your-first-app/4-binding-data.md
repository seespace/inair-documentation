Binding Data
============

InAiR SDK uses [data-binding](https://msdn.microsoft.com/en-us/library/ms752347%28v=vs.100%29.aspx) to connect between properties and layouts. This lesson will teach you the basic of creating a binding within InAiR SDK.

The View Model
--------------
1. In Android Studio, in the java directory, select the package, __com.example.helloworld__, right-click, and select __New__ > __Java Class__.
2. In the __Create New Class__ window, set the class name `MainViewModel` and click __OK__
3. Open the MainViewModel.java file.
4. To use InAiR `ViewModel` APIs, our class must extend InAiR abstract class `ViewModel`. Create the required constructor with only one argument `IAContext`. 

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

The Activity
------------

1. In Android Studio, open the `MainActivity.java` file.
2. Set the `Activity`'s data context. 

The result look like this:

```java
package com.example.helloworld;

...

public class MainActivity extends IAActivity {

  public static final String TAG = "Hello World";

  @Override
  public void onInitialize(Bundle bundle) {
    setRootContentView(R.layout.activity_main);
    setDataContext(new MainViewModel(this));
  }
}
```

The Properties
--------------

1. Our layout has 3 elements that will be changed prediodically: the _photo_, the _photo's title_, and its _description_. Let's create 3 properties that will be used to bind to our layout:
```java
  private BitmapDrawable photoSrc;
  private String photoTitle;
  private String photoDescription;
```
2. Add Setters & Getters:
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
3. Set default value to each property inside the class' constructor.
```java
  // Constructor
  public MainViewModel(IAContext context) {
    super(context);

    setPhotoSrc(((BitmapDrawable) getResources().getDrawable((R.drawable.photo2))));
    setPhotoTitle("Amazing Photo");
    setPhotoDescription("Lorem Ipsum Vivamus sagittis lacus vel augue laoreet rutrum faucibus dolor auctor. Donec sed odio dui.");
  }
```

The Layout XML
--------------

At the moment, we have a fully working `ViewModel`. However, the view is using its hard-coded value in previous lesson. Update the layout to read values from our `ViewModel`

In Android Studio, from the `res/layout` directory, open the `activity_main.xml` file.

Update the file as follows:

```xml
...
  <UIImageView
    ui:width="800"
    ui:height="500"
    ui:id="@+id/main_photo"
    ui:src="{Binding Path: 'photoSrc'}"
    />

  <UITextView
    ui:height="60.0"
    ui:width="800.0"
    ui:text="{Binding Path: 'photoTitle'}"
    ui:textColor="@color/white"
    ui:fontSize="40.0"
    ui:fontStyle="bold"
    ui:alpha="1.0"
    ui:positionY="540.0"
    />

  <UITextView
    ui:height="400.0"
    ui:width="800.0"
    ui:text="{Binding Path: 'photoDescription'}"
    ui:textColor="@color/white"
    ui:fontSize="24.0"
    ui:alpha="1.0"
    ui:positionY="600.0"
    />
```

The syntax `{Binding Path: <property name>}` will tell the layout to look for the corresponding variable inside the model view and listen for changes produced by the binding property's setter.

Now run your application again, the [photo2](../images/photo2.jpg) should be displayed.

![InAiR binding](../../images/running2.jpg)

