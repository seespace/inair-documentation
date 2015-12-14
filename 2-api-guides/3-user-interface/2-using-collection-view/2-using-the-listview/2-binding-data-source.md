## Binding data source

This section will show you the basic of creating a model view file and binding to list view items source within InAiR SDK.

### Creating a view model file for item in list view
Create `ColorItemViewModel.java` file and save it to the `viewmodel` package. Since this class is a **view model**, it need to be inherited from `ViewModel` class. Otherwise, the `ColorItemViewModel` is also an item of **collection view**, it need to be implement `ItemViewData` interface and override `getTag()` method to provide tag data for this **item view**. The `ColorItemViewModel.java` should look like this:
```java
package tv.inair.apptemplate.viewmodel;

import ...

public class ColorItemViewModel extends ViewModel implements ItemViewData {

	public ColorItemViewModel(IAContext context) {
  		super(context);
	}
	
	@Override
	public void setUp() {}
	
	@Override
	public void tearDown() {}
	
	@Override
	public CharSequence getTag() {
  		return null;
	}
}
```

In this example, we have two `tag`s for data: `right` and `left`. As you can see in [Finger 1](http://google.com) the odd items using `left` template and even items using `right` template, we will add a property to store its initialize `index` and use this `index` to return the corresponding `tag`:
```java
private int index;
@Override
public CharSequence getTag() {
	return index % 2 == 1 ? "left" : "right";
}
```

Of course, we need two properties to store the color and its description. Those properties shall be used to bind to our layout later. Then generate the Setters & Getters for all properties:
```java
private int color;
private CharSequence description;
   
//Setters & Getters
public CharSequence getDescription() {
	return description;
}

public void setDescription(CharSequence description) {
	this.description = description;
	notifyPropertyChanged("description");
}

public int getColor() {
	return color;
}

public void setColor(int color) {
	this.color = color;
	notifyPropertyChanged("color");
}
```

Notice the lines `notifyPropertyChanged("<property's name>");` that is being used on every Setters? This line will tell the system that the corresponding property has changed and the layout should refresh to update with the new value.
Let's add more parameters to the class's constructor to initialize all properties we need.
```java
    // Constructor
    public ColorItemViewModel(int index, int color, CharSequence description, IAContext context) {
        super(context);
        this.index = index;

        setColor(color);
        setDescription(description);
    }
```    
### Prepare content for each layers
Create the `MainViewModel.java` extends `ViewModel` implements `LayeredItemViewData`. We will use this `MainViewModel` as data context of `main_layout.xml` and the only Layer of our app which contain an `UIListView`:
```java
package tv.inair.apptemplate.viewmodel;
	  
import ...

public class MainViewModel extends ViewModel implements LayeredItemViewData{
    public MainViewModel(IAContext context) {
        super(context);
    }
}
```
Then we create a `ObservableCollection` of `ItemViewData` and change the class's constructor to initialize view model with preparing content:
```java
public ObservableCollection<ItemViewData> itemViewModels = new  ObservableCollection<ItemViewData>();

public MainViewModel(IAContext context) {
	super(context);
    itemViewModels.add(new ColorItemViewModel(1, Color.BLACK, "Black",context));
    itemViewModels.add(new ColorItemViewModel(2, Color.CYAN, "Cyan",context));
    itemViewModels.add(new ColorItemViewModel(3, Color.DKGRAY, "Dark gray",context));
    itemViewModels.add(new ColorItemViewModel(4, Color.GRAY, "Gray",context));
    itemViewModels.add(new ColorItemViewModel(5, Color.GREEN, "Green",context));
    itemViewModels.add(new ColorItemViewModel(6, Color.LTGRAY, "Light gray",context));
    itemViewModels.add(new ColorItemViewModel(7, Color.MAGENTA, "Magenta",context));
    itemViewModels.add(new ColorItemViewModel(8, Color.RED, "Red",context));
    itemViewModels.add(new ColorItemViewModel(9, Color.TRANSPARENT, "Transparent",context));
    itemViewModels.add(new ColorItemViewModel(10, Color.WHITE, "White",context));
    itemViewModels.add(new ColorItemViewModel(11, Color.YELLOW, "Yellow",context));
    itemViewModels.add(new ColorItemViewModel(12, Color.BLUE, "Blue",context));
}
```

### Binding data to layout
Back to our layouts, open previous created `right_layout.xml`. There 're two properties inside this XML we need to change in order to bind with our **Model View** properties declared previously:

• `ui:color` of `UIRectView`

• `ui:text` of `UITextView`

Complete XML file should be like this:
```xml
<?xml version="1.0" encoding="utf-8"?>
<UIViewGroup
	xmlns:ui="http://schemas.android.com/apk/res-auto">
	
	<UIRectView
		ui:height="100"
		ui:width="100"
		ui:color="{ Binding Path='color' }" />
	
	<UITextView
		ui:width="250"
		ui:positionX="105"
		ui:positionY="20"
		ui:text="{ Binding Path='description' }"
		ui:fontSize="40" />

</UIViewGroup>
```
Do the same with `left_layout.xml` file, we will have the finalize content like this:

```xml
<?xml version="1.0" encoding="utf-8"?>
<UIViewGroup
	xmlns:ui="http://schemas.android.com/apk/res-auto">

<UITextView
    ui:width="250"
    ui:positionY="20"
    ui:text="{ Binding Path='description' }"
    ui:fontSize="40" />

<UIRectView
    ui:positionX="255"
    ui:height="100"
    ui:width="100"
    ui:color="{ Binding Path='color' }" />

</UIViewGroup>
```

The syntax `{Binding Path: <property name>} `will tell the layout to look for the corresponding variable inside the model view and listen for changes produced by the binding property's Setter.

Finally, it's the time for grab it together. Open the `main_layout.xml` file from `res/layout`. Add binding code for `itemsSource`:
```xml
<?xml version="1.0" encoding="utf-8"?>
<UILayeredViewItem
	xmlns:ui="http://schemas.android.com/apk/res-auto">

    <UIListView
   		ui:itemsSource="{ Binding Path='itemViewModels' }">
    
	    <template>
		    <DataTemplate
			    ui:templateId="@layout/right_layout"
			    ui:templateTag="right"/>
		    
		    <DataTemplate
			    ui:templateId="@layout/left_layout"
			    ui:templateTag="left"/>
	    </template>
    </UIListView>
</UILayeredViewItem>
```
__That is, you can now try to Build and Run your project.__
