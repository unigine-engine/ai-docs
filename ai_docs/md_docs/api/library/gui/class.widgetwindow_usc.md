# Unigine::WidgetWindow Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** Widget


This class creates a [titled window](../../../code/gui/ui/ui_containers.md#window).


The object of this class looks as follows:


![](../../../code/gui/ui/widgets/window.png)


By default, the window created by means of this class consists of a [single vertical column container](../../../api/library/gui/class.widgetvbox_usc.md) and a drag area at the top.


The WidgetWindow class provides methods that allow [editing the drag area](#setDragAreaEnabled_int_void). For example:


The window will be rendered as follows:


![](drag_area.png)


### See Also


- C++ sample
- C# Component sample
- UnigineScript sample


## WidgetWindow Class

### Members

## void setText ( string text )

Sets a new window title.
### Arguments

- *string* **text** - The window title.

## const char * getText () const

Returns the current window title.
### Return value

Current window title.
## void setTextAlign ( int align )

Sets a new alignment of the window title. One of the **[GUI_ALIGN_()](../../../api/library/gui/class.gui_usc.md#ALIGN_BACKGROUND)** pre-defined variables.
### Arguments

- *int* **align** - The alignment of the window title

## int getTextAlign () const

Returns the current alignment of the window title. One of the **[GUI_ALIGN_()](../../../api/library/gui/class.gui_usc.md#ALIGN_BACKGROUND)** pre-defined variables.
### Return value

Current alignment of the window title
## int getPaddingBottom () const

Returns the current bottom padding for the widget content.
### Return value

Current bottom padding in pixels.
## int getPaddingTop () const

Returns the current top padding for the widget content.
### Return value

Current top padding in pixels.
## int getPaddingRight () const

Returns the current right-side padding for the widget content.
### Return value

Current right-side padding in pixels.
## int getPaddingLeft () const

Returns the current left-side padding for the widget content.
### Return value

Current left-side padding in pixels.
## int getSpaceY () const

Returns the current vertical space between the widgets in the window and between them and the window border.
### Return value

Current vertical space.
## int getSpaceX () const

Returns the current horizontal space between the widgets in the window and between them and the window border.
### Return value

Current horizontal space.
## void setMaxHeight ( int height )

Sets a new maximum height value of the window.
### Arguments

- *int* **height** - The maximum height value.

## int getMaxHeight () const

Returns the current maximum height value of the window.
### Return value

Current maximum height value.
## void setMaxWidth ( int width )

Sets a new maximum width value of the window.
### Arguments

- *int* **width** - The maximum width value.

## int getMaxWidth () const

Returns the current maximum width value of the window.
### Return value

Current maximum width value.
## void setTransform ( mat4 transform )

Sets a new global widget transformation matrix.
### Arguments

- *mat4* **transform** - The transformation matrix.

## mat4 getTransform () const

Returns the current global widget transformation matrix.
### Return value

Current transformation matrix.
## void setColor ( vec4 color )

Sets a new color for the global color multiplier. The default is equivalent to **#ffffff** (white).
### Arguments

- *vec4* **color** - The color of the global color multiplier

## vec4 getColor () const

Returns the current color for the global color multiplier. The default is equivalent to **#ffffff** (white).
### Return value

Current color of the global color multiplier
## void setSnapDistance ( int distance )

Sets a new distance, at which the window snaps to another window or screen edge. The default is 0 (do not snap).
### Arguments

- *int* **distance** - The distance in pixels.

## int getSnapDistance () const

Returns the current distance, at which the window snaps to another window or screen edge. The default is 0 (do not snap).
### Return value

Current distance in pixels.
## void setFloatable ( int floatable )

Sets a new value indicating if the window is animated when changing to the minimized state and back. By default this option is disabled.
### Arguments

- *int* **floatable** - The value 1 for the window animation, 0 � disable.

## int isFloatable () const

Returns the current value indicating if the window is animated when changing to the minimized state and back. By default this option is disabled.
### Return value

Current value 1 for the window animation, 0 � disable.
## void setBlendable ( int blendable )

Sets a new value indicating if the window can fade in and out when changing to the minimized state and back. By default this option is disabled.
### Arguments

- *int* **blendable** - The fading of the window in and out when its visibility changesvalue 1 for the window ability to fade in and out, 0 � disable.

## int isBlendable () const

Returns the current value indicating if the window can fade in and out when changing to the minimized state and back. By default this option is disabled.
### Return value

Current fading of the window in and out when its visibility changesvalue 1 for the window ability to fade in and out, 0 � disable.
## void setTitleable ( int titleable )

Sets a new value indicating if the window is minimized when double-clicking on it. By default this option is disabled.
### Arguments

- *int* **titleable** - The minimization of the window on a double click of the titlevalue 1 for the window minimization on double click, 0 � disable.

## int isTitleable () const

Returns the current value indicating if the window is minimized when double-clicking on it. By default this option is disabled.
### Return value

Current minimization of the window on a double click of the titlevalue 1 for the window minimization on double click, 0 � disable.
## void setSizeable ( int sizeable )

Sets a new value indicating if the window is resizeable. By default this option is disabled.
### Arguments

- *int* **sizeable** - The resizing of the windowvalue 1 for the ability to resize the window, 0 � disable.

## int isSizeable () const

Returns the current value indicating if the window is resizeable. By default this option is disabled.
### Return value

Current resizing of the windowvalue 1 for the ability to resize the window, 0 � disable.
## void setMoveable ( int moveable )

Sets a new value indicating if the window is movable. By default this option is disabled.
### Arguments

- *int* **moveable** - The moving of the windowvalue 1 for the ability to move the window, 0 � disable.

## int isMoveable () const

Returns the current value indicating if the window is movable. By default this option is disabled.
### Return value

Current moving of the windowvalue 1 for the ability to move the window, 0 � disable.
## void setBorderColor ( vec4 color )

Sets a new border color for the widget.
### Arguments

- *vec4* **color** - The border color for the widget

## vec4 getBorderColor () const

Returns the current border color for the widget.
### Return value

Current border color for the widget
## void setBackgroundColor ( vec4 color )

Sets a new background color used for the widget.
### Arguments

- *vec4* **color** - The background color used for the widget

## vec4 getBackgroundColor () const

Returns the current background color used for the widget.
### Return value

Current background color used for the widget
## void setDragAreaEnabled ( bool enabled )

Sets a new value indicating if the drag area of the window is enabled.
### Arguments

- *bool* **enabled** - Set **true** to enable the drag area of the window; **false** - to disable it.

## bool isDragAreaEnabled () const

Returns the current value indicating if the drag area of the window is enabled.
### Return value

**true** if the drag area of the window is enabled ; otherwise **false**.
## int getDragAreaPaddingTop () const

Returns the current top padding for the drag area.
### Return value

Current top padding in pixels.
## int getDragAreaPaddingRight () const

Returns the current right-side padding for the drag area.
### Return value

Current right-side padding in pixels.
## void setDragAreaBackgroundColor ( )

Sets a new color for the background of the drag area.
### Arguments

- **color** - The background color.

## getDragAreaBackgroundColor () const

Returns the current color for the background of the drag area.
### Return value

Current background color.
## void setDragAreaBackground ( int background )

Sets a new value indicating if background rendering is enabled or disabled for the drag area.
### Arguments

- *int* **background** - The value indicating if rendering of the background is enabled (**1** if rendering is enabled; otherwise, **0**).

## int getDragAreaBackground () const

Returns the current value indicating if background rendering is enabled or disabled for the drag area.
### Return value

Current value indicating if rendering of the background is enabled (**1** if rendering is enabled; otherwise, **0**).
## int getDragAreaPaddingLeft () const

Returns the current left-side padding for the drag area.
### Return value

Current left-side padding in pixels.
## int getDragAreaPaddingBottom () const

Returns the current bottom padding for the drag area.
### Return value

Current bottom padding in pixels.
## void setGlobalMovement ( bool movement )

Sets a new value specifying if the window can be moved across the whole GUI or only within the parent widget. By default, this option is set to false, and the window can be moved only relevant to its parent.
### Arguments

- *bool* **movement** - Set **true** to enable moving the window across the whole GUI; **false** - to disable it.

## bool isGlobalMovement () const

Returns the current value specifying if the window can be moved across the whole GUI or only within the parent widget. By default, this option is set to false, and the window can be moved only relevant to its parent.
### Return value

**true** if moving the window across the whole GUI is enabled ; otherwise **false**.
## int getMinTextureWidth () const

Returns the current minimum width of the window render � the width of the window texture from the GUI skin.
### Return value

Current minimum width of the window render, in pixels.
## int getTextWidth () const

Returns the current window header width.
### Return value

Current window header width, in pixels.
## int getTextHeight () const

Returns the current window header height.
### Return value

Current window header height, in pixels.
## void setOutBoundsCallbacksEnabled ( bool enabled )

Sets a new value specifying if the callback processing for the window child widgets is enabled when the cursor is outside the window.
### Arguments

- *bool* **enabled** - Set **true** to enable callback processing for the child widgets if the cursor is outside the window; **false** - to disable it.

## bool isOutBoundsCallbacksEnabled () const

Returns the current value specifying if the callback processing for the window child widgets is enabled when the cursor is outside the window.
### Return value

**true** if callback processing for the child widgets if the cursor is outside the window is enabled ; otherwise **false**.
## int getMinTextureHeight () const

Returns the current minimum height of the window render � the height of the window texture from the GUI skin.
### Return value

Current minimum height of the window render, in pixels.
## void setStencil ( int stencil )

Sets a new value indicating if a widget cuts off its children along its set [bounds](../../../api/library/gui/class.widget_usc.md#setWidth_int_void). Everything that lies outside of them, is not rendered. This option works only if children have [ALIGN_OVERLAP](../../../api/library/gui/class.gui_usc.md#ALIGN_OVERLAP) flag set (otherwise, they will expand the box widget bounds and no cutting will be done).
### Arguments

- *int* **stencil** - The value indicating if a widget cuts off its children along its set bounds

## int getStencil () const

Returns the current value indicating if a widget cuts off its children along its set [bounds](../../../api/library/gui/class.widget_usc.md#setWidth_int_void). Everything that lies outside of them, is not rendered. This option works only if children have [ALIGN_OVERLAP](../../../api/library/gui/class.gui_usc.md#ALIGN_OVERLAP) flag set (otherwise, they will expand the box widget bounds and no cutting will be done).
### Return value

Current value indicating if a widget cuts off its children along its set bounds
---

## static WidgetWindow ( Gui gui , string str = 0 , int x = 0 , int y = 0 )

Constructor. Creates a window with given parameters and adds it to the specified GUI.
### Arguments

- *[Gui](../../../api/library/gui/class.gui_usc.md)* **gui** - [GUI](../../../api/library/gui/class.gui_usc.md), to which the new window will belong.
- *string* **str** - Window title. This is an optional parameter.
- *int* **x** - Horizontal space between the widgets in the window and between them and the window border. This is an optional parameter.
- *int* **y** - Vertical space between the widgets in the window and between them and the window border. This is an optional parameter.

## static WidgetWindow ( string str = 0 , int x = 0 , int y = 0 )

Constructor. Creates a window with given parameters and adds it to the Engine GUI.
### Arguments

- *string* **str** - Window title. This is an optional parameter.
- *int* **x** - Horizontal space between the widgets in the window and between them and the window border. This is an optional parameter.
- *int* **y** - Vertical space between the widgets in the window and between them and the window border. This is an optional parameter.

## void setPadding ( int l , int r , int t , int b )

Sets widget paddings for all sides. Padding clears an area around the content of a widget (inside of it).
### Arguments

- *int* **l** - Left-side padding in pixels.
- *int* **r** - Right-side padding in pixels.
- *int* **t** - Top padding in pixels.
- *int* **b** - Bottom padding in pixels.

## void setSpace ( int x , int y )

Sets a space between the widgets in the window and between them and the window border.
### Arguments

- *int* **x** - Horizontal space. If a negative value is provided, 0 will be used instead.
- *int* **y** - Vertical space. If a negative value is provided, 0 will be used instead.

## void setDragAreaPadding ( int l , int r , int t , int b )

Sets paddings for all sides of the drag area.
### Arguments

- *int* **l** - Left-side padding in pixels.
- *int* **r** - Right-side padding in pixels.
- *int* **t** - Top padding in pixels.
- *int* **b** - Bottom padding in pixels.
