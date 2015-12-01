###Overview
A collection view facilitates the presentation of a set of data provided by your app. The collection view’s only concern is to take your views and lay them out in a specific way, for example a UIListView presents its item views into a single column layout. Collection view is all about the presentation and arrangement of your views and not about their content.

Current version of inAiR-SDK has three type of collection views: `UILayeredNavigation`, `UIListView` and `UIMenuView`.

###Introduction

When using a collection view, the first thing you might wonder is how can we set data source for a collection or can we have diffirent views for diffirent types of data? The anwser is there are two properties which are avaialble in all of our collection views: `ItemsSource` and `ItemTemplate`.

An example of using Collection view in a xml layout file:
```xml
<?xml version="1.0" encoding="utf-8"?>
<UILayeredNavigation
  xmlns:ui="http://schemas.android.com/apk/res-auto"
  ui:itemsSource="{ Binding Path='viewItemsSource' }"
  ui:itemTemplate="@layout/layered_datatemplate"
/>
```

>The `ItemsSource` property represents data source of collection view and needs to be a list of items view model.

If you want your collection view to update automatically when your item source changes (for example, when adding more items, deleting items...) `ItemsSource` must have ObservableCollection type, a data type similar to List type in Java, which raise events when collection changed.

The `ItemTemplate` property represents a template view for each item view when it's populated from data source. `ItemTemplate` must refer to a xml file which contain a `DataTemplate` element.

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
Using [UILayeredNavigation](http://developer.inair.tv/knowledgebase/index.php?InAiR-Documentation/A.%20Getting%20Started/2.%20Using%20Collection%20View/1.%20Using%20the%20Layered%20Navigation) | Collection view that manages the navigation of content in Z-axis layers
Using [UIListView](http://developer.inair.tv/knowledgebase/index.php?InAiR-Documentation/A.%20Getting%20Started/2.%20Using%20Collection%20View/2.%20Using%20the%20List%20View) | Collection view that similar to Android ListView.
Using [UIMenuView](http://developer.inair.tv/knowledgebase/index.php?InAiR-Documentation/A.%20Getting%20Started/2.%20Using%20Collection%20View/3.%20Using%20the%20Menu%20View) | Collection view that specialize for presenting inAiR menu view.