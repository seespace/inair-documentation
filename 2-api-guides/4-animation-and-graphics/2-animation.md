# Animation

## Overview
In InAiR, animation is used everywhere to animate the views smoothly from state to state to make better user experience. InAiR makes use of Android's [`AnimatorSet`](http://developer.android.com/reference/android/animation/AnimatorSet.html) and [`Animator`](http://developer.android.com/reference/android/animation/Animator.html) to apply animation to UIViews. We provide a helper class [`UIAnimation`](#ui-animation) to make declaring animation easier.

## Implement
**Prerequisites**
Simply, the UIView you want to apply animation to, either declared in xml file that could be get through **findUIViewById()**, or programmatically initialized.

Using [`UIAnimation`](#ui-animation) static methods helps you easily create the animators that apply animation to the specific view. And the rest is similar to Android, you can play the animator instantly, or play it sequentially/together with other animators by an instance of [`AnimatorSet`](http://developer.android.com/reference/android/animation/AnimatorSet.html).

For example, you want to translate an image 200px by X-axis, and animate its alpha to 0.5f, in a duration of 2 seconds simultaneously. Let's look at the implement code below:

```java

   UIImageView imageView = ...   // we have view initialize in somewhere
   
   // Let's create the translate tranform
   float[] translateTransform = TransformTransform.fromIdentity().translateX(200.0f).build();
   // and the target alpha
   float targetAlpha = 0.5f;
   // also the animation duration (in ms)
   long duration 2000;
   
   // Then simply create an animator with the help of UIAnimation.createAnimationForView()
   Animator anim = UIAnimation.createAnimationForView(imageView, translateTransform, targetAlpha, duration);
   
   // The only thing left is to start the animator
   animator.start();
   
```
That's it, with just these simple lines of code, the image will smoothly translate 200px to the X-axis and change its transparency to halve in 2 seconds.

Take a look at [`UIAnimation`](#ui-animation) class for much more convenient methods to play with. Have fun!