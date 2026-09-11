# Unigine::WidgetExternBase Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** Base


The base class, from which [custom user-defined widgets](../../../api/library/gui/class.widgetextern_usc.md) are inherited.


### See Also


- C++ sample


## WidgetExternBase Class

---

## int getClassID ( )

Returns a unique class ID.
### Return value

Unique class ID.
## Gui getGui ( )

Returns the Gui smart pointer.
### Return value

Gui smart pointer.
## int getKeyActivity ( unsigned int key )

Checks the keyboard key.
### Arguments

- *unsigned int* **key** - Key code.

### Return value

Returns **1** if the key is used by widget.
## Widget getWidget ( )

Returns the Widget smart pointer.
### Return value

Widget smart pointer.
## WidgetExtern getWidgetExtern ( )

Returns the WidgetExtern smart pointer.
### Return value

WidgetExtern smart pointer.
## void arrange ( )

Calculates the widget size.
## void checkCallbacks ( int x , int y )

Checks widget callbacks.
### Arguments

- *int* **x** - Mouse X coordinate.
- *int* **y** - Mouse Y coordinate.

## void destroy ( )

Destroys the widget resources.
## void expand ( int width , int height )

Expands the widget size.
### Arguments

- *int* **width** - Maximum available width.
- *int* **height** - Maximum available height.

## void keyPress ( unsigned int key )

Keyboard press event (scan code).
### Arguments

- *unsigned int* **key** - Key code.

## void textPress ( unsigned int unicode )

Keyboard press event (virtual key).
### Arguments

- *unsigned int* **unicode** - Virtual key code.

## void update ( float ifps )

Widget update function.
### Arguments

- *float* **ifps** - Inverse FPS value.

## void render ( )

Renders the widget.
## void updatePositions ( )

Updates the widget's screen coordinates. This function is called after the [arrange()](#arrange_void) and [expand()](#expand_int_int_void) functions.
