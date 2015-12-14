## Binding sata source

This tutorial will help you create a view model file and binding to `UIMenuView` items.

###Creating a view model file for item in UIMenuView
As in `UIListView` [tutorial](#uilistview) explained, create new view model `ColorMenuItemViewModel.java`. Remember, put this line of code `notifyPropertyChanged("<attribute name>");` in every Setters of attributes which need to bind to the Layout.
```java
import ...;

public class ColorMenuItemViewModel extends ViewModel implements ItemViewData {
    public String colorName;
    public int colorCode;
    private ColorDetailViewModel colorDetailViewModel;

    public ColorDetailViewModel getColorDetailViewModel() {
        if (colorDetailViewModel == null)
            colorDetailViewModel = new ColorDetailViewModel(getInAirContext(), colorName, colorCode);
        return colorDetailViewModel;
    }
    public int getColorCode() {	return colorCode;	}
    public void setColorCode(int colorCode) {
        this.colorCode = colorCode;
        notifyPropertyChanged("colorCode");
    }
    public void setColorDetailViewModel(ColorDetailViewModel colorDetailViewModel) {
        this.colorDetailViewModel = colorDetailViewModel;
    }
    public String getColorName() {	return colorName;	}
    public void setColorName(String colorName) {
        this.colorName = colorName;
        notifyPropertyChanged("colorName");
    }
    public ColorMenuItemViewModel(IAContext context, String color, int colorCode) {
        super(context);
        setColorName(color);
        setColorCode(colorCode);
    }
    @Override
    public void setUp() {}
    @Override
    public void tearDown() {}
    @Override
    public CharSequence getTag() {	return "word";	}
}
```
### Populate data for UIMenuView

Create new `ColorMenuViewModel` with a `ObservableCollection` instance and populate it with your data. 
Complete `ColorMenuViewModel`:
```java
import ...;

public class ColorMenuViewModel extends ViewModel {
    public ObservableCollection<ColorMenuItemViewModel> itemViewModels = new ObservableCollection<>();

    public ObservableCollection<ColorMenuItemViewModel> getItemViewModels() {
        return itemViewModels;
    }

    public void setItemViewModels(ObservableCollection<ColorMenuItemViewModel> itemViewModels) {
        this.itemViewModels = itemViewModels;
    }

    public ColorMenuViewModel(IAContext context) {
        super(context);
        itemViewModels.add(new ColorMenuItemViewModel(getInAirContext(), "red", Color.RED));
        itemViewModels.add(new ColorMenuItemViewModel(getInAirContext() , "green", Color.GREEN));
        itemViewModels.add(new ColorMenuItemViewModel(getInAirContext() , "blue", Color.BLUE));
        itemViewModels.add(new ColorMenuItemViewModel(getInAirContext() , "black", Color.BLACK));
        itemViewModels.add(new ColorMenuItemViewModel(getInAirContext() , "gray", Color.GRAY));
        itemViewModels.add(new ColorMenuItemViewModel(getInAirContext() , "magenta", Color.MAGENTA));
        itemViewModels.add(new ColorMenuItemViewModel(getInAirContext() , "white", Color.WHITE));
        itemViewModels.add(new ColorMenuItemViewModel(getInAirContext() , "yellow", Color.YELLOW));
    }
}
```
###Binding data to Layout

Next, we make the XML Layout binding to our code. Open recent `menuview_item_layout.xml` and add the binding code for `colorName` and `colorCode` element:
```java
<UIViewGroup
    xmlns:ui="http://schemas.android.com/apk/res-auto">

    <UIRectView
        ui:height="100"
        ui:width="100"
        ui:color="{ Binding Path='colorCode' }" />

    <UITextView
        ui:width="250"
        ui:positionX="105"
        ui:positionY="20"
        ui:text="{ Binding Path='colorName' }"
        ui:fontSize="40" />

</UIViewGroup>
```
Open `menuview_layout.xml` and add binding code for `itemViewModels`:
```xml
<?xml version="1.0" encoding="utf-8"?>
<UIViewGroup
    xmlns:ui="http://schemas.android.com/apk/res-auto"
    ui:positionX="430"
    ui:width="250"
    ui:height="1080"
    ui:boundToContentSize="false">
    <UIMenuView
        ui:height="1080"
        ui:highlightColor="@color/transparent"
        ui:id="@+id/listColor"
        ui:itemsSource="{ Binding Path='itemViewModels' }"
        ui:separatorHeight="20"
        ui:themeColor="@color/transparent"
        ui:width="500"
        >
        <template>
            <DataTemplate
                ui:templateId="@layout/colorcell_layout"
                ui:templateTag="word"/>
        </template>
    </UIMenuView>
</UIViewGroup>
```
Now you can build and run your app!

###First look of inAir Animations

Your app is ready now but the animation is not satisfy you? The rest of this guide will show you a first look of inAir Animation to make your app more visually.  

By default `UIMenuView` use inAir default Animation, if you want to custom this, add this attribute `ui:useDefaultAnimation` and set it to `"false"` in  `UIMenuView`.
```xml
<UIMenuView
    ui:height="1080"
    ui:highlightColor="@color/transparent"
    ui:id="@+id/listColor"
    ui:itemsSource="{ Binding Path='itemViewModels' }"
    ui:separatorHeight="20"
    ui:themeColor="@color/transparent"
    ui:useDefaultAnimation="false"
    ui:width="500"
    >
    <template>
        <DataTemplate
            ui:templateId="@layout/colorcell_layout"
            ui:templateTag="word"/>
    </template>
</UIMenuView>
```    
Next, open `RootLayout.java` and add two [`UIViewDescriptor`]() instance:
```java
static final UIViewDescriptor DEFAULT_ITEM_STATE = UIViewDescriptor.create().alpha(0.65f).transform(Transform.fromIdentity().build()).sealed();
static final UIViewDescriptor HIGHLIGHT_ITEM_STATE = UIViewDescriptor.create().alpha(1f).transform(Transform.fromIdentity().scale(1.3f).translateX(50.0f).build()).sealed(); 
```

As you can see, the `alpha()` method will set the transparency, the value `0f` mean totally transparent and `1f` mean totally opaque. The `transform()` method make the transformations such as `scale`, `translateX`, `translateY` and so on (More information you can look at [Animation](http://google.com) guide section).
 
`DEFAULT_ITEM_STATE` will be the state for normal items in our `UIMenuView` which make the item transparent with `alpha = 0.65f` and `HIGHLIGHT_ITEM_STATE` will be the state for highlighted item which make it fully display with `alpha = 1f`, scale up to 1.3 time and translate 50px to the right from its original place. 

Now we make use of those attributes by inserting some lines of code in `onInitialize()`:
```java
@Override
public void onInitialize(Bundle bundle) {
    viewModel = new ColorMenuViewModel(this);
    setAndBindRootContentView(R.layout.colorlist_layout, viewModel);
    menuView = (UIMenuView) findUIViewById(R.id.listColor);
    menuView.controlBySide(Side.Both);
    menuView.setItemViewState(
            UIItemViewState.create()
                    .normalState(DEFAULT_ITEM_STATE)
                    .highlightState(HIGHLIGHT_ITEM_STATE)
    );
    addViewEventListener(UIView.SwipeEvent, swipeHandler);
}
```
You can build your app again now and see the new animations. 
