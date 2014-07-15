This lesson will guide you through building a simple Place Application like [Figure 1]() in `Overview` section.

__First of all:__ we using InAiR Layered App Template

###Creating a layered view
Open the `first_layout.xml` file from `res/layout`

```xml
<?xml version="1.0" encoding="utf-8"?>
<UIViewGroup xmlns:ui="http://schemas.android.com/apk/res-auto">

  <UIImageView
    ui:width="310"
    ui:height="248"
    ui:positionX="0"
    ui:positionY="100"
    ui:src="@drawable/logohi" />

  <UITextView
    ui:width="310"
    ui:positionX="0"
    ui:positionY="400"
    ui:text="InAiR - This is the first layer with static content"
    ui:textSize="40" />

</UIViewGroup>
```

We use this file as a template for each layer of layered navigation. Following design, we need an `UIImageView` to show an image of the place and an `UITextView` to present a short description.

###Define a data template
Open the `layered_datatemplate.xml` file from `res/layout`

Since this application only need one template, we remove the second `DataTemplate` element from this file.

Complete xml file
```xml
<?xml version="1.0" encoding="utf-8"?>
<MultiDataTemplate xmlns:ui="http://schemas.android.com/apk/res-auto">
  <DataTemplate
    ui:templateId="@layout/first_layout"
    ui:templateTag="firstlayer"/>
</MultiDataTemplate>
```

###Creating the Layout XML File
Open the `layered_navigation.xml` file from `res/layout` directory.

```xml
<?xml version="1.0" encoding="utf-8"?>

<UILayeredNavigationView
  xmlns:ui="http://schemas.android.com/apk/res-auto"
  ui:id="@+id/layeredview"
  ui:itemsSource="{ Binding Path:'layeredItemViewModels' }"
  ui:itemTemplate="@layout/layered_datatemplate"/>

```

In this XML file, we notice the [UILayeredNavigationView]() tag with two attributes present in Collection View overview `itemsSource` and `itemTemplate`
We do not need to change anything here.

Great, now you have the basic layout laid out. Proceed to the next lesson to learn how you can use *Binding* to complete the application.