###Overview
A collection view facilitates the presentation of data-driven views provided by your app. The collection view’s only concern is taking your views and laying them out in a specific way. The collection view is all about the presentation and arrangement of your views and not about their content.

With current version of inAiR-SDK we have `three` collection views `UILayeredNavigation`, `UIListView` and `UIMenuView`.

###First touch
When using a collection view, first thing you maybe wonder how can we set data source for this collection or can we have diffirent view for diffirent type of data? The anwser for you question is two properties which is contained in all our collection view `ItemsSource` and `ItemTemplate`

> An example of using Collection view in layout xml file
```xml
<?xml version="1.0" encoding="utf-8"?>
<UILayeredNavigation
  xmlns:ui="http://schemas.android.com/apk/res-auto"
  ui:itemsSource="{ Binding Path='viewItemsSource' }"
  ui:itemTemplate="@layout/layered_datatemplate"
/>
```

* The `ItemsSource` property stands for data source of collection view and need to be a list of items view model.

> If you want your collection auto update when you item source changes (such as add more item, delete item, ...) `ItemsSource` must be an ObservableCollection ~ a java list that will raise event when collection changed.

* The `ItemTemplate` property stands for template view for each item view when it populates from data source. `ItemTemplate` must be an xml file which contain a `DataTemplate` tag.

> A simple datatemplate file
```xml
<?xml version="1.0" encoding="utf-8"?>
<DataTemplate
  xmlns:ui="http://schemas.android.com/apk/res-auto"
  ui:templateId="@layout/first_layer"
  />
```

> **Notes:** Using binding method with collection view is the easiest way to populate data for a collection view.

###In this section
Topic         | Description
------------- | -------------
Using [UILayeredNavigation](1. Using the Layered Navigation/) | Layout that manages the navigation of content in Z-axis layers
Using [UIListView](2. Using the List View/) | Arranges child elements into a single line that can be oriented vertically.
Using [UIMenuView](3. Using the Menu View/) | Represent a menu control that arranges child elements into a single line that can be oriented vertically.