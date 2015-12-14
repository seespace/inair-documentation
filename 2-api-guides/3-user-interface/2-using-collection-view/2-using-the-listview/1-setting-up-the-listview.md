# Setting up the List View

The following of this tutorial will guide you through building simple Color Application.

__First of all__: Create your app using InAir Blank App Template.

### Creating the Main Layout XML File: 

Create the `main_layout.xml` file in `res/layout` directory. Since this application using a `UIListView`, we need to create an empty `UIListView` element as this code below. 
```xml
<?xml version="1.0" encoding="utf-8"?>
<UILayeredViewItem
    xmlns:ui="http://schemas.android.com/apk/res-auto">

    <UIListView
    </UIListView>
</UILayeredViewItem>
```

### Define data template
Create new XML file named `right_layout.xml` and put it into `res/layout`. We use this file as a template for right color item of list view. Following the design, we need an `UIRectView` to present color and an `UITextView` to show a color name.

Complete `right_layout.xml` file:

```xml
<?xml version="1.0" encoding="utf-8"?>
<UIViewGroup
	xmlns:ui="http://schemas.android.com/apk/res-auto">

<UIRectView
	ui:height="100"
	ui:width="100"
	ui:color="#ffffffff" />

<UITextView
	ui:width="250"
	ui:positionX="105"
	ui:positionY="20"
	ui:text="White"
	ui:textSize="40" />

</UIViewGroup>
```

We need to create another XML file named `left_layout.xml` and save it to `res/layout`. This file will be used as a template for left color item of list view. Just like `right_layout.xml`.

Complete `left_layout.xml` file:
```xml
<?xml version="1.0" encoding="utf-8"?>
<UIViewGroup
	xmlns:ui="http://schemas.android.com/apk/res-auto">

<UITextView
    ui:width="250"
    ui:positionY="20"
    ui:text="White"
    ui:textSize="40" />

<UIRectView
	ui:positionX="255"
	ui:height="100"
	ui:width="100"
	ui:color="#ffffffff" />

</UIViewGroup>
```
    
Now we have all materials to create the item data template for the UIListView. Insert `template` element with two `DataTemplate` to determind they layouts which `UIListView` will display its item.

Complete the XML file: 

```xml
<?xml version="1.0" encoding="utf-8"?>
<UILayeredViewItem
    xmlns:ui="http://schemas.android.com/apk/res-auto">

    <UIListView>
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
Now your application is nearly completed. Proceed to the next tutorial to learn how you can use *Binding* to complete the application.
