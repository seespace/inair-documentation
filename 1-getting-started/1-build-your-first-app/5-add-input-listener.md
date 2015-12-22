Add Input Listener
==================

So far, we've built an InAiR application that displays a beautiful photo with its title & description. In the quest of building a slideshow, let's add more photo and some basic interactions.


Setting up data
---------------

1. In Android Studio, open `MainActivity.java` file.
2. Before `onInitialize(Bundle bundle)` method, add a field declaration that holds our view models:
    ```java
    private ArrayList<MainViewModel> mViewModels = new ArrayList<>();
    ```
3. In `onInitialize(Bundle bundle)` method, delete the code `setDataContext(new MainViewModel(this));`
3. Add the following code right after:
    ```java
    // Create 5 view models holding data of our photo
    MainViewModel viewModel1 = new MainViewModel(this);
    viewModel1.setPhotoSrc((BitmapDrawable) getResources().getDrawable(R.drawable.photo1));
    viewModel1.setPhotoTitle("Pharetra Dapibus");
    viewModel1.setPhotoDescription("Lorem ipsum dolor sit amet, consectetur adipiscing elit.");

    MainViewModel viewModel2 = new MainViewModel(this);
    viewModel2.setPhotoSrc((BitmapDrawable) getResources().getDrawable(R.drawable.photo2));
    viewModel2.setPhotoTitle("Commodo Dapibus");
    viewModel2.setPhotoDescription("Nullam id dolor id nibh ultricies vehicula ut id elit.");

    MainViewModel viewModel3 = new MainViewModel(this);
    viewModel3.setPhotoSrc((BitmapDrawable) getResources().getDrawable(R.drawable.photo3));
    viewModel3.setPhotoTitle("Tristique Vestibulum");
    viewModel3.setPhotoDescription("Cras justo odio, dapibus ac facilisis in, egestas eget quam.");

    MainViewModel viewModel4 = new MainViewModel(this);
    viewModel4.setPhotoSrc((BitmapDrawable) getResources().getDrawable(R.drawable.photo4));
    viewModel4.setPhotoTitle("Quam Bibendum");
    viewModel4.setPhotoDescription("Morbi leo risus, porta ac consectetur ac, vestibulum at eros.");

    MainViewModel viewModel5 = new MainViewModel(this);
    viewModel5.setPhotoSrc((BitmapDrawable) getResources().getDrawable(R.drawable.photo5));
    viewModel5.setPhotoTitle("Nullam Ridiculus");
    viewModel5.setPhotoDescription("Lorem ipsum dolor sit amet, consectetur adipiscing elit.");

    // add into mViewModels array, so we can use later 
    mViewModels.add(viewModel1);
    mViewModels.add(viewModel2);
    mViewModels.add(viewModel3);
    mViewModels.add(viewModel4);
    mViewModels.add(viewModel5);

    // by default, we display photo1
    setDataContext(viewModel1);
    ```
5. Add the following method:
    ```java
    // switch to next view model, trigger a change so layout will be automatically updated
    private void next() {
        MainViewModel currentViewModel = (MainViewModel) getDataContext();
        int currentIndex = mViewModels.indexOf(currentViewModel);
        int nextIndex = currentIndex + 1;
        if (nextIndex == mViewModels.size()) {
          nextIndex = 0;
        }
        setDataContext(mViewModels.get(nextIndex));
    }
    ```

What we're doing here is creating a `ArrayList` of 5 `ViewModel` then bind our main layout `MainActivity` to the first item in the list. Everytime the `next()` method is called, the `Activity`'s ViewModel changes and the layout will bind to the new `ViewModel` which updates its photo & text.

Good work, now we have our `ViewModel` ready with some dynamic data. What left to do is invoking `next()` method every time user _double tap_ on anywhere on the controller.

Listening for InputEvent
------------------------

Events handling are almost always done from the __Activity__. 

1. In Android Studio, open `MainActivity.java` file.
2. In `onInitialize(Bundle bundle)` method, add the following code:
    ```java
    // Listen to double tap event
    addViewEventListener(UIView.DoubleTapEvent, onDoubleTap);
    ```
3. Add a new EventListener called `onDoubleTap`:
    ```java
    // Trigger a `next()` when user performs double tap
  private Event.Listener<TouchEventArgs> onDoubleTap = new Event.Listener<TouchEventArgs>() {
    @Override
    public void onTrigger(Object o, TouchEventArgs args) {
      next();
    }
  };
    ```

That's it, you can now Build and Run your project.

You'll need InAiR Remote app to interact with InAiR app you've just built. You can download the app from [here](https://www.inair.tv/remote). Once you have the app, follow below instructions:
1. [Setup Wifi]() for InAiR box
2. [Connect remote control app to InAiR box]()
3. Open this app following standard [InAiR gestures]() control
4. Double tap to change slide


Get the full source code for this demo here: [https://github.com/seespace/hello-world-example](https://github.com/seespace/hello-world-example)