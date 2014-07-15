###Overview
The `UILayeredNavigation` class implements a specialized layout that manages the navigation of content in Z-axis layers. This navigation interface makes it possible to present your data efficiently and makes it easier for the user to navigate that content.

Each Layer of a `UILayeredNavigation` interface is associated with a custom layout. When the user navigates to a specific layer, the `UILayeredNavigation` displays the root view of the corresponding view layout, and hiding any previous views. (User taps always display the root view of the tab, regardless of which tab was previously selected. This is true even if the tab was already selected.) Because selecting a tab replaces the contents of the interface, the type of interface managed in each tab need not be similar in any way. In fact, tab bar interfaces are commonly used either to present different types of information or to present the same information using a completely different style of interface. Figure 1 shows the tab bar interface presented by the Place application, each tab of which presents an short description of each place.

![Figure 1](http://developer.inair.tv/upload_file/attachment/0716035118.png "Figure 1")

###In this section:
1. [Setting up the Layered Navigation](http://developer.inair.tv/knowledgebase/1.%20Setting%20up%20the%20Layered%20Navigation)
2. [Binding data source](http://developer.inair.tv/knowledgebase/index.php?InAiR-Documentation/A.%20Getting%20Started/2.%20Using%20Collection%20View/1.%20Using%20the%20Layered%20Navigation/2.%20Binding%20data%20source)
3. [Programatically way](http://developer.inair.tv/knowledgebase/index.php?InAiR-Documentation/A.%20Getting%20Started/2.%20Using%20Collection%20View/1.%20Using%20the%20Layered%20Navigation/3.%20Programatically%20way)