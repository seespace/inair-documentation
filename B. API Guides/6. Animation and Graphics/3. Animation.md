InAir makes use of Android's [`AnimatorSet`](http://developer.android.com/reference/android/animation/AnimatorSet.html(android.animation.Animator)) class to apply animation to UIViews. We provide a helper class `UIAnimation` to make declaring animation easier.

Let's look at the following example:

```java

   UIView view = ...   // we have view initialize in somewhere

   // This is a set of animation so we make a set
   AnimatorSet animSet = new AnimatorSet();

   // Set the animation duration to be 1000ms (1 sec)
   animSet.setDuration(1000);

   // Interpolation aka Easing for animation
   animSet.setInterpolator(new InOutQuadInterpolator());

   // matrix with scale function
   float[] scaleTransform = UIAnimation.identityMatrix();
   Matrix.scaleM(scaleTransform, 0, 1.2f, 2.0f, 0.0f);

   // create scale animation
   Animator scaleAnim = UIAnimation.createTransformAnimation(view, scaleTransform);

   // create alpha animation
   Animator alphaAnim = UIAnimation.createAlphaAnimation(view, alpha);

   // setup animation chain
   animSet.play(scaleAnim).with(alphaAnim);
   ...

   ...
   // run animation
   animSet.start();
```

The first lines of code assume that we get the target view from somewhere, either by `findUIViewWithId` from XML layouts, or creating a view programatically.

This `AnimatorSet` class plays a set of Animator objects in the specified order. Animations can be set up to play together, in sequence, or after a specified delay. The following lines setup the basic properties of the `AnimatorSet` such as duration and easing interpolation.


For this example, we wanted to __scale__ and object and change its __Alpha value__ (transparency). For scaling, we create a new float array that represent a __Matrix__ and apply an __scale transformation__([see our transformation article](#)) to the matrix. Then we create an [`Animator`](http://developer.android.com/reference/android/animation/Animator.html) that links between an UIView and a transformation matrix using [`UIAnimation`](http://developer.inair.tv/documents/inair/view/UIAnimation.html) which is basically InAir's helper for generating `Animator`. To create an animator that changes the Alpha value of the view, we simply pass an __`float`__ to `UIAnimator`'s `createAlphaAnimation` function.

Finally, we excecute the animation chain by invoking `animSet.play(scaleAnim).with(alphaAnim)`

If all done correctly, the view will smoothly resize and change its transparency in 1 second.