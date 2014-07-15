###Overview
A collection view facilitates the presentation of a set of data provided by your app. The collection view’s only concern is to take your views and lay them out in a specific way, for example a UIListView presents its item views into a single column layout. Collection view is all about the presentation and arrangement of your views and not about their content.

Current version of inAiR-SDK has three type collection views `UILayeredNavigation`, `UIListView` and `UIMenuView`.

###First touch
When using a collection view, first thing you might wonder is how can we set data source for this collection or can we have diffirent view for diffirent type of data? The anwser is there are two properties which are avaialble in all our collection view `ItemsSource` and `ItemTemplate`

An example of using Collection view in a xml layout file
```xml
<?xml version="1.0" encoding="utf-8"?>
<UILayeredNavigation
  xmlns:ui="http://schemas.android.com/apk/res-auto"
  ui:itemsSource="{ Binding Path='viewItemsSource' }"
  ui:itemTemplate="@layout/layered_datatemplate"
/>
```

* The `ItemsSource` property represents data source of collection view and needs to be a list of items view model.

If you want your collection view to update automatically when your item source changes (for example, when adding more item, deleting item, ...) `ItemsSource` must be an ObservableCollection instance. ObservableCollection is a data type which is similiar to List type in Java, the different is it will raise event when collection changed.

* The `ItemTemplate` property represents a template view for each item view when it's populated from data source. `ItemTemplate` must be an xml file which contain a `DataTemplate` element.

`DataTemplale` is an object that defines a relationship between a layout view, represented by `templateId` attribute, and a data tag, represented by `templateTag`. Following is a simple data template file:
```xml
<?xml version="1.0" encoding="utf-8"?>
<MutilDataTemplate xmlns:ui="http://schemas.android.com/apk/res-auto">
    <DataTemplate
        ui:templateId="@layout/first_layout"
        ui:templateTag="firstlayer"/>
    <DataTemplate
        ui:templateId="@layout/second_layout"
        ui:templateTag="secondlayer"/>
</MutilDataTemplate>
```

###In this section
Topic         | Description
------------- | -------------
Using [UILayeredNavigation](1. Using the Layered Navigation/) | Layout that manages the navigation of content in Z-axis layers
Using [UIListView](2. Using the List View/) | Arranges child elements into vertical line.
Using [UIMenuView](3. Using the Menu View/) | Represent a menu control that layout child elements into a vertical line.