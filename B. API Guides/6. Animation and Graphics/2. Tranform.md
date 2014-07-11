Before beginning our lesson, there're two concepts we need to learn about the coordinate spaces: __user space__, which represents the element's view, and __device space__, which represents the native resolution of a device. User space coordinates are floating-point numbers that are unrelated to the resolution of pixels in device space. When you want to print or display your UI element, Quartz maps user space coordinates to device space coordinates. Therefore, you never have to rewrite your application or write additional code to adjust the output from your application for optimum display on different devices.

You can modify the default user space by operating on the __current transformation matrix__, or CTM. After you create a graphics context, the CTM is the identity matrix. You can use [Android's Matrix](http://developer.android.com/reference/android/opengl/Matrix.html) functions to modify the CTM and, as a result, modify drawing in user space.

##Transformation Functions

You can easily translate, scale, and rotate your drawing using the Android's built-in Matrix transformation functions. With just a few lines of code, you can apply these transformations in any order and in any combination. The figure bellow illustrates the effects of scaling and rotating an image. Each transformation you apply updates the CTM. The CTM always represents the current mapping between user space and device space. This mapping ensures that the output from your application looks great on any display screen.

> <img src="http://inair.tv/wp-content/uploads/shared/transform1.png" width="600"/>


## Modifying the Current Transformation Matrix

The following line of code get an image from it's layout file then apply some simple transfomation:

```java

//Get image from the Layout
UIImageView image = (UIImageView)findUIViewById(R.id.image);

//Create and init a new transformation matrix
float[] transform = UIAnimation.identityMatrix();

//Apply transformation to the transform matrix

Matrix.scaleM(transform, 0, 0.5f, 0.5f, 1.0f);
Matrix.rotateM(transform, 0, 45, 0, 1f, 0f);
Matrix.translateM(transform, 0, -300f, 300f, 0);

//Set to the current CTM
image.setTransform(transform);

```
Here's the result
> <img src="http://inair.tv/wp-content/uploads/shared/transform2.png" width="600"/>

If you want to return to the original object as defined in the layout file, then just setTransform as an Identity Matrix

```java
image.setTransform(UIAnimation.identityMatrix());
```

> **Note:** the translate function is affected by other previous transformation, e.g: if you scaled the object by 0.5, then translate the object 400px, then on the __device space__ (TV) is appeared to be translated only 200px; if you rotated the object previously, then translating the X-axis wouldn't always move horizontally.

