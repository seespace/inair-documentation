InAir framework use MVVM as a main pattern for building application.

# MVVM Pattern

The Model-View-ViewModel (MVVM) pattern helps you to cleanly separate the business and presentation logic of your application from its user interface (UI). Maintaining a clean separation between application logic and UI helps to make your application much easier to test, maintain, and evolve. It can also greatly improve code reusability and allows developers and UI designers to more easily collaborate when developing their respective parts of the application.

## Class Responsibilities and Characteristics

In the MVVM pattern, the view encapsulates the UI and any UI logic, the view model encapsulates presentation logic and state, and the model encapsulates business logic and data. The view interacts with the view model through data binding, commands, and change notification events. The view model queries, observes, and coordinates updates to the model, converting, validating, and aggregating data as necessary for display in the view.

![Image](http://developer.inair.tv/upload_file/attachment/IC448690.png)

### The View Class

The view's responsibility is to define the structure and appearance of what the user sees on the screen. It data context is set to the view model, and the view model implements properties and commands to which the view can bind and notifies the view of any changes in state through change notification events. There is typically a one-to-one relationship between a view and its view model.

**Communication:** View and model view communicate via data binding or change notification events implemented in model view.

### The View Model Class

The view model in the MVVM pattern encapsulates the presentation logic and data for the view. It has no direct reference to the view or any knowledge about the view's specific implementation or type. 

**Communication:** The view model implements properties and commands to which the view can data bind and notifies the view of any state changes through change notification events. The properties and commands that the view model provides define the functionality to be offered by the UI, but the view determines how that functionality is to be rendered.

The view model is responsible for coordinating the view's interaction with any model classes that are required. Typically, there is a one-to many-relationship between the view model and the model classes. The view model may choose to expose model classes directly to the view so that controls in the view can data bind directly to them. In this case, the model classes will need to be designed to support data binding and the relevant change notification events.

### The Model Class

The model in the MVVM pattern encapsulates business logic and data. Business logic is defined as any application logic that is concerned with the retrieval and management of application data and for making sure that any business rules that ensure data consistency and validity are imposed. To maximize re-use opportunities, models should not contain any use case–specific or user task–specific behavior or application logic.

Typically, the model represents the client-side domain model for the application. It can define data structures based on the application's data model and any supporting business and validation logic. The model may also include the code to support data access and caching, though typically a separate data repository or service is employed for this.

**Communication:** the model can be accessed directly in Model View, and changed in model can be notified to model view via notification events

