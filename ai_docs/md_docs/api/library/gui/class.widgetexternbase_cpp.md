# Unigine::WidgetExternBase Class (CPP)

**Header:** #include <UnigineWidgets.h>

**Inherits from:** Base


The base class, from which [custom user-defined widgets](../../../api/library/gui/class.widgetextern_cpp.md) are inherited.


### See Also


- C++ sample


## WidgetExternBase Class

---

## template < class Type >

## static addClassID ( int class_id )

Registers the custom widget class with a unique class ID.
```cpp
// register the MyWidget class
WidgetExternBase::addClassID<MyWidget>(1);

```


### Arguments

- *int* **class_id** - Unique class ID.

## int getClassID ( )

Returns a unique class ID.
### Return value

Unique class ID.
## Ptr < Gui > getGui ( ) const

Returns the Gui smart pointer.
### Return value

Gui smart pointer.
## int getKeyActivity ( unsigned int key )

Checks the keyboard key.
### Arguments

- *unsigned int* **key** - Key code.

### Return value

Returns **1** if the key is used by widget.
## Ptr < Widget > getWidget ( ) const

Returns the Widget smart pointer.
### Return value

Widget smart pointer.
## Ptr < WidgetExtern > getWidgetExtern ( ) const

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

## void preRender ( )

Widget pre-render function executed after the *update()* and before the *render()* function. This method is used to make necessary preparations for rendering (e.g. prepare a texture) after the *update()* and is called automatically for *[WidgetSpriteViewport](../../../api/library/gui/class.widgetspriteviewport_cpp.md)* and *[WidgetSpriteNode](../../../api/library/gui/class.widgetspriteviewport_cpp.md)* to ensure proper rendering of the widgets during *render()*. In case you implement a custom GUI or widgets using the *WidgetExtern* class you should put all such rendering preparations to this method and call **[Gui::preRender()](../../../api/library/gui/class.gui_cpp.md#preRender_void)***preRender()* manually after *update()*.
## void render ( )

Renders the widget.
## void updatePositions ( )

Updates the widget's screen coordinates. This function is called after the [arrange()](#arrange_void) and [expand()](#expand_int_int_void) functions.
