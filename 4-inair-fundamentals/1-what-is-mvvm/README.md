What's is MVVM Pattern?
===============

The Model-View-ViewModel (MVVM) pattern helps you to cleanly separate the business and presentation logic of your application from its user interface (UI). Maintaining a clean separation between application logic and UI helps to make your application much easier to test, maintain, and evolve. It can also greatly improve code reusability and allows developers and UI designers to more easily collaborate when developing their respective parts of the application.

-------------

 **As anyone can work out by its name it is composed by three elements:**
 

1. **View**
    * **Responsibility**: To present the data available at the DataContext to the end user to allow him to interact with it.
    * **Communication:** View and model view communicate via data binding or change notification events implemented in model view.
    * **Design Tips:** Avoid putting logic on the View even when XAML allows to do it. Prefer moving that logic to the ViewModel over adding it to the View because:
        *   XAML logic cannot be debugged.
        *   XAML logic cannot be tested.
2.  **Model**
    *   **Responsibility:** To model a business object containing the required data.
    * **Communication:** The model can be accessed directly in Model View, and changed in model can be notified to model view via notification events.
    *   **Design Tips:** As the model is only a representation of the data of a business entity (object) it should contain only properties containing object’s data and constructors. 
2.  **ViewModel**
    *   **Responsibility:** To contain the logic that acts as a bridge between the View and the Model.
    * **Communication:** The view model implements properties and commands to which the view can data bind and notifies the view of any state changes through change notification events. The properties and commands that the view model provides define the functionality to be offered by the UI, but the view determines how that functionality is to be rendered.
    *   **Design Tips:** Avoid putting too much logic inside the ViewModel and consider creating more classes (services, engines, etc.) if the ViewModel logic is too big to fit in one class. Include always a reference to the model on the ViewModel.