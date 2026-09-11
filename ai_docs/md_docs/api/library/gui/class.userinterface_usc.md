# Unigine::UserInterface Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


The class is used to work with widgets that are created by loading a UI file.


### Usage Examples


The examples below show:

- Loading a UserInterface from the `*.ui` file and accessing the widgets it stores.
- Adding callbacks to these widgets.
- Managing the UserInterface lifetime.


#### Managing Lifetime by the World


The UserInterface is created on loading the world. When you reload or exit the world, or close the Engine window, the UserInterface is deleted.


#### Managing Lifetime by the Window


The UserInterface is created in a separate window. When you close the window, the UserInterface is deleted as its lifetime is managed by this window. The console shows whether the window and UserInterface are deleted or not, whether the remove event is fired, and the message from the remove event handler (if it is).


After closing, the window can be re-created by pressing **T**.


#### Managing Lifetime by the Engine


The lifetime of the UserInterface is managed by the Engine, so it is deleted on Engine shutdown. A [Gui](../../../api/library/gui/class.gui_usc.md) instance is set manually via the *[setGui()](#setGui_Gui_void)* method.


The console shows whether the window and UserInterface are deleted or not, whether the remove event is fired, and the message from the remove event handler (if it is). After closing, the window can be re-created by pressing **T**.


### See Also


- C++ sample
- C# Component sample


## UserInterface Class

### Members

## int getNumWidgets () const

Returns the current number of associated widgets.
### Return value

Current number of associated widgets
## void setGui ( Gui gui )

Sets a new *[Gui](../../../api/library/gui/class.gui_usc.md)* instance used for the UserInterface.
### Arguments

- *[Gui](../../../api/library/gui/class.gui_usc.md)* **gui** - The Gui instance used for the UserInterface

## Gui getGui () const

Returns the current *[Gui](../../../api/library/gui/class.gui_usc.md)* instance used for the UserInterface.
### Return value

Current Gui instance used for the UserInterface
## void setLifetime ( int lifetime )

Sets a new lifetime management type for the UserInterface. By default, the [LIFETIME_ENGINE](../../../api/library/gui/class.widget_usc.md#LIFETIME) type is used.
> **Notice:** Lifetime of each UserInterface in the hierarchy is defined by its root. Thus, a lifetime management type set for a child UserInterface that differs from the one set for the root is ignored.

### Arguments

- *int* **lifetime** - The lifetime management type for the UserInterface

## int getLifetime () const

Returns the current lifetime management type for the UserInterface. By default, the [LIFETIME_ENGINE](../../../api/library/gui/class.widget_usc.md#LIFETIME) type is used.
> **Notice:** Lifetime of each UserInterface in the hierarchy is defined by its root. Thus, a lifetime management type set for a child UserInterface that differs from the one set for the root is ignored.

### Return value

Current lifetime management type for the UserInterface
---

## int getCallback ( int num , int callback )

Returns the number of a given callback function.
### Arguments

- *int* **num** - Widget number.
- *int* **callback**

### Return value

Callback number.
## string getCallbackInstanceData ( int num )

Returns the callback instance data.
### Arguments

- *int* **num** - Widget number.

### Return value

Instance data.
## string getCallbackName ( int num )

Returns the name of a given callback function.
### Arguments

- *int* **num** - Widget number.

### Return value

Callback function name.
## string getCallbackStringData ( int num )

Returns the callback string data.
### Arguments

- *int* **num** - Widget number.

### Return value

Callback string data (i.e. string data specified in the *string* parameter of the [callback](../../../code/gui/ui/ui_widgets.md#child_callback)).
## string getCallbackVariableData ( int num )

Returns the callback variable data.
### Arguments

- *int* **num** - Widget number.

### Return value

Callback variable data (i.e. string data specified in the *variable* parameter of the [callback](../../../code/gui/ui/ui_widgets.md#child_callback)).
## Widget getCallbackWidgetData ( int num )

Returns the callback widget data.
### Arguments

- *int* **num** - Widget number.

### Return value

Widget data (i.e. reference to a widget specified in the *widget* parameter of the [callback](../../../code/gui/ui/ui_widgets.md#child_callback)).
## int getNumCallbacks ( int num )

Returns the total number of callbacks for a given widget.
### Arguments

- *int* **num** - Widget number.

### Return value

Number of callbacks.
## Widget getWidget ( int num )

Returns a widget with the given ID.
### Arguments

- *int* **num** - Widget ID.

### Return value

Reference to widget with the given ID.
## Widget getWidgetByName ( string name )

Returns a widget with the given name.
### Arguments

- *string* **name** - Widget name.

### Return value

Widget with the given ID.
## int getWidgetExport ( int num )

Returns a value indicating if a given widget is exported into a script (has `export="1"` flag in UI file).
### Arguments

- *int* **num** - Widget ID.

### Return value

**1** if the widget is exported; otherwise, **0**.
## string getWidgetName ( int num )

Returns widget name by ID.
### Arguments

- *int* **num** - Widget ID.

### Return value

Widget name.
## string getWidgetNext ( int num )

Returns the name of the widget, which will be focused next.
### Arguments

- *int* **num** - Widget number.

### Return value

Widget name.
## int findWidget ( string name )

Searches a widget by its name.
### Arguments

- *string* **name** - Widget name.

### Return value

Returns the number of the widget if exists; otherwise, -1.
## void updateWidgets ( )

Updates all widgets belonging to the user interface. This function should be called, for example, after change of the interface language.
