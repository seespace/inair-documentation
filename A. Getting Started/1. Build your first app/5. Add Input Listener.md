In the last lesson, we've successfully binded some UIView's properties to the Model View, which means that any time those properties in the model view is changed, the corresponding binded values in the View will be changed and the change will be visible right away on the display.


### Setting up the data

To continue our task of building a SlideShow, let's create a new class `PhotoItem` to hold information about a photo:

```java
public class PhotoItem {

  //Constructor
  public PhotoItem(int photoId, String photoName, String photoDescription) {
    this.photoId = photoId;
    this.photoName = photoName;
    this.photoDescription = photoDescription;
  }


  public int getPhotoId() {
    return photoId;
  }

  public void setPhotoId(int photoId) {
    this.photoId = photoId;
  }

  private int photoId;


  public String getPhotoName() {
    return photoName;
  }

  public void setPhotoName(String photoName) {
    this.photoName = photoName;
  }

  private String photoName;



  public String getPhotoDescription() {
    return photoDescription;
  }

  public void setPhotoDescription(String photoDescription) {
    this.photoDescription = photoDescription;
  }

  private String photoDescription;


}

```

Our `PhotoItem` has 3 properties `photoId`, `photoName`, `photoDescription` and an constructor that directly assigns values for those properties. Now let's get back to our ModelView class `TestModelView` and add a new `ArrayList` of `PhotoItem`, and an __`int`__ that keep an index on which  `PhotoItem` is being shown.

```java
public class TestModelView extends ViewModel {

  private BitmapDrawable imageSrc;
  private String photoName;
  private String photoDescription;

  private int index;
  private ArrayList<PhotoItem> images;

  ...
```

Then in our _constructor_, let's init and add some data for the `ArrayList<PhotoItem>`:

```java
  // Constructor
  public TestModelView() {
    images = new ArrayList<PhotoItem>();
    //Add some dummies data, make sure you have all the photos in your resource dir.
    images.add(new PhotoItem(R.drawable.photo1, "Pharetra Dapibus", "Lorem ipsum dolor sit amet, consectetur adipiscing elit."));
    images.add(new PhotoItem(R.drawable.photo2, "Commodo Dapibus", "Nullam id dolor id nibh ultricies vehicula ut id elit."));
    images.add(new PhotoItem(R.drawable.photo3, "Tristique Vestibulum", "Cras justo odio, dapibus ac facilisis in, egestas eget quam."));
    images.add(new PhotoItem(R.drawable.photo4, "Quam Bibendum", "Morbi leo risus, porta ac consectetur ac, vestibulum at eros."));
    images.add(new PhotoItem(R.drawable.photo5, "Nullam Ridiculus", "Lorem ipsum dolor sit amet, consectetur adipiscing elit."));

    this.nextPhoto();

  }
```

Now, we create a new public function that set a PhotoItem information to the ModelView's binded properties. The same function is called within the constructor to initialize the binded properties for the first time.

```java

  public void nextPhoto() {

    index ++;
    int i = index % images.size();

    PhotoItem photo = images.get(i);
    this.setImageSrc((BitmapDrawable)resources.getDrawable(photo.getPhotoId()));
    this.setPhotoName(photo.getPhotoName());
    this.setPhotoDescription(photo.getPhotoDescription());
  }
```

Good work, now we have our ModelView ready with some dynamic data. What left todo now is invoking `nextPhoto` function everytime the user _double tap_on anywhere on the controller.

### Listening for InputEvent

Events listening are almost always done from the __Layout Class__. In our case, Open the existing `TestLayout` class. Let's take a look inside:

```java
public class TestLayout extends IABaseRootLayout {

  @Override
  public void onInitialize(Bundle savedInstanceState) {
    setAndBindRootContentView(R.layout.test_layout, Application.modelView);
  }
}
```
In InAir, a __Layout Class__ works like a ViewController in MVC pattern, it manages the behaviour of a Layout in our resource directory. In our current case, `TestLayout` manages the views in `test_layout.xml`. The __Layout Class__ has a method `onInitialize` that is invoked very early when the layout is created. The `setAndBindRootContentView` method bind the Layout class to a Model View class `Application.modelView` which is our`TestModelView`.

To handle _double tap_, let's create a public method inside `TestLayout` class and invoke our Model View's `nextPhoto` method declared in the previous section:

```java
  public void onDoubleTap(Object sender, TouchEventArgs args) {
    Application.modelView.nextPhoto();
  }
```

In order to listen for double tap event, we need to use any UIView in out layout to intercept a `DoubleTapEvent`. We can get an UIView by assigning __id__ to any element and make it __focusable__. For this lesson, let's assign to our root `UIViewGroup`, the properties we need to add are `ui:id` and `ui:isFocusable` respectively:

__test_layout.xml__
```xml
<UIViewGroup
  xmlns:tools="http://schemas.android.com/tools"
  xmlns:ui="http://schemas.android.com/apk/res-auto"
  tools:context=".TestLayout"
  ui:id="@+id/root"
  ui:isFocusable="true"
  ...
```

Now we get back to our __TestLayout__ class and add the following code to our `onInitialize` method:

```java
  public void onInitialize(Bundle savedInstanceState) {
    setAndBindRootContentView(R.layout.test_layout, Application.modelView);

    UIView rootViewGroup = findUIViewById(R.id.root);
    rootViewGroup.focus();


    rootViewGroup.addHandler(UIView.DoubleTapEvent, Delegate.create(this, "onDoubleTap", TouchEventArgs.class));
  }

```

The `findUIViewById(R.id.root)` method returns an UIView with id _"root"_ that we gave to our UIViewGroup. UIView's `.focus()` method tell the UIView to intercept Input events, and finally `rootViewGroup.addHandler(UIView.DoubleTapEvent, Delegate.create(this, "onDoubleTap", TouchEventArgs.class));` make our UIView to handles Event with the type `UIView.DoubleTapEvent`, then invoke our `onDoubleTap` method declared previously. To learn more about Handling inputs, please read our [Events Guide](http://developer.inair.tv/knowledgebase/index.php?InAiR-Documentation/B.%20API%20Guides/7.%20Events/1.%20Event).

That is, you can now try to Build and Run your project.

Get the full source code for this demo here: [https://github.com/seespace/hello-world-example](https://github.com/seespace/hello-world-example)