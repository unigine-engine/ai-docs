# Unigine::Gui Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


Creates a GUI. Different types of GUI widgets can be either added to one of the following:

- To the system GUI (Unigine user interface) that is rendered on top of application window.
- To the [GUI object](../../../api/library/objects/class.objectgui_usc.md) positioned in the world. In this case, any postprocessing filter can be applied.

Default values returned by the following methods can be overridden via [RC files](../../../code/gui/rc.md) defining a custom GUI.
## Gui Class

### Members

## int getNumChildren () const

Returns the current
### Return value

Current
## void setMouseGrab ( int grab )

Sets a new value indicating if the mouse pointer is bound to the GUI.
### Arguments

- *int* **grab** - The value indicating if the mouse pointer is bound to the GUI: 1 if the mouse pointer cannot leave the GUI; otherwise, 0.

## int getMouseGrab () const

Returns the current value indicating if the mouse pointer is bound to the GUI.
### Return value

Current value indicating if the mouse pointer is bound to the GUI: 1 if the mouse pointer cannot leave the GUI; otherwise, 0.
## void setMouseCursor ( int cursor )

Sets a new mouse cursor value, one of the *CURSOR_** pre-defined variables.
### Arguments

- *int* **cursor** - The mouse cursor value, one of the *CURSOR_** pre-defined variables.

## int getMouseCursor () const

Returns the current mouse cursor value, one of the *CURSOR_** pre-defined variables.
### Return value

Current mouse cursor value, one of the *CURSOR_** pre-defined variables.
## void setMouseSprite ( WidgetSprite sprite )

Sets a new custom mouse pointer currently in use.
### Arguments

- *[WidgetSprite](../../../api/library/gui/class.widgetsprite_usc.md)* **sprite** - The sprite with a custom mouse pointer, or NULL if the standard mouse pointer is used.

## WidgetSprite getMouseSprite () const

Returns the current custom mouse pointer currently in use.
### Return value

Current sprite with a custom mouse pointer, or NULL if the standard mouse pointer is used.
## void setMouseEnabled ( int enabled )

Sets a new value indicating if the mouse cursor is rendered.
### Arguments

- *int* **enabled** - The rendering of the mouse cursor

## int isMouseEnabled () const

Returns the current value indicating if the mouse cursor is rendered.
### Return value

Current rendering of the mouse cursor
## void setToolTipTime ( float time )

Sets a new delay before tooltip appearing.
### Arguments

- *float* **time** - The delay before tooltip appearing, in cycles per second.

## float getToolTipTime () const

Returns the current delay before tooltip appearing.
### Return value

Current delay before tooltip appearing, in cycles per second.
## void setToolTipAlpha ( float alpha )

Sets a new alpha value of a tooltip.
### Arguments

- *float* **alpha** - The alpha value of a tooltip.

## float getToolTipAlpha () const

Returns the current alpha value of a tooltip.
### Return value

Current alpha value of a tooltip.
## void setToolTipColor ( vec4 color )

Sets a new font color of a tooltip.
### Arguments

- *vec4* **color** - The font color of a tooltip. The default is equivalent to **#000000** (black).

## vec4 getToolTipColor () const

Returns the current font color of a tooltip.
### Return value

Current font color of a tooltip. The default is equivalent to **#000000** (black).
## void setToolTipWidth ( int width )

Sets a new width of the tooltip.
### Arguments

- *int* **width** - The width of the tooltip.

## int getToolTipWidth () const

Returns the current width of the tooltip.
### Return value

Current width of the tooltip.
## void setToolTipSize ( int size )

Sets a new font size of a tooltip.
### Arguments

- *int* **size** - The font size of a tooltip.

## int getToolTipSize () const

Returns the current font size of a tooltip.
### Return value

Current font size of a tooltip.
## void setToolTipEnabled ( int enabled )

Sets a new value indicating if tooltips are available.
### Arguments

- *int* **enabled** - The tooltips display

## int isToolTipEnabled () const

Returns the current value indicating if tooltips are available.
### Return value

Current tooltips display
## void setTransparentAlpha ( float alpha )

Sets a new alpha value of a transparent widget. A widget is transparent, if it uses blending.
### Arguments

