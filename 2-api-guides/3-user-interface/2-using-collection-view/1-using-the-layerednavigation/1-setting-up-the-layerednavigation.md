This lesson will guide you through building a simple Place Application like [Figure 1]() in `Overview` section.

__First of all:__ we using InAiR Layered App Template

###Creating a layered view
Open the `first_layer.xml` file from `res/layout`

```xml
<?xml version="1.0" encoding="utf-8"?>
<UILayeredViewItem xmlns:ui="http://schemas.android.com/apk/res-auto">
  <UIViewGroup>

    <UIImageView
      ui:width="310"
      ui:height="248"
      ui:positionX="0"
      ui:positionY="100"
      ui:src="@drawable/ic_inairlogo" />

    <UITextView
      ui:width="310"
      ui:positionX="0"
      ui:positionY="400"
      ui:text="Welcome to InAiR Layered View Template"
      ui:fontSize="40" />

  </UIViewGroup>
</UILayeredViewItem>
```

We use this file as a template for each layer of layered navigation. Following design, we need an `UIImageView` to show an image of the place and an `UITextView` to present a short description.

###Creating a model view file for one layer
Open the `FirstViewModel.java` file inside the `viewmodel` package, you should see the following content:

```java
public class FirstViewModel extends ViewModel implements LayeredItemViewData {
  public FirstViewModel(IAContext context) {
    super(context);
  }

  @Override
  public CharSequence getTitle() {
    return "first";
  }

  @Override
  public boolean getShouldOpen() {
    return true;
  }
}
```

> ####Note:
> FirstViewModel is a view model for one layer, it need to be implement `LayeredItemViewData` interface and override `getTitle()` method to provide `title` for each layered in UILayeredNavigation. 
> Override `getShouldOpen()` method to provide open or close door for each layered. Default, getShouldOpen() return true

###Creating a view file for bind view model to layered
Open the `FirstLayer.java` file inside the `view` package

```java
public class FirstLayer extends IAFragment {
  @Override
  public void onInitialize(Bundle bundle) {
    setAndBindRootContentView(R.layout.first_layer, new FirstViewModel(this));
  }
}
```
Great, now you have the basic layout laid out. Proceed to the next lesson to learn how you can use *Binding* to complete the application.