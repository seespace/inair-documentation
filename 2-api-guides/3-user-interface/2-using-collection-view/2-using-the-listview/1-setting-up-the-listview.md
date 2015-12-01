This lesson will guide you through building a simple Color Application like [Figure 1]() in `Overview` section.

__First of all:__ we using InAir Blank App Template

###Creating a list view item
Create new xml with name `right_layout.xml` file and save it to `res/layout` folder. We use this file as a template for right color item of list view. Following design, we need an `UIRectView` to present color and an `UITextView` to show a color name.

Compelete `right_layout.xml` file:
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

We need to create another xml file with name `left_layout.xml` and save it to `res/layout` folder. This file will be used as a template for left color item of list view. Just like `right_layout.xml`.

Compelete `left_layout.xml` file:
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

###Define a data template
Create the `listview_datatemplate.xml` file and save it to `res/layout`.

Complete xml file
```xml
<?xml version="1.0" encoding="utf-8"?>
<MultiDataTemplate xmlns:ui="http://schemas.android.com/apk/res-auto">
    
  <DataTemplate
    ui:templateId="@layout/right_layout"
    ui:templateTag="right"/>

  <DataTemplate
    ui:templateId="@layout/left_layout"
    ui:templateTag="left"/>

</MultiDataTemplate>
```

###Creating the Layout XML File
Open the `main_layout.xml` file from `res/layout` directory. Since this application using a `UIListView`, we need to change the content of this xml file following this code below:

```xml
<?xml version="1.0" encoding="utf-8"?>

<UIListView
  xmlns:ui="http://schemas.android.com/apk/res-auto"
  ui:positionX="1280.0"
  ui:width="400.0"
  ui:height="1080.0"
  ui:itemTemplate="@layout/listview_datatemplate"/>

```

Now your application is nearly completed. Proceed to the next lesson to learn how you can use *Binding* to complete the application.