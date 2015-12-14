# Binding data source

This tutorial will help you create a model view file and binding to layered navigation items source within InAiR SDK.

###Creating a model view file for one layer
Open the `SecondViewModel.java` file inside the `viewmodel` package.
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

The data can be set to the properties right here in the view model, or pass down from layout when call the view model's constructor. For this example, we specify the sample data right in the view model constructor, just like this:
```java
// Constructor
public SecondViewModel(IAContext context) {
    super(context);
    setText("InAiR - This is the second layer screen with binding content");
    setImage(R.drawable.ic_logo2d3d);
}
```
###Finalize the layered layout XML
Open the `second_layer.xml` file from `res/layout`.
Since we use `second_layer.xml` as a template, content of `UIImageView`and `UITextView` will depend on the data that showing on each layer, we need to use `DataBinding`.

There're two properties inside this XML we need to change in order to bind with our View Model properties declared previously:

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
The syntax `{Binding Path: <property name>}` will tell the layout to look for the corresponding variable inside the view model and listen for changes produced by the binding property's setter.

###Prepare content for layer
```java
public class SecondLayer extends IAFragment {
  @Override
  public void onInitialize(Bundle bundle) {
    setRootContentView(R.layout.second_layer);
    setDataContext(new SecondViewModel(this));
  }
}
```
Here we use `setRootContentView()` to specify which layout is our root content view for our layer. And we use `setDataContext()` to specify which view model is bound to that root layout. Or for short, we can use `setAndBindRootContentView(the_layout, the_view_model)` to do the same thing.

That's it, you can now try to **Build** and **Run** your app.