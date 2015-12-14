###Programmatically way
Open the ThirdLayer.java file inside the view package, you should see the following content:
Now, create UILayeredViewItem and setTitle(), setShouldOpen() for this layer:

```java
public class ThirdLayer extends IAFragment {
  @Override
  public void onInitialize(Bundle bundle) {
    UILayeredViewItem root = new UILayeredViewItem(this);
    root.setTitle("third");
    root.setShouldOpen(true); 
  }
}
```
After created layer, setContentView for our layer:

```java
  UIViewGroup contentView = new UIViewGroup(this, false , true);

  UITextView textView = new UITextView(this);
  textView.setFontSize(30);
  textView.setWidth(300f);
  textView.setTextAlignment(UITextView.TextAlignment.CENTER);
  textView.setText("Programmatically Views");
  contentView.addView(textView);

  root.setContentView(contentView);

  setRootContentView(root);
```
><h4>Note:</h4>
UILayeredViewItem can have only one content view
