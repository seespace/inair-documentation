This lesson will teach you the basic of creating a model view file and binding to layered navigation items source within InAiR SDK.

###Creating a model view file for one layer
Open the `SecondViewModel.java` file inside the `viewmodel` package, you should see the following content:
Now, our layout has two elements that will be diffirent between each others: the image, and it's description. Let's create two properties that shall be used to bind to our layout:
```java
private String text;
private int image;
```
And we create the Setters & Getters for them:
```java
public String getText() {
    return text;
}

public void setText(String text) {
    this.text = text;
    notifyPropertyChanged("text");
}

public Drawable getImage() {
    return getResources().getDrawable(image);
}

public void setImage(int image) {
    this.image = image;
    notifyPropertyChanged("image");
}
```
Notice the function `notifyPropertyChanged("<property's name>");` that is being used on every setters? This function will tell the system that the corresponding property has changed and the layout should refresh to update with the new value.
Let's add more parameters to the class' constructor to initialize all properties we need.
```java
// Constructor
public SecondViewModel(IAContext context, String text, int imageSrc) {
    super(context);
    setText("InAiR - This is the second layer screen with binding content");
    setImage(R.drawable.ic_logo2d3d);
}
```
###Finalize the layered layout XML
Open the `second_layer.xml` file from `res/layout`
Since we use `second_layer.xml` as a template, content of `UIImageView`and `UITextView` will depend on the data that showing on each layer, we need to use `DataBinding`.

There're two properties inside this XML we need to change in order to bind with our Model View properties declared previously:

- `ui:src` of __`UIImageView`__
- `ui:text` of __`UITextView`__

Complete XML file should be like this:
```xml
<?xml version="1.0" encoding="utf-8"?>
<UILayeredViewItem xmlns:ui="http://schemas.android.com/apk/res-auto">
  <UIViewGroup>

    <UIImageView
      ui:height="254"
      ui:positionX="0"
      ui:positionY="100"
      ui:src="{ Binding Path='image' }"
      ui:width="310"/>

    <UITextView
      ui:fontSize="40"
      ui:height="100"
      ui:positionX="20"
      ui:positionY="400"
      ui:text="{ Binding Path='text' }"
      ui:width="310"/>

  </UIViewGroup>
</UILayeredViewItem>
```
The syntax `{Binding Path: <property name>}` will tell the layout to look for the corresponding variable inside the model view and listen for changes produced by the binding property's setter.

###Prepare content for layers
```java
public class SecondLayer extends IAFragment {
  @Override
  public void onInitialize(Bundle bundle) {
    setAndBindRootContentView(R.layout.second_layer,
      new SecondViewModel(this, "InAiR - This is the second layer screen with binding content", R.drawable.ic_logo2d3d));
  }
}
```

__That is, you can now try to Build and Run your project.__