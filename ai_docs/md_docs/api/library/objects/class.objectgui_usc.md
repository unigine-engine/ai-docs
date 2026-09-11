# ObjectGui Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** Object


This class allows to create a flat [GUI](../../../objects/objects/gui/gui_object.md) object that is positioned in the world and to which different [widgets](../../../api/library/gui/class.widget_usc.md) are assigned to be displayed. Basically, ObjectGui is a flat display to which a player can come to and click some buttons. GUI objects can undergo postprocessing filtering, for example, blurring or any other one.


> **Notice:** When you create an instance of the *ObjectGui* class, it is automatically associated with an instance of the [*Gui*](../../../api/library/gui/class.gui_usc.md) class.


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
## void setMouseShow ( int show )

Sets a new value indicating if the mouse cursor is rendered in the gui object.
### Arguments

- *int* **show** - The value indicating if the mouse cursor is rendered in the gui object

## int isMouseShow () const

Returns the current value indicating if the mouse cursor is rendered in the gui object.
### Return value

Current value indicating if the mouse cursor is rendered in the gui object
## void setDepthTest ( int test )

Sets a new value indicating if the gui object uses depth test.
### Arguments

- *int* **test** - The value indicating if the gui object uses depth test

## int isDepthTest () const

Returns the current value indicating if the gui object uses depth test.
### Return value

Current value indicating if the gui object uses depth test
## void setBackground ( int background )

Sets a new value indicating if gui background (black screen) is rendered.
### Arguments

- *int* **background** - The value indicating if gui background (black screen) is rendered

## int isBackground () const

Returns the current value indicating if gui background (black screen) is rendered.
### Return value

Current value indicating if gui background (black screen) is rendered
## void setBillboard ( int billboard )

Sets a new value indicating if the gui object is a billboard.
### Arguments

- *int* **billboard** - The value indicating if the gui object is a billboard

## int isBillboard () const

Returns the current value indicating if the gui object is a billboard.
### Return value

Current value indicating if the gui object is a billboard
---

## static ObjectGui ( float width , float height , string name = 0 )

Constructor. Creates a new GUI object with given properties.
### Arguments

- *float* **width** - Physical width of the new GUI object in units.
- *float* **height** - Physical height of the new GUI object in units.
- *string* **name** - Path to the folder with GUI skin (the [RC file](../../../code/gui/rc.md) and textures). If no value is specified, the default gui skin will be used.

## Gui getGui ( )

Returns a [Gui](../../../api/library/gui/class.gui_usc.md) instance associated with the object. This function is used when assigning a widget to the GUI object.
> **Notice:** When you create an instance of the *ObjectGui* class, it is automatically associated with a *[Gui](../../../api/library/gui/class.gui_usc.md)* instance.


### Return value

GUI associated with the object.
## void setMouse ( Vec3 p0 , Vec3 p1 , int mouse_button , int mouse_show )

Sets mouse cursor position in the [virtual control mode](#MOUSE_VIRTUAL).
### Arguments

- *Vec3* **p0** - Start point. A line segment between the start and the end points must intersect ObjectGui. The point of intersection determines x and y coordinates on the ObjectGui.
- *Vec3* **p1** - End point. A line segment between the start and the end points must intersect ObjectGui. The point of intersection determines x and y coordinates on the ObjectGui.
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

[Object](../../../api/library/objects/class.object_usc.md) type identifier.