- *float* **alpha** - The alpha value of a transparent widget. **0** means completely transparent.

## float getTransparentAlpha () const

Returns the current alpha value of a transparent widget. A widget is transparent, if it uses blending.
### Return value

Current alpha value of a transparent widget. **0** means completely transparent.
## void setTransparentColor ( vec4 color )

Sets a new font color of a transparent widget. A widget is transparent, if it uses blending.
### Arguments

- *vec4* **color** - The font color of a transparent widget. The default is equivalent to **#869caa** (light bluish).

## vec4 getTransparentColor () const

Returns the current font color of a transparent widget. A widget is transparent, if it uses blending.
### Return value

Current font color of a transparent widget. The default is equivalent to **#869caa** (light bluish).
## void setTransparentEnabled ( int enabled )

Sets a new value indicating if a widget can be rendered as [transparent](../../../code/gui/rc.md#transparent) (i.e. change its color accordingly), when necessary. For example, it can indicate whether the drop-down list of combobox is transparent or not.
### Arguments

- *int* **enabled** - The rendering of a widget as transparent

## int isTransparentEnabled () const

Returns the current value indicating if a widget can be rendered as [transparent](../../../code/gui/rc.md#transparent) (i.e. change its color accordingly), when necessary. For example, it can indicate whether the drop-down list of combobox is transparent or not.
### Return value

Current rendering of a widget as transparent
## void setDisabledAlpha ( float alpha )

Sets a new alpha value of a disabled widget.
### Arguments

- *float* **alpha** - The alpha value of a disabled widget. **0** means completely transparent.

## float getDisabledAlpha () const

Returns the current alpha value of a disabled widget.
### Return value

Current alpha value of a disabled widget. **0** means completely transparent.
## void setDisabledColor ( vec4 color )

Sets a new font color of a disabled widget.
### Arguments

- *vec4* **color** - The font color of a disabled widget. The default is equivalent to **#869caa** (light bluish).

## vec4 getDisabledColor () const

Returns the current font color of a disabled widget.
### Return value

Current font color of a disabled widget. The default is equivalent to **#869caa** (light bluish).
## void setDisabledEnabled ( int enabled )

Sets a new value indicating if a widget can be rendered as [disabled](../../../code/gui/rc.md#disabled) (i.e. change its color accordingly), when necessary.
### Arguments

- *int* **enabled** - The rendering of a widget as disabled

## int isDisabledEnabled () const

Returns the current value indicating if a widget can be rendered as [disabled](../../../code/gui/rc.md#disabled) (i.e. change its color accordingly), when necessary.
### Return value

Current rendering of a widget as disabled
## void setFocusedAlpha ( float alpha )

Sets a new alpha value of a focused widget.
### Arguments

- *float* **alpha** - The alpha value of a focused widget. **0** means completely transparent.

## float getFocusedAlpha () const

Returns the current alpha value of a focused widget.
### Return value

Current alpha value of a focused widget. **0** means completely transparent.
## void setFocusedColor ( vec4 color )

Sets a new font color of a focused widget.
### Arguments

- *vec4* **color** - The font color of a focused widget. The default is equivalent to **#ffffff** (white).

## vec4 getFocusedColor () const

Returns the current font color of a focused widget.
### Return value

Current font color of a focused widget. The default is equivalent to **#ffffff** (white).
## void setFocusedPermanent ( int permanent )

Sets a new value indicating if the permanent color of the focused widget is changed.
### Arguments

- *int* **permanent** - The change of the permanent color of the focused widget

## int isFocusedPermanent () const

Returns the current value indicating if the permanent color of the focused widget is changed.
### Return value

Current change of the permanent color of the focused widget
## void setFocusedEnabled ( int enabled )

Sets a new value indicating if a widget can be rendered as [focused](../../../code/gui/rc.md#focused) on (i.e. change its color accordingly), when necessary.
### Arguments

- *int* **enabled** - The rendering of a widget as focused on

## int isFocusedEnabled () const

Returns the current value indicating if a widget can be rendered as [focused](../../../code/gui/rc.md#focused) on (i.e. change its color accordingly), when necessary.
### Return value

Current rendering of a widget as focused on
## void setDefaultAlpha ( float alpha )

Sets a new standard alpha value of a widget.
### Arguments

- *float* **alpha** - The standard alpha value of a widget. **0** means completely transparent.

## float getDefaultAlpha () const

Returns the current standard alpha value of a widget.
### Return value

Current standard alpha value of a widget. **0** means completely transparent.
## void setDefaultColor ( vec4 color )

Sets a new standard font color of a widget.
### Arguments

- *vec4* **color** - The standard font color of a widget. The default is equivalent to **#ddddff** (blue-white).

## vec4 getDefaultColor () const

Returns the current standard font color of a widget.
### Return value

Current standard font color of a widget. The default is equivalent to **#ddddff** (blue-white).
## void setDefaultSize ( int size )

Sets a new standard font size of a widget.
### Arguments

- *int* **size** - The standard font size of a widget.

## int getDefaultSize () const

Returns the current standard font size of a widget.
### Return value

Current standard font size of a widget.
## void setFadeOutSpeed ( float speed )

Sets a new duration of fade-out animation played when a widget loses focus.
### Arguments

- *float* **speed** - The duration in cycles per second, for example, **4** means that the duration is a **1/4** of a second.

## float getFadeOutSpeed () const

Returns the current duration of fade-out animation played when a widget loses focus.
### Return value

Current duration in cycles per second, for example, **4** means that the duration is a **1/4** of a second.
## void setFadeInSpeed ( float speed )

Sets a new duration of fade-in animation played when a widget gets focused.
### Arguments

- *float* **speed** - The duration in cycles per second, for example, **8** means that the duration is a **1/8** of a second.

## float getFadeInSpeed () const

Returns the current duration of fade-in animation played when a widget gets focused.
### Return value

Current duration in cycles per second, for example, **8** means that the duration is a **1/8** of a second.
## void setExposeSpeed ( float speed = 1024 )

Sets a new duration of animation played when a widget appears.
### Arguments

- *float* **speed** - The duration in cycles per second. For example, **6** means that the duration is a **1/6** of a second. The value less than or equal to 0 implies that no smooth animations are applied.

## float getExposeSpeed () const

Returns the current duration of animation played when a widget appears.
### Return value

Current duration in cycles per second. For example, **6** means that the duration is a **1/6** of a second. The value less than or equal to 0 implies that no smooth animations are applied.
## void setTransform ( mat4 transform )

Sets a new global GUI transformation matrix. This 2D matrix can be tilted, rotated, moved or modified in many ways in 3D space.
### Arguments

- *mat4* **transform** - The global GUI transformation matrix.

## mat4 getTransform () const

Returns the current global GUI transformation matrix. This 2D matrix can be tilted, rotated, moved or modified in many ways in 3D space.
### Return value

Current global GUI transformation matrix.
## void setColor ( vec4 color )

Sets a new color of the global color multiplier.
### Arguments

- *vec4* **color** - The color of the global color multiplier. The default is equivalent to #ffffff (white).

## vec4 getColor () const

Returns the current color of the global color multiplier.
### Return value

Current color of the global color multiplier. The default is equivalent to #ffffff (white).
## int getHeight () const

Returns the current screen height.
### Return value

Current screen height, in [logical units](../../../principles/dpi/index.md).
## int getWidth () const

Returns the current screen width.
### Return value

Current screen width, in [logical units](../../../principles/dpi/index.md).
## void setHidden ( int hidden )

Sets a new value indicating if the GUI is hidden (not rendered).
### Arguments

- *int* **hidden** - The true if the GUI is hidden, false if it is shown

## int isHidden () const

Returns the current value indicating if the GUI is hidden (not rendered).
### Return value

Current true if the GUI is hidden, false if it is shown
## void setEnabled ( int enabled )

Sets a new
### Arguments

- *int* **enabled** - The the GUI

## int isEnabled () const

Returns the current
### Return value

Current the GUI
## bool isActive () const

Returns the current value indicating if any widget in the GUI is in focus.
### Return value

**true** if any widget in the GUI is in focus; otherwise **false**.
## WidgetVBox getVBox () const

Returns the current root widget of the GUI (a [WidgetVBox](../../../api/library/gui/class.widgetvbox_usc.md)).
### Return value

Current root widget of the GUI.
## Widget getPermanentFocus () const

Returns the current widget that is always in focus.
### Return value

Current widget that is always in focus.
## Widget getOverlappedFocus () const

Returns the current
### Return value

Current overlapped widget.
## Widget getFocus () const

Returns the current widget that is currently in focus.
### Return value

Current widget that is currently in focus.
## int getMouseDY () const

Returns the current difference between the previous position of the mouse pointer and the current one along the Y axis in [logical units](../../../principles/dpi/index.md).
### Return value

Current difference between the previous position of the mouse pointer and the current one along the Y axis in [logical units](../../../principles/dpi/index.md).
## int getMouseDX () const

Returns the current difference between the previous position of the mouse pointer and the current one along the X axis in [logical units](../../../principles/dpi/index.md).
### Return value

Current difference between the previous position of the mouse pointer and the current one along the X axis in [logical units](../../../principles/dpi/index.md).
## int getMouseY () const

Returns the current Y coordinate of the mouse pointer in the coordinate system of the application window in [logical units](../../../principles/dpi/index.md).
### Return value

Current Y coordinate of the mouse pointer in the coordinate system of the application window in [logical units](../../../principles/dpi/index.md).
## int getMouseX () const

Returns the current X coordinate of the mouse pointer in the coordinate system of the application window in [logical units](../../../principles/dpi/index.md).
### Return value

Current X coordinate of the mouse pointer in the coordinate system of the application window in [logical units](../../../principles/dpi/index.md).
## void setToolTipY ( int y )

Sets a new
### Arguments

- *int* **y** - The tooltip position along the Y axis.

## int getToolTipY () const

Returns the current
### Return value

Current tooltip position along the Y axis.
## void setToolTipX ( int x )

Sets a new
### Arguments

- *int* **x** - The tooltip position along the X axis.

## int getToolTipX () const

Returns the current
### Return value

Current tooltip position along the X axis.
## void setToolTipText ( string text )

Sets a new GUI tooltip text.
### Arguments

- *string* **text** - The GUI tooltip text.

## const char * getToolTipText () const

Returns the current GUI tooltip text.
### Return value

Current GUI tooltip text.
## bool isUnderCursor () const

Returns the current value indicating if the GUI object is under cursor.
### Return value

**true** if the GUI object is under cursor; otherwise **false**.
## int getMouseWheelHorizontal () const

Returns the current horizontal mouse scroll value.
### Return value

Current horizontal mouse scroll value in the [-1;1] range.
## int getMouseWheel () const

Returns the current mouse scroll value. Negative values correspond to scrolling downwards; positive values correspond to scrolling upwards; the value is zero when the mouse wheel is not scrolled.
### Return value

Current mouse scroll value in the [-1;1] range.
## void setMouseShow ( bool show )

Sets a new value indicating if the OS mouse pointer is displayed, or if the application cursor is used only.
### Arguments

- *bool* **show** - Set **true** to enable displaying of OS mouse pointer; **false** - to disable it.

## bool isMouseShow () const

Returns the current value indicating if the OS mouse pointer is displayed, or if the application cursor is used only.
### Return value

**true** if displaying of OS mouse pointer is enabled ; otherwise **false**.
## void setMouseButtons ( int buttons )

Sets a new mouse buttons the input of which is received.
### Arguments

- *int* **buttons** - The

## int getMouseButtons () const

Returns the current mouse buttons the input of which is received.
### Return value

Current
## void setWorldObject ( bool object )

Sets a new value indicating if the GUI object is available in the hierarchy and rendered as a world object, or if it should have the window handle.
### Arguments

- *bool* **object** - Set **true** to enable the GUI object is available in the hierarchy and rendered as a world object; **false** - to disable it.

## bool isWorldObject () const

Returns the current value indicating if the GUI object is available in the hierarchy and rendered as a world object, or if it should have the window handle.
### Return value

**true** if the GUI object is available in the hierarchy and rendered as a world object; otherwise **false**.
## void setWinHandle ( )

Sets a new engine handle of the window.
### Arguments

- **handle** - The window handle.

## getWinHandle () const

Returns the current engine handle of the window.
### Return value

Current window handle.
## void setPosition ( )

Sets a new GUI object position (top left corner) in screen coordinates.
### Arguments

- **position** - The GUI object position (top left corner) in screen coordinates.

## getPosition () const

Returns the current GUI object position (top left corner) in screen coordinates.
### Return value

Current GUI object position (top left corner) in screen coordinates.
## void setSize ( )

Sets a new GUI object size in [logical units](../../../principles/dpi/index.md).
### Arguments

- **size** - The GUI object size (width and height) in [logical units](../../../principles/dpi/index.md).

## getSize () const

Returns the current GUI object size in [logical units](../../../principles/dpi/index.md).
### Return value

Current GUI object size (width and height) in [logical units](../../../principles/dpi/index.md).
## void setDpiScale ( float scale )

Sets a new DPI scale applied to the GUI.
### Arguments

- *float* **scale** - The DPI scale applied to the GUI.

## float getDpiScale () const

Returns the current DPI scale applied to the GUI.
### Return value

Current DPI scale applied to the GUI.
## getEventUpdate () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## void setGlobalCursorMode ( int mode )

Sets a new default cursor movement mode applied to all text edit widgets of this GUI whose own *CursorMode* property is set to *CURSOR_MODE_AUTO*. Reading this property never returns *CURSOR_MODE_AUTO*: it resolves to *CURSOR_MODE_LOGICAL* (the effective default).
### Arguments

- *int* **mode** - The default cursor mode for text edit widgets

## int getGlobalCursorMode () const

Returns the current default cursor movement mode applied to all text edit widgets of this GUI whose own *CursorMode* property is set to *CURSOR_MODE_AUTO*. Reading this property never returns *CURSOR_MODE_AUTO*: it resolves to *CURSOR_MODE_LOGICAL* (the effective default).
### Return value

Current default cursor mode for text edit widgets
## void setGlobalTextDirection ( int direction )

Sets a new default base text direction applied to all widgets of this GUI whose own *TextDirection* property is set to *TEXT_DIRECTION_AUTO*. The default value is *TEXT_DIRECTION_AUTO* (the direction is detected from the text content).
### Arguments

- *int* **direction** - The default base text direction for widgets

## int getGlobalTextDirection () const

Returns the current default base text direction applied to all widgets of this GUI whose own *TextDirection* property is set to *TEXT_DIRECTION_AUTO*. The default value is *TEXT_DIRECTION_AUTO* (the direction is detected from the text content).
### Return value

Current default base text direction for widgets
---

## engine.gui. getCurrent ( )

Returns the current GUI instance.
### Return value

Current GUI instance.
## Widget engine.gui. getChild ( int num )

Returns a child widget with a given number.
### Arguments

- *int* **num** - Widget number.

### Return value

Required widget.
## int engine.gui. isChild ( Widget widget )

Checks if a given widget belongs to the GUI.
### Arguments

- *[Widget](../../../api/library/gui/class.widget_usc.md)* **widget** - Widget to check.

### Return value

**1** if the widget belongs to the GUI; otherwise, **0**.
## int engine.gui. getKeyActivity ( unsigned int key )

Checks if a given key already has a special purpose for the widget in focus.
### Arguments

- *unsigned int* **key** - One of the standard ASCII control codes or one of the *[KEY_*](../../../api/library/controls/class.input_usc.md#KEY_UNKNOWN)* pre-defined variables.

### Return value

**1** if the key cannot be used; otherwise, **0**.
## int engine.gui. setResource ( string name )

Changes the resource file skin used for widgets in the current GUI.
### Arguments

- *string* **name** - Path to the [*.rc](../../../code/gui/rc.md) file.

### Return value

**1** if the resource file is successfully changed; otherwise, **0**.
## void engine.gui. setToolTip ( int x , int y , string str )

Sets a tooltip to be displayed. The tooltip is positioned on the screen by its upper left corner. For the tooltip to be displayed, this function should be called each frame.
### Arguments

- *int* **x** - Screen position along the X axis.
- *int* **y** - Screen position along the Y axis.
- *string* **str** - Tooltip to display.

## int engine.gui. getToolTipHeight ( string str )

Returns a height of the given tooltip.
> **Notice:** Height of a single-line tooltip is equal to 21 pixels.


### Arguments

- *string* **str** - A tooltip text.

### Return value

Height of the given tooltip (in pixels).
## int engine.gui. getToolTipWidth ( string str )

Returns the current width of the tooltip.
### Arguments

- *string* **str** - A tooltip text.

### Return value

Width of the tooltip.
## void engine.gui. addChild ( Widget widget , int flags = 0 )

Adds a given widget to the GUI.
### Arguments

- *[Widget](../../../api/library/gui/class.widget_usc.md)* **widget** - Widget to add.
- *int* **flags** - One of the *GUI_ALIGN_** pre-defined variables. This is an optional parameter.

## int engine.gui. addDictionary ( string name , string language = 0 )

Adds a dictionary with required localization. Dictionaries cannot be changed in real-time.
### Arguments

- *string* **name** - Path to the dictionary file.
- *string* **language** - Name of the dictionary language.

### Return value

**1** if the dictionary is added successfully; otherwise, **0**.
## void engine.gui. clearDictionaries ( )

Unloads all loaded dictionaries.
## int engine.gui. clearTexture ( string name )

Clears the specified GUI texture file cache.
### Arguments

- *string* **name** - Name of the texture.

### Return value

1 if the texture is successfully cleared; otherwise, 0.
## Gui engine.gui. create ( string name = 0 )

GUI constructor.
### Arguments

- *string* **name** - GUI skin name.

### Return value

Pointer to the created GUI.
## int engine.gui. hasTranslation ( string arg1 )

Returns a value indicating if there is translation for a given string in the localization dictionary.
### Arguments

- *string* **arg1** - String to check.

### Return value

**1** if there is translation for the given string; otherwise, **0**.
## vec4 engine.gui. parseColor ( string str )

Converts a color string in the Web format (RRGGBB / #RRGGBB or RRGGBBAA / #RRGGBBAA) into its *vec4* equivalent.
### Arguments

- *string* **str** - Color string in the Web format.

### Return value

Color value as a *vec4* vector (R, G, B, A).
## void engine.gui. removeChild ( Widget widget )

Removes the specified widget from the GUI.
### Arguments

- *[Widget](../../../api/library/gui/class.widget_usc.md)* **widget** - Child widget to be removed.

## void engine.gui. removeFocus ( )

Removes the current focus.
## void engine.gui. replaceChild ( Widget widget , Widget old_widget , int flags = 0 )

Replaces a given widget in the GUI with another widget.
### Arguments

- *[Widget](../../../api/library/gui/class.widget_usc.md)* **widget** - Replacement widget.
- *[Widget](../../../api/library/gui/class.widget_usc.md)* **old_widget** - Widget to be replaced.
- *int* **flags** - One of the *GUI_ALIGN_** pre-defined variables. This is an optional parameter.

## int engine.gui. saveDictionary ( string name , string language = 0 )

Saves the dictionary with required localization. This function can be used to save the currently loaded dictionary into another file.
### Arguments

- *string* **name** - Path to a dictionary file.
- *string* **language** - Name of the dictionary language.

### Return value

**1** if the dictionary is saved successfully; otherwise, **0**.
## string engine.gui. translate ( string str )

Returns the source string translated using the dictionary.
### Arguments

- *string* **str** - String to translate (source).

### Return value

Target (translated) string if it is found in the localization dictionary; otherwise, the source string.
## void engine.gui. render ( )

Renders the GUI.
## void engine.gui. render ( int custom_mouse_buttons )

Renders the GUI.
### Arguments

- *int* **custom_mouse_buttons** - Pressed mouse button.

## int engine.gui. isRenderingBootScreen ( )

Returns a value indicating if the GUI currently renders the [boot screen](../../../code/gui/screens/index.md#boot).
### Return value

**1** if the GUI currently renders the [boot screen](../../../code/gui/screens/index.md#boot); otherwise, **0**.
## int engine.gui. isRenderingSplashScreen ( )

Returns a value indicating if the GUI currently renders the [splash screen](../../../code/gui/screens/index.md#splash).
### Return value

**1** if the GUI currently renders the [splash screen](../../../code/gui/screens/index.md#splash); otherwise, **0**.
## int engine.gui. isRenderingLoadingScreen ( )

Returns a value indicating if the GUI currently renders the [loading screen](../../../code/gui/screens/index.md#loading).
### Return value

**1** if the GUI currently renders the [loading screen](../../../code/gui/screens/index.md#loading); otherwise, **0**.
## void engine.gui. focusGained ( )

The focus is set on the GUI object.
## void engine.gui. focusLost ( )

The focus is removed from the GUI.
## int engine.gui. isHover ( int global_pos_x , int global_pos_y )

Returns a value indicating if the cursor is hovering over the GUI object.
### Arguments

- *int* **global_pos_x** - The X coordinate of the cursor in global coordinates.
- *int* **global_pos_y** - The Y coordinate of the cursor in global coordinates.

### Return value

**1** if the cursor is hovering over the GUI object; otherwise, **0**.
## Widget engine.gui. getWidgetIntersection ( int global_pos_x , int global_pos_y )

Returns the intersected widget that is visually perceptible (not empty, not transparent).
### Arguments

- *int* **global_pos_x** - The X coordinate of the [cursor in global coordinates](../../../api/library/controls/class.input_usc.md#getMousePosition_ivec2).
- *int* **global_pos_y** - The Y coordinate of the [cursor in global coordinates](../../../api/library/controls/class.input_usc.md#getMousePosition_ivec2).

### Return value

The intersected widget that is visually perceptible.
## Widget engine.gui. getUnderCursorWidget ( )

Returns the visually perceptible widget, over which the cursor is currently hovering.
### Return value

The widget, over which the cursor is currently hovering.
## Gui engine.gui. getFocusGui ( )

Returns the GUI object that is currently in focus.
### Return value

The GUI object currently in focus.
## Gui engine.gui. getGuiIntersection ( int global_pos_x , int global_pos_y )

Returns the intersected GUI object.
> **Notice:** This method takes Z-ordering into consideration: if the GUI object is overlapped by any other window, the method returns null.

### Arguments

- *int* **global_pos_x** - The X coordinate of the intersection point in global coordinates.
- *int* **global_pos_y** - The Y coordinate of the intersection point in global coordinates.

### Return value

The intersected GUI object.
## Gui engine.gui. getUnderCursorGui ( )

Returns the GUI object that is currently under cursor.
> **Notice:** If case of dragging or resizing a window, this method returns null. To receive the intersected GUI in such a case, use [getGuiIntersection()](#getGuiIntersection_int_int_Gui).

### Return value

GUI object currently under cursor.
## void engine.gui. getWorldGuiInstances ( Vector< Gui >& OUT_ret_instances )

Returns all GUI instances that are available in the scene hierarchy and rendered as world objects.
### Arguments

- *Vector<[Gui](../../../api/library/gui/class.gui_usc.md)>&* **OUT_ret_instances** - All GUI instances that are available in the scene hierarchy and rendered as world objects. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## int engine.gui. getAndClearMouseWheel ( )

Returns the mouse scroll value and clears the mouse scroll state info.
### Return value

The mouse scroll value in the [-1;1] range.
## void engine.gui. forceSetMouseWheel ( int value )

Sets the mouse scroll value.
### Arguments

- *int* **value** - The mouse scroll value in the [-1;1] range.

## int engine.gui. getAndClearMouseWheelHorizontal ( )

Returns the mouse horizontal scroll value and clears the mouse scroll state info.
### Return value

The horizontal mouse scroll value in the [-1;1] range.
## void engine.gui. forceSetMouseWheelHorizontal ( int value )

Sets the mouse vertical scroll value.
### Arguments

- *int* **value** - The horizontal mouse scroll value in the [-1;1] range.

## int engine.gui. getKey ( int key )

Returns the value indicating if the specified key is pressed.
### Arguments

- *int* **key** - One of the standard ASCII control codes or one of the *[KEY_*](../../../api/library/controls/class.input_usc.md#KEY_UNKNOWN)* pre-defined variables.

### Return value

**1** if the key is pressed; otherwise, **0**.
## int engine.gui. getAndClearKey ( int key )

Returns the value indicating if the specified key is pressed and clears the key state info.
### Arguments

- *int* **key** - One of the standard ASCII control codes or one of the *[KEY_*](../../../api/library/controls/class.input_usc.md#KEY_UNKNOWN)* pre-defined variables.

### Return value

**1** if the key is pressed; otherwise, **0**.
## int engine.gui. toRenderSize ( int unit_size )

Transforms the unit value to the pixel value.
### Arguments

- *int* **unit_size** - Size in units.

### Return value

Size in pixels.
## int engine.gui. toUnitSize ( int render_size )

Transforms the pixel value to the unit value.
### Arguments

- *int* **render_size** - Size in pixels.

### Return value

Size in units.
## int engine.gui. setFontPath ( string path )

Changes the regular font used for widgets in the current GUI.
### Arguments

- *string* **path** - Path to the font file.

### Return value

**1** if the font is set successfully, otherwise **0**.
## string engine.gui. getFontPath ( )

Returns the path to the regular font currently used for widgets in the current GUI.
### Return value

Path to the font file.
## int engine.gui. setFontPaths ( string normal_path , string bold_path , string italic_path , string bold_italic_path )

Changes the set of fonts � regular, bold, italic, and italic bold � used for widgets in the current GUI.
### Arguments

- *string* **normal_path** - Path to the regular font file.
- *string* **bold_path** - Path to the bold font file.
- *string* **italic_path** - Path to the italic font file.
- *string* **bold_italic_path** - Path to the bold italic font file.

### Return value

**1** if the fonts are set successfully, otherwise **0**.
## int engine.gui. setFontRichBoldPath ( string path )

Changes the bold font used for widgets in the current GUI.
### Arguments

- *string* **path** - Path to the bold font file.

### Return value

**1** if the fonts are set successfully, otherwise **0**.
## string engine.gui. getFontRichBoldPath ( )

Returns the path to the bold font currently used for widgets in the current GUI.
### Return value

Path to the bold font file.
## int engine.gui. setFontRichItalicPath ( string path )

Changes the italic font used for widgets in the current GUI.
### Arguments

- *string* **path** - Path to the italic font file.

### Return value

**1** if the font is set successfully, otherwise **0**.
## string engine.gui. getFontRichItalicPath ( )

Returns the path to the italic font currently used for widgets in the current GUI.
### Return value

Path to the italic font file.
## int engine.gui. setFontRichBoldItalicPath ( string path )

Changes the bold italic font used for widgets in the current GUI.
### Arguments

- *string* **path** - Path to the bold italic font file.

### Return value

**1** if the font is set successfully, otherwise **0**.
## string engine.gui. getFontRichBoldItalicPath ( )

Returns the path to the bold italic font currently used for widgets in the current GUI.
### Return value

Path to the bold italic font file.
## int engine.gui. setSkinPath ( string path )

Changes the skin used for widgets in the current GUI.
### Arguments

- *string* **path** - Path to the directory where the skin files (an [RC file](../../../code/gui/rc.md) and textures) are stored.

### Return value

**1** if the skin is set successfully, otherwise **0**.
## string engine.gui. getSkinPath ( )

Returns the path to the current GUI skin.
### Return value

Path to the directory where the skin files (an [RC file](../../../code/gui/rc.md) and textures) are stored.
## void engine.gui. setGlobalFontFallback ( Vector<String> fallbacks )

Sets the global list of fallback fonts. When a character is not found in the current font, the system searches these fonts in order. Global fallbacks apply to all fonts.
### Arguments

- *Vector<String>* **fallbacks** - List of paths to fallback font files.

## void engine.gui. getGlobalFontFallback ( Vector<String>& OUT_ret )

Returns the global list of fallback fonts.
### Arguments

- *Vector<String>&* **OUT_ret** - An array to store the paths to global fallback font files. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## void engine.gui. setFontFallback ( string font , Vector<String> fallbacks )

Sets the list of fallback fonts for a specific font. When a character is not found in the specified font, the system searches these fonts first, then the global fallbacks.
### Arguments

- *string* **font** - Path to the font file to set fallbacks for.
- *Vector<String>* **fallbacks** - List of paths to fallback font files.

## void engine.gui. getFontFallback ( string font , Vector<String>& OUT_ret )

Returns the list of fallback fonts for a specific font.
### Arguments

- *string* **font** - Path to the font file to get fallbacks for.
- *Vector<String>&* **OUT_ret** - An array to store the paths to fallback font files for the specified font. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.
