# ObjectGui Class (CS)

**Inherits from:** Object


This class allows to create a flat [GUI](../../../objects/objects/gui/gui_object.md) object that is positioned in the world and to which different [widgets](../../../api/library/gui/class.widget_cs.md) are assigned to be displayed. Basically, ObjectGui is a flat display to which a player can come to and click some buttons. GUI objects can undergo postprocessing filtering, for example, blurring or any other one.


> **Notice:** When you create an instance of the *ObjectGui* class, it is automatically associated with an instance of the [*Gui*](../../../api/library/gui/class.gui_cs.md) class.


### See Also


UnigineScript samples:


-
-
-
-
-
-


## ObjectGui Class

### Properties

## 🔒︎ int ScreenHeight

The screen height of the gui object.
## 🔒︎ int ScreenWidth

The screen width of the gui object.
## 🔒︎ float PhysicalHeight

The physical height of the gui object.
## 🔒︎ float PhysicalWidth

The physical width of the gui object.
## float PolygonOffset

The offset of the gui object above the background to avoid z-fighting. If a negative value is provided, 0 will be used instead.
## float ControlDistance

The distance at which the gui becomes controllable.
## int MouseMode

The mouse mode. One of the [MOUSE_*](#MOUSE_VIRTUAL) variables.
## bool MouseShow

The value indicating if the mouse cursor is rendered in the gui object.
## bool DepthTest

The value indicating if the gui object uses depth test.
## bool Background

The value indicating if gui background (black screen) is rendered.
## bool Billboard

The value indicating if the gui object is a billboard.
### Members

---

## ObjectGui ( float width , float height , string name = 0 )

Constructor. Creates a new GUI object with given properties.
### Arguments

- *float* **width** - Physical width of the new GUI object in units.
- *float* **height** - Physical height of the new GUI object in units.
- *string* **name** - Path to the folder with GUI skin (the [RC file](../../../code/gui/rc.md) and textures). If no value is specified, the default gui skin will be used.

## Gui GetGui ( )

Returns a [Gui](../../../api/library/gui/class.gui_cs.md) instance associated with the object. This function is used when assigning a widget to the GUI object.
> **Notice:** When you create an instance of the *ObjectGui* class, it is automatically associated with a *[Gui](../../../api/library/gui/class.gui_cs.md)* instance.


### Return value

Gui smart pointer.
## void SetMouse ( vec3 p0 , vec3 p1 , int mouse_button , int mouse_show )

Sets mouse cursor position in the [virtual control mode](#MOUSE_VIRTUAL).
### Arguments

- *vec3* **p0** - Start point. A line segment between the start and the end points must intersect ObjectGui. The point of intersection determines x and y coordinates on the ObjectGui.
- *vec3* **p1** - End point. A line segment between the start and the end points must intersect ObjectGui. The point of intersection determines x and y coordinates on the ObjectGui.
- *int* **mouse_button** - Mouse button status. Set 1 to indicate that the button is clicked; otherwise, 0.
- *int* **mouse_show** - Mouse cursor status. Set 1 to show mouse cursor; otherwise, 0.

## void SetPhysicalSize ( float width , float height )

Sets physical dimensions of the GUI object.
### Arguments

- *float* **width** - New width in units. If a negative value is provided, 0 will be used instead.
- *float* **height** - New height in units. If a negative value is provided, 0 will be used instead.

## void SetScreenSize ( int width , int height )

Sets screen dimensions of the GUI object.
### Arguments

- *int* **width** - New width in pixels. If a negative value is provided, 0 will be used instead.
- *int* **height** - New height in pixels. If a negative value is provided, 0 will be used instead.

## static int type ( )

Returns the type of the node.
### Return value

[Object](../../../api/library/objects/class.object_cs.md) type identifier.
