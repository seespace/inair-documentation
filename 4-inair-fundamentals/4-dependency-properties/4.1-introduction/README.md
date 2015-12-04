4.1 Introduction DP
===

When you begin to develop appliations with WPF, you will soon stumble across DependencyProperties. They look quite similar to normal .NET properties, but the concept behind is much more complex and powerful.

The main difference is, that the value of a normal .NET property is read directly from a private member in your class, whereas the value of a DependencyProperty is resolved dynamically when calling the GetValue() method that is inherited from DependencyObject.

When you set a value of a dependency property it is not stored in a field of your object, but in a dictionary of keys and values provided by the base class DependencyObject. The key of an entry is the name of the property and the value is the value you want to set.

**The advantages of dependency properties are:**

* **Reduced memory footprint** <br />
It's a huge dissipation to store a field for each property when you think that over 90% of the properties of a UI control typically stay at its initial values. Dependency properties solve these problems by only store modified properties in the instance. The default values are stored once within the dependency property.

* **Value inheritance** <br />
When you access a dependency property the value is resolved by using a value resolution strategy. If no local value is set, the dependency property navigates up the logical tree until it finds a value. When you set the FontSize on the root element it applies to all textblocks below except you override the value. 

* **Change notification** <br />
Dependency properties have a built-in change notification mechanism. By registering a callback in the property metadata you get notified, when the value of the property has been changed. This is also used by the databinding.

