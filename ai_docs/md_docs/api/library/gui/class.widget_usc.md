# Unigine::Widget Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


This base class is used to create [graphical user interface](../../../objects/objects/gui/index.md) widgets of different types. The Widget class doesn't provide creating of a widget: you can create the required widget by using a constructor of the corresponding class inherited from the Widget class.


Widgets can be used separately or form a hierarchy.


### Working with Widgets


The example below demonstrates how to create a single widget, a hierarchy of widgets, and subscribe for a widget's event.


#### Lifetime of Widgets


By default each new widget's lifetime matches the lifetime of the **[Engine](#LIFETIME_ENGINE)** (i.e. the widget shall be deleted on Engine shutdown). But you can choose widget's lifetime to be managed:

- By a separate **[window](#LIFETIME_WINDOW)** � in this case the widget is deleted automatically on deleting the window.
- By the **[world](#LIFETIME_WORLD)** � in this case the widget is deleted when the world is closed.
- **[Manually](#LIFETIME_MANUAL)** � in this case the widget should be deleted manually.


The examples below show how the different lifetime management types work.


##### Managing Lifetime by the World


In this example, the widgets appear on loading the world. When you reload or exit the world, or close the Engine window, the widgets are deleted as their lifetime is managed by the *world*. The corresponding messages will be shown in the console.


##### Managing Lifetime by the Window


In this example, widgets appear in a separate window. When you close the window, the widgets are deleted as their lifetime is managed by this *window*. The console shows the following information:

- Whether the window, button and hbox hierarchy are deleted or not.
- Whether the remove callbacks are fired or not.
- Messages from the remove callbacks.


After closing, the window can be re-created by pressing **T**.


##### Managing Lifetime by the Engine


Widgets are created on Engine initialization, and then added to a separate window. The console shows the following information:


- Whether the window, button and hbox hierarchy are deleted or not.
- Whether the remove callbacks are fired or not.
- Messages from the remove callbacks.


If you close the window, it will be deleted and the information in the console will change. All the other widgets are deleted only on Engine shutdown, as their lifetime is managed by the Engine.


If the separate window is closed, press **T** to re-create it.


### See Also


- C++ sample
- C# Component sample
- A set of [UnigineScript samples](../../../code/uniginescript/samples/widgets.md) located in the `<UnigineSDK>/data/samples/widgets/` folder


## Widget Class

### Members

## int getNumChildren () const

Returns the current
### Return value

Current number of child widgets.
## void setFontWrap ( int wrap )

Sets a new value indicating if text wrapping to widget width is enabled.
### Arguments

- *int* **wrap** - The value of 1 for text wrapping; otherwise, 0.

## int getFontWrap () const

Returns the current value indicating if text wrapping to widget width is enabled.
### Return value

Current value of 1 for text wrapping; otherwise, 0.
## void setFontRich ( int rich )

Sets a new value indicating if rich text formatting is used.
### Arguments

- *int* **rich** - The value of 1 for rich text formatting; otherwise, 0.

## int getFontRich () const

Returns the current value indicating if rich text formatting is used.
### Return value

Current value of 1 for rich text formatting; otherwise, 0.
## void setFontOutline ( int outline )

Sets a new value indicating if widget text is rendered casting a shadow. Positive or negative values determine the distance in pixels used to offset the font outline.
### Arguments

- *int* **outline** - The positive value if outline is offset in the bottom-right corner direction, negative value if outline is offset in the top-left corner direction. 0 if font is not outlined.

## int getFontOutline () const

Returns the current value indicating if widget text is rendered casting a shadow. Positive or negative values determine the distance in pixels used to offset the font outline.
### Return value

Current positive value if outline is offset in the bottom-right corner direction, negative value if outline is offset in the top-left corner direction. 0 if font is not outlined.
## void setFontVOffset ( int voffset )

Sets a new
### Arguments

- *int* **voffset** - The vertical offset value, in pixels.

## int getFontVOffset () const

Returns the current
### Return value

Current vertical offset value, in pixels.
## void setFontHOffset ( int hoffset )

Sets a new
### Arguments

- *int* **hoffset** - The horizontal offset value, in pixels.

## int getFontHOffset () const

Returns the current
### Return value

Current horizontal offset value, in pixels.
## void setFontVSpacing ( int vspacing )

Sets a new spacing (in pixels) between widget text lines.
### Arguments

- *int* **vspacing** - The vertical spacing value, in pixels.

## int getFontVSpacing () const

Returns the current spacing (in pixels) between widget text lines.
### Return value

Current vertical spacing value, in pixels.
## void setFontHSpacing ( int hspacing )

Sets a new
### Arguments

- *int* **hspacing** - The horizontal spacing value, in pixels.

## int getFontHSpacing () const

Returns the current
### Return value

Current horizontal spacing value, in pixels.
## void setFontPermanent ( int permanent )

Sets a new
### Arguments

- *int* **permanent** - The value of 1 to keep the text color unchanged; 0 to change it.

## int getFontPermanent () const

Returns the current
### Return value

Current value of 1 to keep the text color unchanged; 0 to change it.
## void setFontColor ( vec4 color )

Sets a new color of the font used by the widget.
### Arguments

- *vec4* **color** - The font color.

## vec4 getFontColor () const

Returns the current color of the font used by the widget.
### Return value

Current font color.
## void setFontSize ( int size )

Sets a new size of the font used by the widget.
### Arguments

- *int* **size** - The Font size in pixels.

## int getFontSize () const

Returns the current size of the font used by the widget.
### Return value

Current Font size in pixels.
## void setMouseCursor ( int cursor )

Sets a new mouse pointer set for the widget.
### Arguments

- *int* **cursor** - The mouse pointer, one of the [*CURSOR_**](../../../api/library/gui/class.gui_usc.md) pre-defined variables.

## int getMouseCursor () const

Returns the current mouse pointer set for the widget.
### Return value

Current mouse pointer, one of the [*CURSOR_**](../../../api/library/gui/class.gui_usc.md) pre-defined variables.
## int getMouseY () const

Returns the current Y coordinate of the mouse pointer position in the widget's local space.
### Return value

Current Y coordinate of the mouse pointer position in the widget's local space.
## int getMouseX () const

Returns the current X coordinate of the mouse pointer position in the widget's local space.
### Return value

Current X coordinate of the mouse pointer position in the widget's local space.
## void setHeight ( int height )

Sets a new
### Arguments

- *int* **height** - The widget minimal height, in [logical units](../../../principles/dpi/index.md). If a negative value is provided, the value of 0 will be used instead.

## int getHeight () const

Returns the current
### Return value

Current widget minimal height, in [logical units](../../../principles/dpi/index.md). If a negative value is provided, the value of 0 will be used instead.
## void setWidth ( int width )

Sets a new
### Arguments

- *int* **width** - The widget minimal width, in [logical units](../../../principles/dpi/index.md). If a negative value is provided, the value of 0 will be used instead.

## int getWidth () const

Returns the current
### Return value

Current widget minimal width, in [logical units](../../../principles/dpi/index.md). If a negative value is provided, the value of 0 will be used instead.
## int getScreenPositionY () const

Returns the current screen position of the widget (its top left corner) on the screen along the y axis.
### Return value

Current screen position along the Y axis in [logical units](../../../principles/dpi/index.md).
## int getScreenPositionX () const

Returns the current screen position of the widget (its top left corner) on the screen along the x axis.
### Return value

Current screen position along the X axis in [logical units](../../../principles/dpi/index.md).
## void setPositionY ( int y )

Sets a new Y coordinate of the widget position relative to its parent.
### Arguments

- *int* **y** - The Y coordinate of the widget position relative to its parent.

## int getPositionY () const

Returns the current Y coordinate of the widget position relative to its parent.
### Return value

Current Y coordinate of the widget position relative to its parent.
## void setPositionX ( int x )

Sets a new X coordinate of the widget position relative to its parent.
### Arguments

- *int* **x** - The X coordinate of the widget position relative to its parent.

## int getPositionX () const

Returns the current X coordinate of the widget position relative to its parent.
### Return value

Current X coordinate of the widget position relative to its parent.
## void setNextFocus ( Widget focus )

Sets a new widget which will be focused next if the user presses **TAB**.
### Arguments

- *[Widget](../../../api/library/gui/class.widget_usc.md)* **focus** - The widget which will be focused next if the user presses **TAB**.

## Widget getNextFocus () const

Returns the current widget which will be focused next if the user presses **TAB**.
### Return value

Current widget which will be focused next if the user presses **TAB**.
## void setData ( string data )

Sets a new
### Arguments

- *string* **data** - The

## const char * getData () const

Returns the current
### Return value

Current
## void setOrder ( int order )

Sets a new
### Arguments

- *int* **order** - The rendering order (z-order) for the widget, in the range **[-128;127]**. (126 for the Profiler, 127 for the Console).

## int getOrder () const

Returns the current
### Return value

Current rendering order (z-order) for the widget, in the range **[-128;127]**. (126 for the Profiler, 127 for the Console).
## void setHidden ( int hidden )

Sets a new value indicating if the widget is hidden.
### Arguments

- *int* **hidden** - The true if the widget is hidden, false if it is shown

## int isHidden () const

Returns the current value indicating if the widget is hidden.
### Return value

Current true if the widget is hidden, false if it is shown
## void setEnabled ( int enabled )

Sets a new value indicating if the widget is enabled (the user can interact with the widget).
### Arguments

- *int* **enabled** - The interaction with the widget

## int isEnabled () const

Returns the current value indicating if the widget is enabled (the user can interact with the widget).
### Return value

Current interaction with the widget
## void setIntersectionEnabled ( int enabled )

Sets a new value indicating if intersection detection is enabled for the widget.
### Arguments

- *int* **enabled** - The intersection detection for the widget

## int isIntersectionEnabled () const

Returns the current value indicating if intersection detection is enabled for the widget.
### Return value

Current intersection detection for the widget
## void setFlags ( int flags )

Sets a new
### Arguments

- *int* **flags** - The widget flags, [*ALIGN_**](../../../api/library/gui/class.gui_usc.md#ALIGN_BACKGROUND) pre-defined variables.

## int getFlags () const

Returns the current
### Return value

Current widget flags, [*ALIGN_**](../../../api/library/gui/class.gui_usc.md#ALIGN_BACKGROUND) pre-defined variables.
## void setParent ( Widget parent )

Sets a new
### Arguments

- *[Widget](../../../api/library/gui/class.widget_usc.md)* **parent** - The parent widget.

## Widget getParent () const

Returns the current
### Return value

Current parent widget.
## Gui getParentGui () const

Returns the current [Gui](../../../api/library/gui/class.gui_usc.md) instance that currently renders the widget's parent, if the widget has a parent. (This function can be used if the widget is created and used in two different GUIs, for example, in case of the Interface plugin.)
### Return value

Current GUI instance used for the widget's parent.
## Gui getGui () const

Returns the current
### Return value

Current GUI instance used for the widget.
## const char * getTypeName () const

Returns the current
### Return value

Current name of the widget type.
## getType () const

Returns the current
### Return value

Current type of the widget.
## bool isLayout () const

Returns the current value indicating if the widget is a layout.
### Return value

**true** if the widget is a layout; otherwise **false**.
## bool isFixed () const

Returns the current value indicating if the widget is fixed.
### Return value

**true** if the widget is fixed; otherwise **false**.
## bool isBackground () const

Returns the current value indicating if the widget is a background one.
### Return value

**true** if the widget is a background one; otherwise **false**.
## bool isOverlapped () const

Returns the current value indicating if the widget is overlapped.
### Return value

**true** if the widget is overlapped; otherwise **false**.
## bool isExpanded () const

Returns the current value indicating if the widget is expanded.
### Return value

**true** if the widget is expanded; otherwise **false**.
## void setLifetime ( )

Sets a new lifetime management type for the root of the widget, or for the widget itself (if it is not a child for another widget).
> **Notice:** Lifetime of each widget in the hierarchy is defined by its root. Thus, lifetime management type set for a child widget that differs from the one set for the root is ignored.

. One of the [LIFETIME_*](#LIFETIME) variables.
### Arguments

- **lifetime** - The lifetime management type.

## getLifetime () const

Returns the current lifetime management type for the root of the widget, or for the widget itself (if it is not a child for another widget).
> **Notice:** Lifetime of each widget in the hierarchy is defined by its root. Thus, lifetime management type set for a child widget that differs from the one set for the root is ignored.

. One of the [LIFETIME_*](#LIFETIME) variables.
### Return value

Current lifetime management type.
## float getDpiScale () const

Returns the current DPI scale applied to the widget.
### Return value

Current DPI scale applied to the widget.
## int getRenderHeight () const

Returns the current widget frame height in pixels.
### Return value

Current widget frame height in pixels.
## int getRenderWidth () const

Returns the current widget frame width in pixels.
### Return value

Current widget frame width in pixels.
## getEventRemove () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## getEventDragDrop () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## getEventDragMove () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## getEventLeave () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## getEventEnter () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## getEventTextPressed () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## getEventKeyPressed () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## getEventReleased () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## getEventPressed () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## getEventDoubleClicked () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## getEventClicked () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## getEventChanged () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## getEventFocusOut () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## getEventFocusIn () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## getEventHide () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## getEventShow () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## void setTextDirection ( int direction )

Sets a new base paragraph direction for this widget's text, one of the *Gui::TEXT_DIRECTION_** values. With *TEXT_DIRECTION_AUTO* (default) the direction is inherited from the **[getGlobalTextDirection()()](../../../api/library/gui/class.gui_usc.md#getGlobalTextDirection_int)** property of the GUI, and if that is also set to auto, it is detected from the text content.
### Arguments

- *int* **direction** - The base direction of the widget text

## int getTextDirection () const

Returns the current base paragraph direction for this widget's text, one of the *Gui::TEXT_DIRECTION_** values. With *TEXT_DIRECTION_AUTO* (default) the direction is inherited from the **[getGlobalTextDirection()()](../../../api/library/gui/class.gui_usc.md#getGlobalTextDirection_int)** property of the GUI, and if that is also set to auto, it is detected from the text content.
### Return value

Current base direction of the widget text
---

## Widget getChild ( int num )

Returns a child widget with a given number.
### Arguments

- *int* **num** - Widget number.

### Return value

Required widget.
## int isChild ( Widget w )

Checks if a given widget is a child of the current one.
### Arguments

- *[Widget](../../../api/library/gui/class.widget_usc.md)* **w** - Widget to check.

### Return value

**1** if the widget in question is a child; otherwise, **0**.
## void setFocus ( )

Make the widget focused.
## int isFocused ( )

Returns a value indicating if the widget is currently in focus.
### Return value

1 if the widget is in focus; otherwise, 0.
## void setFont ( string name )

Sets a true-type font (*.ttf) that will be used to render text on the widget by file path.
### Arguments

- *string* **name** - Path to the font file (`*.ttf`) stored in your project's `data` folder.

## int getIntersection ( int local_pos_x , int local_pos_y )

Checks for an intersection with the widget's bounds for the given point.
### Arguments

- *int* **local_pos_x** - Local X coordinate.
- *int* **local_pos_y** - Local Y coordinate.

### Return value

**1** if the input coordinate is inside the widget; otherwise, **0**.
## Widget getHierarchyIntersection ( int screen_pos_x , int screen_pos_y )

Checks for an intersection with a widget that belongs to the hierarchy of the current widget.
### Arguments

- *int* **screen_pos_x** - The X coordinate of the screen position.
- *int* **screen_pos_y** - The Y coordinate of the screen position.

### Return value

Widget the intersection with which is found.
## int getKeyActivity ( unsigned int key )

Checks if a given key already has a special purpose for the widget.
### Arguments

- *unsigned int* **key** - One of the standard ASCII keycodes or one of the *[INPUT_KEY_*](../../../api/library/controls/class.input_usc.md#KEY_UNKNOWN)*pre-defined variables.

### Return value

1 if the key cannot be used; otherwise, 0.
## void setPermanentFocus ( )

Sets permanent focus on the widget (it means that the widget is always in focus).
## void setPosition ( int x , int y )

Sets a position of the widget relative to its parent in [logical units](../../../principles/dpi/index.md).
### Arguments

- *int* **x** - X coordinate of the upper left corner of the widget in [logical units](../../../principles/dpi/index.md).
- *int* **y** - Y coordinate of the upper left corner of the widget in [logical units](../../../principles/dpi/index.md).

## void setToolTip ( string str , int reset = 0 )

Sets a tooltip for the widget.
### Arguments

- *string* **str** - Tooltip text.
- *int* **reset** - **1** to recalculate a tooltip location if the mouse cursor was relocated; otherwise � **0**(by default).

## string getToolTip ( )

Returns the widget's tooltip text.
### Return value

Tooltip text.
## void addAttach ( Widget w , string format = 0 , int multiplier = 1 , int flags = 0 )

Attaches a given widget to the current one. When applied to checkboxes, converts them into a group of radio buttons. A horizontal/vertical slider can be attached to a label or a text field. The text field can be attached to any of the sliders.
### Arguments

- *[Widget](../../../api/library/gui/class.widget_usc.md)* **w** - Widget to attach.
- *string* **format** - Format string for values entered into the attached widget. If none specified, **"%d"** is implied. This is an optional parameter.
- *int* **multiplier** - Multiplier value, which is used to scale values provided by the attached widget. This is an optional parameter.
- *int* **flags** - One of the [*ATTACH_**](../../../api/library/gui/class.gui_usc.md) pre-defined variables. This is an optional parameter.

## void addChild ( Widget w , int flags = 0 )

Adds a child to the widget.
### Arguments

- *[Widget](../../../api/library/gui/class.widget_usc.md)* **w** - Child widget.
- *int* **flags** - One of the [*ALIGN_**](../../../api/library/gui/class.gui_usc.md) pre-defined variables. This is an optional parameter.

## void arrange ( )

Rearranges the widget and its children to lay them out neatly. This function forces to recalculate widget size and allows to get updated GUI layout data in the current frame. If this function is not called, widget modifications made in the current *update()* will be available only in the next frame (i.e. with one-frame lag), as GUI is calculated and rendered after the script *update()* function has been executed.
## void raise ( Widget w )

Brings a given widget to the top.
> **Notice:** Works only for widgets added to GUI via the [*addChild()*](../../../api/library/gui/class.gui_usc.md#addChild_Widget_int_void) function with the [GUI_ALIGN_OVERLAP](../../../api/library/gui/class.gui_usc.md#ALIGN_OVERLAP) flag specified (should not be [GUI_ALIGN_FIXED](../../../api/library/gui/class.gui_usc.md#ALIGN_FIXED)).


### Arguments

- *[Widget](../../../api/library/gui/class.widget_usc.md)* **w** - Widget to be brought up.

## void removeAttach ( Widget w )

Detaches a given widget from the current one.
### Arguments

- *[Widget](../../../api/library/gui/class.widget_usc.md)* **w** - Widget to detach.

## void removeChild ( Widget w )

Removes a child widget from the list of the widget's children.
### Arguments

- *[Widget](../../../api/library/gui/class.widget_usc.md)* **w** - Child widget.

## void removeFocus ( )

Removes focus from the widget.
## void replaceChild ( Widget w , Widget old_w , int flags = 0 )

Replaces one child widget with another.
### Arguments

- *[Widget](../../../api/library/gui/class.widget_usc.md)* **w** - Replacement widget.
- *[Widget](../../../api/library/gui/class.widget_usc.md)* **old_w** - Widget to be replaced.
- *int* **flags** - One of the [*ALIGN_**](../../../api/library/gui/class.gui_usc.md) pre-defined variables. This is an optional parameter.

## int getLifetimeSelf ( )

Returns the lifetime management type set for the widget.
> **Notice:** Lifetime of each widget in the hierarchy is defined by it's root. Setting lifetime management type for a child widget different from the one set for the root has no effect.


## ivec2 getTextRenderSize ( const char * OUT_text )

Returns the size (in pixels) of the specified text string rendered on the screen with taking into account all text output settings such as dpi, font size and style.
### Arguments

- *const char ** **OUT_text** - Text string. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

### Return value

Text size in pixels.
## void runEventShow ( )

Emulates the *[Show](#getEventShow_Event)* event.
## void runEventHide ( )

Emulates the *[Hide](#getEventHide_Event)* event.
## void runEventFocusIn ( )

Emulates the *[FocusIn](#getEventFocusIn_Event)* event.
## void runEventFocusOut ( )

Emulates the *[FocusOut](#getEventFocusOut_Event)* event.
## void runEventChanged ( )

Emulates the *[Changed](#getEventChanged_Event)* event.
## void runEventClicked ( int mouse_buttons )

Emulates the *[Clicked](#getEventClicked_Event)* event.
### Arguments

- *int* **mouse_buttons** - Mouse button - a mask representing a combination of the following flags: *[Gui.MOUSE_MASK_LEFT](../../../api/library/gui/class.gui_usc.md#MOUSE_MASK_LEFT) | [Gui.MOUSE_MASK_MIDDLE](../../../api/library/gui/class.gui_usc.md#MOUSE_MASK_MIDDLE) | [Gui.MOUSE_MASK_RIGHT](../../../api/library/gui/class.gui_usc.md#MOUSE_MASK_RIGHT)*.

## void runEventDoubleClicked ( )

Emulates the *[DoubleClicked](#getEventDoubleClicked_Event)* event.
## void runEventPressed ( int mouse_buttons )

Emulates the *[Pressed](#getEventPressed_Event)* event.
### Arguments

- *int* **mouse_buttons** - Mouse button - a mask representing a combination of the following flags: *[Gui.MOUSE_MASK_LEFT](../../../api/library/gui/class.gui_usc.md#MOUSE_MASK_LEFT) | [Gui.MOUSE_MASK_MIDDLE](../../../api/library/gui/class.gui_usc.md#MOUSE_MASK_MIDDLE) | [Gui.MOUSE_MASK_RIGHT](../../../api/library/gui/class.gui_usc.md#MOUSE_MASK_RIGHT)*.

## void runEventReleased ( int mouse_buttons )

Emulates the *[Released](#getEventReleased_Event)* event.
### Arguments

- *int* **mouse_buttons** - Mouse button - a mask representing a combination of the following flags: *[Gui.MOUSE_MASK_LEFT](../../../api/library/gui/class.gui_usc.md#MOUSE_MASK_LEFT) | [Gui.MOUSE_MASK_MIDDLE](../../../api/library/gui/class.gui_usc.md#MOUSE_MASK_MIDDLE) | [Gui.MOUSE_MASK_RIGHT](../../../api/library/gui/class.gui_usc.md#MOUSE_MASK_RIGHT)*.

## void runEventKeyPressed ( int key )

Emulates the *[KeyPressed](#getEventKeyPressed_Event)* event.
### Arguments

- *int* **key** - Key scan code.

## void runEventTextPressed ( unsigned int code )

Emulates the *[TextPressed](#getEventTextPressed_Event)* event.
### Arguments

- *unsigned int* **code** - Vistual key.

## void runEventEnter ( )

Emulates the *[Enter](#getEventEnter_Event)* event.
## void runEventLeave ( )

Emulates the *[Leave](#getEventLeave_Event)* event.
## void runEventDragMove ( Widget pointer )

Emulates the *[DragMove](#getEventDragMove_Event)* event.
### Arguments

- *[Widget](../../../api/library/gui/class.widget_usc.md)* **pointer** - Underlying widget.

## void runEventDragDrop ( Widget pointer )

Emulates the *[DragDrop](#getEventDragDrop_Event)* event.
### Arguments

- *[Widget](../../../api/library/gui/class.widget_usc.md)* **pointer** - Target widget.

## ivec2 getTextUnitSize ( string text )

Returns the text dimensions (width and height in logical unit). This function helps you estimate how well the text will fit in the widget before rendering.
### Arguments

- *string* **text** - Text string.

### Return value

Text size in logical unit (width, height).
