This lesson will teach you how to create an `UIListView` with custom list items without XML Layout.
Notice that : not all the views in this guide are programmatically created, but the `UIListView`, as we're talking about `UIListView`. And sure, you can programmatically create all those views.

Let's start from our recent `UIListView` demo app.

### Review the Main_Layout
The main Layout in our recent demo app is a `UILayeredViewItem` that contains an `UIListView` with two list item templates for the odd and even item, and some attributes.
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
### Programmatically create UIListView 
Open `MainViewLayout`, which define the only layout for our app. Instead of set content view from XML, we create an `UILayeredViewItem` object named `root`.
```java 
	@Override
    public void onInitialize(Bundle bundle) {
        UILayeredViewItem root = new UILayeredViewItem(this);
        setAndBindRootContentView(root, new MainViewModel(this));

    } 
```
Now, as we discussed before, the `UILayeredViewItem` contains `UIListView` so we create a `UIListView` item and set it as the content view of `root`
```java
@Override
  public void onInitialize(Bundle bundle) {
      UILayeredViewItem root = new UILayeredViewItem(this);
	UIListView listView = new UIListView(this);
	root.setContentView(listView);
      setAndBindRootContentView(root, new MainViewModel(this));
  } 
```
Next, we're going to set the list view item templates for `UIListView`. Create 2 `DataTemplate` for odd and even list items with these XML Layout. Then wrap them into a `DataTemplateSet`. Set the data template for `UIListView` with this `DataTemplateSet` and we have:
```java
@Override
public void onInitialize(Bundle bundle) {
    UILayeredViewItem root = new UILayeredViewItem(this);
    UIListView listView = new UIListView(this);
    DataTemplateSet dataTemplateSet = new DataTemplateSet(this);
    DataTemplate odd = new DataTemplate(this,R.layout.left_layout, "left");
    DataTemplate even = new DataTemplate(this,R.layout.right_layout, "right");
    try {
        dataTemplateSet.addTemplate(odd);
        dataTemplateSet.addTemplate(even);
    } catch (IAException e) {
        e.printStackTrace();
    }
    listView.setItemTemplate(dataTemplateSet);
    root.setContentView(listView);
    setAndBindRootContentView(root, new MainViewModel(this));
}
```
Finally, bind list items data for `UIListView`. We've known that the data for list items is `itemViewModels` property of `MainViewModel`. So create a `MainViewModel` then bind data and do not forget binding root's content view data object to that new `MainViewModel`:
```java
@Override
public void onInitialize(Bundle bundle) {
    UILayeredViewItem root = new UILayeredViewItem(this);
    UIListView listView = new UIListView(this);
    DataTemplateSet dataTemplateSet = new DataTemplateSet(this);
    DataTemplate odd = new DataTemplate(this,R.layout.left_layout);
    DataTemplate even = new DataTemplate(this,R.layout.right_layout);
    try {
        DataTemplate odd = new DataTemplate(this,R.layout.left_layout, "left");
    	DataTemplate even = new DataTemplate(this,R.layout.right_layout, "right");
    } catch (IAException e) {
        e.printStackTrace();
    }
    listView.setItemTemplate(dataTemplateSet);

    MainViewModel mainViewModel = new MainViewModel(this);
    listView.setItemsSource(mainViewModel.itemViewModels);

    root.setContentView(listView);
    setAndBindRootContentView(root, mainViewModel);
}
```
And now you can try again to Build and Run your project. Enjoy!
