# Animation

## Overview
In InAiR, animation is used everywhere to animate the views smoothly from state to state to make better user experience. InAiR makes use of Android's [`AnimatorSet`](http://developer.android.com/reference/android/animation/AnimatorSet.html) and [`Animator`](http://developer.android.com/reference/android/animation/Animator.html) to apply animation to UIViews. We provide a helper class [`UIAnimation`](#ui-animation) to make declaring animation easier.

## Implement
**Prerequisites**
Simply, the UIView you want to apply animation to, either declared in xml file that could be get through **findUIViewById()**, or programmatically initialized.

Using [`UIAnimation`](#ui-animation) static methods helps you easily create the animators that apply animation to the specific view. And the rest is similar to Android, you can play the animator instantly, or play it sequentially/together with other animators by an instance of [`AnimatorSet`](http://developer.android.com/reference/android/animation/AnimatorSet.html).

For example, you want to translate an image 500px by X-axis, and animate its alpha to 0.5f, in a duration of 2 seconds simultaneously. Let's look at the code below:

```java
// Initialize the view
UIImageView imageView = new UIImageView(this);
imageView.setSource(getResources().getDrawable(R.drawable.ic_inairlogo));
imageView.setSize(200, 200);
imageView.setPosition(860, 440, 0);

// Add our view to the root view
rootView.addView(imageView);

// Create the target descriptor with UIViewDescriptor
UIViewDescriptor imageDescriptor = UIViewDescriptor.createFromView(imageView);
imageDescriptor.translateX(300.0f);
imageDescriptor.alpha(0.5f);

// Then simply create an animator with the help of UIAnimation.createAnimationForView()
Animator animator = UIAnimation.createAnimationForView(imageView, imageDescriptor, 2000);

// The only thing left is to start the animator
animator.start();

```
That's it, with just these simple lines of code, the image will smoothly translate 300px to the right and change its transparency to 0.5f in 2 seconds.

Take a look at [`UIAnimation`](#ui-animation) and [`UIViewDescriptor`](#ui-view-descriptor) class for more useful functions.