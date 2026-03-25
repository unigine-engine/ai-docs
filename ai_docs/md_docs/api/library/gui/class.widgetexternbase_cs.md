# Unigine::WidgetExternBase Class (CS)

**Inherits from:** Base


The base class, from which [custom user-defined widgets](../../../api/library/gui/class.widgetextern_cs.md) are inherited.


### See Also


- C++ sample


## WidgetExternBase Class

### Members

---

## int GetClassID ( )

Returns a unique class ID.
### Return value

Unique class ID.
## Gui GetGui ( )

Returns the Gui smart pointer.
### Return value

Gui smart pointer.
## int GetKeyActivity ( uint key )

Checks the keyboard key.
### Arguments

- *uint* **key** - Key code.

### Return value

Returns **1** if the key is used by widget.
## Widget GetWidget ( )

Returns the Widget smart pointer.
### Return value

Widget smart pointer.
## WidgetExtern GetWidgetExtern ( )

Returns the WidgetExtern smart pointer.
### Return value

WidgetExtern smart pointer.
## void Arrange ( )

Calculates the widget size.
## void CheckCallbacks ( int x , int y )

Checks widget callbacks.
### Arguments

- *int* **x** - Mouse X coordinate.
- *int* **y** - Mouse Y coordinate.

## void Destroy ( )

Destroys the widget resources.
## void Expand ( int width , int height )

Expands the widget size.
### Arguments

- *int* **width** - Maximum available width.
- *int* **height** - Maximum available height.

## void KeyPress ( uint key )

Keyboard press event (scan code).
### Arguments

- *uint* **key** - Key code.

## void TextPress ( uint unicode )

Keyboard press event (virtual key).
### Arguments

- *uint* **unicode** - Virtual key code.

## void Update ( float ifps )

Widget update function.
### Arguments

- *float* **ifps** - Inverse FPS value.

## void PreRender ( )

Widget pre-render function executed after the *update()* and before the *render()* function. This method is used to make necessary preparations for rendering (e.g. prepare a texture) after the *update()* and is called automatically for *[WidgetSpriteViewport](../../../api/library/gui/class.widgetspriteviewport_cs.md)* and *[WidgetSpriteNode](../../../api/library/gui/class.widgetspriteviewport_cs.md)* to ensure proper rendering of the widgets during *render()*. In case you implement a custom GUI or widgets using the *WidgetExtern* class you should put all such rendering preparations to this method and call **[Gui.PreRender()](../../../api/library/gui/class.gui_cs.md#preRender_void)***preRender()* manually after *update()*.
## void Render ( )

Renders the widget.
## void UpdatePositions ( )

Updates the widget's screen coordinates. This function is called after the [arrange()](#arrange_void) and [expand()](#expand_int_int_void) functions.
