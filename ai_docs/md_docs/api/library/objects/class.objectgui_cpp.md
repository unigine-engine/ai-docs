# ObjectGui Class (CPP)

**Header:** #include <UnigineObjects.h>

**Inherits from:** Object


This class allows to create a flat [GUI](../../../objects/objects/gui/gui_object.md) object that is positioned in the world and to which different [widgets](../../../api/library/gui/class.widget_cpp.md) are assigned to be displayed. Basically, ObjectGui is a flat display to which a player can come to and click some buttons. GUI objects can undergo postprocessing filtering, for example, blurring or any other one.


> **Notice:** When you create an instance of the *ObjectGui* class, it is automatically associated with an instance of the [*Gui*](../../../api/library/gui/class.gui_cpp.md) class.


### See Also


UnigineScript samples:


-
-
-
-
-
-


## ObjectGui Class

### Members

---

## static ObjectGuiPtr create ( float width , float height , const char * name = 0 )

Constructor. Creates a new GUI object with given properties.
### Arguments

- *float* **width** - Physical width of the new GUI object in units.
- *float* **height** - Physical height of the new GUI object in units.
- *const char ** **name** - Path to the folder with GUI skin (the [RC file](../../../code/gui/rc.md) and textures). If no value is specified, the default gui skin will be used.

## void setBackground ( bool background )

Sets a value indicating if the GUI background (black screen) should be rendered.
### Arguments

- *bool* **background** - true to render GUI background, false to keep it transparent.

## bool isBackground ( ) const

Returns a value indicating if GUI background (black screen) is rendered.
### Return value

true if background is rendered; otherwise, false.
## void setBillboard ( bool billboard )

Sets a value indicating if the GUI object should be a billboard.
### Arguments

- *bool* **billboard** - true to render the GUI object as a billboard; otherwise, false.

## bool isBillboard ( ) const

Returns a value indicating if the GUI object is a billboard.
### Return value

**true** if GUI object is a billboard; otherwise, **false**.
## void setControlDistance ( float distance )

Sets a distance at which the GUI becomes controllable.
### Arguments

- *float* **distance** - New distance in units. If a negative value is provided, 0 will be used instead.

## float getControlDistance ( ) const

Returns the distance, at which the GUI becomes controllable.
### Return value

Distance in units.
## void setDepthTest ( bool test )

Sets a value indicating if depth test should be used for the GUI object.
### Arguments

- *bool* **test** - true to use depth test; otherwise, false.

## bool isDepthTest ( ) const

Returns a value indicating if the GUI object uses depth test.
### Return value

true if the GUI object uses depth test; otherwise, false.
## Ptr < Gui > getGui ( ) const

Returns a [Gui](../../../api/library/gui/class.gui_cpp.md) instance associated with the object. This function is used when assigning a widget to the GUI object.
> **Notice:** When you create an instance of the *ObjectGui* class, it is automatically associated with a *[Gui](../../../api/library/gui/class.gui_cpp.md)* instance.


### Return value

Gui smart pointer.
## void setMouse ( const Math:: Vec3 & p0 , const Math:: Vec3 & p1 , int mouse_button , int mouse_show )

Sets mouse cursor position in the [virtual control mode](#MOUSE_VIRTUAL).
### Arguments

- *const  Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) &* **p0** - Start point. A line segment between the start and the end points must intersect ObjectGui. The point of intersection determines x and y coordinates on the ObjectGui.
- *const  Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) &* **p1** - End point. A line segment between the start and the end points must intersect ObjectGui. The point of intersection determines x and y coordinates on the ObjectGui.
- *int* **mouse_button** - Mouse button status. Set 1 to indicate that the button is clicked; otherwise, 0.
- *int* **mouse_show** - Mouse cursor status. Set 1 to show mouse cursor; otherwise, 0.

## void setMouseMode ( int mode )

Sets mouse mode. This method can be used to set a [virtual control mode](#MOUSE_VIRTUAL) for the mouse.
### Arguments

- *int* **mode** - Mouse mode. One of the [MOUSE_*](#MOUSE_VIRTUAL) variables.

## int getMouseMode ( ) const

Returns the current mouse mode.
### Return value

Mouse mode. One of the [MOUSE_*](#MOUSE_VIRTUAL) variables.
## void setMouseShow ( bool show )

Sets a value indicating if the mouse cursor should be rendered in the GUI object.
### Arguments

- *bool* **show** - true to render the mouse cursor; otherwise, false.

## bool isMouseShow ( ) const

Returns a value indicating if the mouse cursor is rendered in the GUI object.
### Return value

true if the cursor is rendered; otherwise, false.
## float getPhysicalHeight ( ) const

Returns the physical height of the GUI object.
### Return value

Height in units.
## void setPhysicalSize ( float width , float height )

Sets physical dimensions of the GUI object.
### Arguments

- *float* **width** - New width in units. If a negative value is provided, 0 will be used instead.
- *float* **height** - New height in units. If a negative value is provided, 0 will be used instead.

## float getPhysicalWidth ( ) const

Returns the physical width of the GUI object.
### Return value

Width in units.
## void setPolygonOffset ( float offset )

Sets an offset of the GUI object above the background to avoid z-fighting.
### Arguments

- *float* **offset** - Polygon offset in units. If a negative value is provided, 0 will be used instead.

## float getPolygonOffset ( ) const

Returns an offset of the GUI object above the background to avoid z-fighting.
### Return value

Polygon offset in units.
## int getScreenHeight ( ) const

Returns the screen height of the GUI object.
### Return value

Height in pixels.
## void setScreenSize ( int width , int height )

Sets screen dimensions of the GUI object.
### Arguments

- *int* **width** - New width in pixels. If a negative value is provided, 0 will be used instead.
- *int* **height** - New height in pixels. If a negative value is provided, 0 will be used instead.

## int getScreenWidth ( ) const

Returns the screen width of the GUI object.
### Return value

Width in pixels.
## static int type ( )

Returns the type of the node.
### Return value

[Object](../../../api/library/objects/class.object_cpp.md) type identifier.
