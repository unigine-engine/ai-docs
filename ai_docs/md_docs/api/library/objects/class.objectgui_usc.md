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

---

## static ObjectGui ( float width , float height , string name = 0 )

Constructor. Creates a new GUI object with given properties.
### Arguments

- *float* **width** - Physical width of the new GUI object in units.
- *float* **height** - Physical height of the new GUI object in units.
- *string* **name** - Path to the folder with GUI skin (the [RC file](../../../code/gui/rc.md) and textures). If no value is specified, the default gui skin will be used.

## void setBackground ( int background )

Sets a value indicating if the GUI background (black screen) should be rendered.
### Arguments

- *int* **background** - **1** to render GUI background, **0** to keep it transparent.

## int isBackground ( )

Returns a value indicating if GUI background (black screen) is rendered.
### Return value

**1** if background is rendered; otherwise, **0**.
## void setBillboard ( int billboard )

Sets a value indicating if the GUI object should be a billboard.
### Arguments

- *int* **billboard** - **1** to render the GUI object as a billboard; otherwise, **0**.

## int isBillboard ( )

Returns a value indicating if the GUI object is a billboard.
### Return value

**1** if GUI object is a billboard; otherwise, **0**.
## void setControlDistance ( float distance )

Sets a distance at which the GUI becomes controllable.
### Arguments

- *float* **distance** - New distance in units. If a negative value is provided, 0 will be used instead.

## float getControlDistance ( )

Returns the distance, at which the GUI becomes controllable.
### Return value

Distance in units.
## void setDepthTest ( int test )

Sets a value indicating if depth test should be used for the GUI object.
### Arguments

- *int* **test** - **1** to use depth test; otherwise, **0**.

## int isDepthTest ( )

Returns a value indicating if the GUI object uses depth test.
### Return value

**1** if the GUI object uses depth test; otherwise, **0**.
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

## void setMouseMode ( int mode )

Sets mouse mode. This method can be used to set a [virtual control mode](#MOUSE_VIRTUAL) for the mouse.
### Arguments

- *int* **mode** - Mouse mode. One of the [MOUSE_*](#MOUSE_VIRTUAL) variables.

## int getMouseMode ( )

Returns the current mouse mode.
### Return value

Mouse mode. One of the [MOUSE_*](#MOUSE_VIRTUAL) variables.
## void setMouseShow ( int show )

Sets a value indicating if the mouse cursor should be rendered in the GUI object.
### Arguments

- *int* **show** - **1** to render the mouse cursor; otherwise, **0**.

## int isMouseShow ( )

Returns a value indicating if the mouse cursor is rendered in the GUI object.
### Return value

**1** if the cursor is rendered; otherwise, **0**.
## float getPhysicalHeight ( )

Returns the physical height of the GUI object.
### Return value

Height in units.
## void setPhysicalSize ( float width , float height )

Sets physical dimensions of the GUI object.
### Arguments

- *float* **width** - New width in units. If a negative value is provided, 0 will be used instead.
- *float* **height** - New height in units. If a negative value is provided, 0 will be used instead.

## float getPhysicalWidth ( )

Returns the physical width of the GUI object.
### Return value

Width in units.
## void setPolygonOffset ( float offset )

Sets an offset of the GUI object above the background to avoid z-fighting.
### Arguments

- *float* **offset** - Polygon offset in units. If a negative value is provided, 0 will be used instead.

## float getPolygonOffset ( )

Returns an offset of the GUI object above the background to avoid z-fighting.
### Return value

Polygon offset in units.
## int getScreenHeight ( )

Returns the screen height of the GUI object.
### Return value

Height in pixels.
## void setScreenSize ( int width , int height )

Sets screen dimensions of the GUI object.
### Arguments

- *int* **width** - New width in pixels. If a negative value is provided, 0 will be used instead.
- *int* **height** - New height in pixels. If a negative value is provided, 0 will be used instead.

## int getScreenWidth ( )

Returns the screen width of the GUI object.
### Return value

Width in pixels.
## static int type ( )

Returns the type of the node.
### Return value

[Object](../../../api/library/objects/class.object_usc.md) type identifier.
