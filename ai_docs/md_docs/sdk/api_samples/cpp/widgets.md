# User Interface

> **Notice:** The complete sample source code is available on GitHub:
> **[github.com/unigine-engine/cpp-api-samples](https://github.com/unigine-engine/cpp-api-samples)**.


Samples in this section illustrate the use of the [GUI-Related](../../../api/library/gui/index.md) classes.


## Object Frame

This sample shows how to dynamically create and display rectangular frames around objects in the scene using the *[WidgetCanvas](../../../api/library/gui/class.widgetcanvas_cpp.md)*. These frames include object labels and appear only if the object is visible and is located within a certain distance from the camera.


You can also take screenshots via the *Snap Screenshot* button. The captured image does not include the rendered frames, but all frame metadata (including object *ID*, name, transform, and screen coordinates of the frame) is saved to a separate *JSON* file. The screenshot and frame metadata are saved in the sample content folder.


The bounding box of each object is computed recursively based on all its mesh components. The resulting rectangle is projected onto the screen space and checked for visibility. If visible and not occluded, a *2D* frame is drawn using *[WidgetCanvas](../../../api/library/gui/class.widgetcanvas_cpp.md)* class.


All metadata, such as object *ID*, name, world-space position and rotation, as well as screen-space rectangle coordinates, is collected and saved as a structured *JSON* document using the *[Json](../../../api/library/common/class.json_cpp.md) class*.


This approach is useful for creating visual overlays, annotations, or *UI* debug elements where object-specific data must be highlighted or preserved externally.


**SDK Path:***<SAMPLES_PROJECT_PATH>/source/user_interface/object_frame*
## Object Text

This sample demonstrates how to create and control text objects in the scene via API, using the *[ObjectText](../../../api/library/objects/class.objecttext_cpp.md)* class.


It showcases different text rendering features, including adjustable font parameters, color animation, and support for rich text formatting:


**Left object** - a static *rich text* block with varying colors, font sizes, and outlines.


**Center object** - a user-editable text that can be customized through the Parameters window. It supports adjustments for wrap width, depth test, outline, vertical and horizontal spacing, font resolution, size, and rich text mode.


**Right object** - a dynamic text object that continuously updates its color over time, displaying its current RGBA values in real time.


**SDK Path:***<SAMPLES_PROJECT_PATH>/source/user_interface/object_text*
## Target Marker

This sample demostrates how to implement a marker that always highlights the target when it is within the field of view, or displays an arrow pointing the direction to the target when it is out of sight (aligned with the screen borders).
**SDK Path:***<SAMPLES_PROJECT_PATH>/source/user_interface/target_marker*

## User Interface

This sample shows how to generate a User Interface from a description stored in a **.ui** file (*XML* format) via C++ API. The sample also demonstrates how to get a UI widget by name via *[getWidgetByName()](../../../api/library/gui/class.userinterface_cpp.md#getWidgetByName_cstr_Widget)* and subscribe to events to implement custom handling for user actions (particularly selecting *File -> Reload* from the main menu or entering text in the text field on the **EditText** tab).
**SDK Path:***<SAMPLES_PROJECT_PATH>/source/user_interface/user_interface*

## Widgets

This sample demonstrates the implementation of various UI widgets in UNIGINE. It showcases how to create, configure and manage interactive **[GUI](../../../objects/objects/gui/index.md)** elements.


The sample includes multiple widget types with event handling capabilities, demonstrating how to create and position widgets, configure visual properties, handle user interactions, etc., such as **sliders, scrolls, buttons, checkboxes, drop-down lists, etc**.


**SDK Path:***<SAMPLES_PROJECT_PATH>/source/user_interface/widgets*
## Widget Canvas

This sample demonstrates how to use the *[WidgetCanvas](../../../api/library/gui/class.widgetcanvas_cpp.md)* class to draw vector-based shapes and text. The canvas supports adding lines, polygons, and text by defining their geometry through vertex positions. Elements are layered by draw order and colored individually.


The canvas content remains sharp regardless of scaling or rotation. In this example, the entire canvas is transformed over time, rotating and moving in 3D space while preserving the clarity of its contents. The geometry is built using helper functions that generate radial lines and regular polygons, and the layout is updated every frame using a transformation matrix.


This can be used to create clean, scalable UI elements, procedural charts, custom overlays, or dynamic data visualizations in tools or applications.


**SDK Path:***<SAMPLES_PROJECT_PATH>/source/user_interface/widget_canvas*
## Widget Dialogs

This sample demonstrates how to create and manage a GUI dialog system using UNIGINE's dialog widgets via the C++ API. A *[WidgetWindow](../../../api/library/gui/class.widgetwindow_cpp.md)* instance contains several buttons, each opening a different type of dialog: *[WidgetDialogMessage](../../../api/library/gui/class.widgetdialogmessage_cpp.md)*, *[WidgetDialogFile](../../../api/library/gui/class.widgetdialogfile_cpp.md)*, *[WidgetDialogColor](../../../api/library/gui/class.widgetdialogcolor_cpp.md)*, or *[WidgetDialogImage](../../../api/library/gui/class.widgetdialogimage_cpp.md)*.


Each button is connected to an event handler that creates and configures the corresponding dialog widget. Dialogs are shown centered on screen and support user interaction through *OK* and *Cancel* buttons. A shared handler manages these responses, logs actions to the console, and deletes the dialog afterward to clean up resources.


This approach can be used to build simple and interactive GUI tools, settings panels, or development utilities that require built-in dialog interactions.


**SDK Path:***<SAMPLES_PROJECT_PATH>/source/user_interface/widget_dialogs*
## Widget Extern

This sample demonstrates how to create a custom GUI widget by inheriting from *[WidgetExternBase](../../../api/library/gui/class.widgetexternbase_cpp.md)* via the C++ API. The custom class overrides key methods like *[render()](../../../api/library/gui/class.widgetexternbase_cpp.md#render_void)*, *[arrange()](../../../api/library/gui/class.widgetexternbase_cpp.md#arrange_void)*, and *[checkCallbacks()](../../../api/library/gui/class.widgetexternbase_cpp.md#checkCallbacks_int_int_void)* to implement unique visual and interactive behavior.


The widget is registered with a unique class ID using *[WidgetExternBase::addClassID()](../../../api/library/gui/class.widgetexternbase_cpp.md#addClassID_int_void)*, and can then be instantiated using *[WidgetExtern::create()](../../../api/library/gui/class.widgetextern_cpp.md#WidgetExtern_int)*.


This setup allows full control over widget rendering and logic directly in C++.


**SDK Path:***<SAMPLES_PROJECT_PATH>/source/user_interface/widget_extern*
## Widget Manipulators

This sample demonstrates the use of manipulators. You can lock axes for transformations, and apply transformation in local or world coordinates.
**SDK Path:***<SAMPLES_PROJECT_PATH>/source/user_interface/widget_manipulators*

## Widget Window

This sample demonstrates how to create a basic *[WidgetWindow](../../../api/library/gui/class.widgetwindow_cpp.md)* using the C++ API and handle user interactions (edit line and button press events) through handler function connections.


The window includes a *[WidgetEditLine](../../../api/library/gui/class.widgeteditline_cpp.md)* and a *[WidgetButton](../../../api/library/gui/class.widgetbutton_cpp.md)*. The *WidgetEditLine* listens for text changes via *[Widget::getEventChanged()](../../../api/library/gui/class.widget_cpp.md#getEventChanged_Event)* and logs the new input, while the WidgetButton uses *[Widget::getEventClicked()](../../../api/library/gui/class.widget_cpp.md#getEventClicked_Event)* to trigger an action when pressed. Font sizes are adjusted for better readability, and the layout is arranged automatically.


This approach is suitable for building interactive UI elements directly within UNIGINE's native GUI system.


**SDK Path:***<SAMPLES_PROJECT_PATH>/source/user_interface/widget_window*
