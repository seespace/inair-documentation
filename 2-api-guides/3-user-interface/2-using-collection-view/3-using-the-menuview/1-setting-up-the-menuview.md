The following of this guide will guide you through building simple Color Application as in Figure 1. 

First of all: Create your app using **InAir Blank App Template**.

###Creating the Main Layout XML File:
Create a `menuview_layout.xml` in `res/layout` directory and set up a `ViewGroup` that would contain our `UIMenuView` with some specific like below:
```xml
<?xml version="1.0" encoding="utf-8"?>
<UIViewGroup
    xmlns:ui="http://schemas.android.com/apk/res-auto"
    ui:positionX="430"
    ui:width="250"
    ui:height="1080"
    ui:boundToContentSize="false">
	
	<UIMenuView>
	
	</UIMenuView>
</UIViewGroup>
```
Then define some attribute for our `UIMenuView` 
```xml
<UIMenuView
    ui:height="1080"
	ui:width="500"
    ui:highlightColor="@color/transparent"
    ui:id="@+id/listColor"
    ui:separatorHeight="20"
    ui:themeColor="@color/transparent"
    ui:useDefaultAnimation="false"
    >
</UIMenuView>
```
###Define data template
Create new `menuview_item_layout.xml` in `res/layout`. It has a color name next to the correspond color rectangle. This is our `UIMenuView` item layout.

Complete `menuview_item_layout.xml` file:
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
        ui:text="color"
        ui:fontSize="40" />
</UIViewGroup>  
```
Now, just like in [`UIListView` Guide](http://google.com), we insert `<template>` element with `<DataTemplate>` to define the item layout which `UIMenuView` will display.
```xml
UIMenuView
    ui:height="1080"
    ui:highlightColor="@color/transparent"
    ui:id="@+id/listColor"
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
```
Your application is nearly completed. Proceed to the next lesson to learn how you can use *Binding* to complete the application and some *Animations* to make your app more visually.
