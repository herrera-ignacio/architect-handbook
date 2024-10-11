# Presenter and View

The _View_ is the humble object that is hard to test. The code in this object is kept as simple as posible. It moves data into the GUI but does not process that data.

The _Presenter_ is the testable object. Its job is to accept data from the application and format it for presentation so that the _View_ can simple move it to the screen.

For example, if the application wants a date displayed in a field, it will hand the _Presenter_ a `Date` object. The *Presenter* will then format that data into an appropriate string and place it in a simple data structure called the `ViewModel`, where the *View* can find it.

> Anything and everything that appears on the screen, and that the application has some kind of control over, is represented in the `ViewModel` as a string,m or a boolean, or an enum.

Every button on the screen will have a name. That name will be a string in the `ViewModel`, placed there by the presenter. If those buttons should be grayed out, the Presenter will set an appropriate boolean flag in the `ViewModel`.
