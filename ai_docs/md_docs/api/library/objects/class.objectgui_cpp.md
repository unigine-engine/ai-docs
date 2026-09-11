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

## int getScreenHeight () const

Returns the current screen height of the gui object.
### Return value

Current screen height of the gui object
## int getScreenWidth () const

Returns the current screen width of the gui object.
### Return value

Current screen width of the gui object
## float getPhysicalHeight () const

Returns the current physical height of the gui object.
### Return value

Current physical height of the gui object
## float getPhysicalWidth () const

Returns the current physical width of the gui object.
### Return value

Current physical width of the gui object
## void setPolygonOffset ( float offset )

Sets a new offset of the gui object above the background to avoid z-fighting. If a negative value is provided, 0 will be used instead.
### Arguments

- *float* **offset** - The offset of the gui object above the background to avoid z-fighting

## float getPolygonOffset () const

Returns the current offset of the gui object above the background to avoid z-fighting. If a negative value is provided, 0 will be used instead.
### Return value

Current offset of the gui object above the background to avoid z-fighting
## void setControlDistance ( float distance )

Sets a new distance at which the gui becomes controllable.
### Arguments

- *float* **distance** - The distance at which the gui becomes controllable

## float getControlDistance () const

Returns the current distance at which the gui becomes controllable.
### Return value

Current distance at which the gui becomes controllable
## void setMouseMode ( int mode )

Sets a new mouse mode. One of the [MOUSE_*](#MOUSE_VIRTUAL) variables.
### Arguments

- *int* **mode** - The mouse mode

## int getMouseMode () const

Returns the current mouse mode. One of the [MOUSE_*](#MOUSE_VIRTUAL) variables.
### Return value

Current mouse mode
## void setMouseShow ( bool show )

Sets a new value indicating if the mouse cursor is rendered in the gui object.
### Arguments

- *bool* **show** - value indicating if the mouse cursor is rendered in the gui object

## bool isMouseShow () const

Returns the current value indicating if the mouse cursor is rendered in the gui object.
### Return value

value indicating if the mouse cursor is rendered in the gui object
## void setDepthTest ( bool test )

Sets a new value indicating if the gui object uses depth test.
### Arguments

- *bool* **test** - value indicating if the gui object uses depth test

## bool isDepthTest () const

Returns the current value indicating if the gui object uses depth test.
### Return value

value indicating if the gui object uses depth test
## void setBackground ( bool background )

Sets a new value indicating if gui background (black screen) is rendered.
### Arguments

- *bool* **background** - value indicating if gui background (black screen) is rendered

## bool isBackground () const

Returns the current value indicating if gui background (black screen) is rendered.
### Return value

value indicating if gui background (black screen) is rendered
## void setBillboard ( bool billboard )

Sets a new value indicating if the gui object is a billboard.
### Arguments

- *bool* **billboard** - value indicating if the gui object is a billboard

## bool isBillboard () const

Returns the current value indicating if the gui object is a billboard.
### Return value

value indicating if the gui object is a billboard
---

## static ObjectGuiPtr create ( float width , float height , const char * name = 0 )

Constructor. Creates a new GUI object with given properties.
### Arguments

- *float* **width** - Physical width of the new GUI object in units.
- *float* **height** - Physical height of the new GUI object in units.
- *const char ** **name** - Path to the folder with GUI skin (the [RC file](../../../code/gui/rc.md) and textures). If no value is specified, the default gui skin will be used.

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

## void setPhysicalSize ( float width , float height )

Sets physical dimensions of the GUI object.
### Arguments

- *float* **width** - New width in units. If a negative value is provided, 0 will be used instead.
- *float* **height** - New height in units. If a negative value is provided, 0 will be used instead.

## void setScreenSize ( int width , int height )

Sets screen dimensions of the GUI object.
### Arguments

- *int* **width** - New width in pixels. If a negative value is provided, 0 will be used instead.
- *int* **height** - New height in pixels. If a negative value is provided, 0 will be used instead.

## static int type ( )

Returns the type of the node.
### Return value

[Object](../../../api/library/objects/class.object_cpp.md) type identifier.
