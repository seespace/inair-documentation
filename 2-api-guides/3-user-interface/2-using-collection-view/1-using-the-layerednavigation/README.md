###Overview
The `UILayeredNavigation` class implements a specialized layout that manages the navigation of content in Z-axis layers. This navigation interface makes it possible to present your data efficiently and makes it easier for the user to navigate that content.

Each Layer of a `UILayeredNavigation` interface is associated with a custom layout. When the user navigates to a specific layer, the `UILayeredNavigation` displays the root view of the corresponding view layout, and hiding any previous views. (User taps always display the root view of the tab, regardless of which tab was previously selected. This is true even if the tab was already selected.) Because selecting a tab replaces the contents of the interface, the type of interface managed in each tab need not be similar in any way. In fact, tab bar interfaces are commonly used either to present different types of information or to present the same information using a completely different style of interface.

###In this section:
1. [Setting up the Layered Navigation](1-setting-up-the-layerednavigation.md)
2. [Binding data source](2-binding-data-source.md)
3. [Programatically way](3-programatically-way.md)