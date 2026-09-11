# Unigine::Gui Class (CS)


Creates a GUI. Different types of GUI widgets can be either added to one of the following:

- To the system GUI (Unigine user interface) that is rendered on top of application window.
- To the [GUI object](../../../api/library/objects/class.objectgui_cs.md) positioned in the world. In this case, any postprocessing filter can be applied.

Default values returned by the following methods can be overridden via [RC files](../../../code/gui/rc.md) defining a custom GUI.
## Gui Class

### Enums

## CursorMode

Cursor movement and hit-test mode for text edit widgets, relevant for bidirectional (mixed left-to-right and right-to-left) text.
| Name | Description |
|---|---|
| **CURSOR_MODE_AUTO** = 0 | On a widget, the mode is inherited from the **[GlobalCursorMode](../../...md#getGlobalCursorMode_int)** property of the *Gui*; on the *Gui* itself, this value is treated as *CURSOR_MODE_LOGICAL*. |
| **CURSOR_MODE_VISUAL** = 1 | The cursor moves over glyphs in on-screen (visual) order: arrow keys move the caret in the pressed direction even across boundaries between left-to-right and right-to-left text runs. |
| **CURSOR_MODE_LOGICAL** = 2 | The cursor moves through the underlying character sequence in logical (storage) order. |

## TextDirection

Base paragraph direction used for laying out widget text with bidirectional content.
| Name | Description |
|---|---|
| **TEXT_DIRECTION_AUTO** = 0 | The base direction is detected automatically from the text content (default). |
| **TEXT_DIRECTION_LTR** = 1 | The text is laid out with the left-to-right base direction. |
| **TEXT_DIRECTION_RTL** = 2 | The text is laid out with the right-to-left base direction. |

### Properties

## 🔒︎ int NumChildren

The number of widgets in the GUI.
## int MouseGrab

The value indicating if the mouse pointer is bound to the GUI.
## int MouseCursor

The mouse cursor value, one of the *CURSOR_** pre-defined variables.
## WidgetSprite MouseSprite

The custom mouse pointer currently in use.
## bool MouseEnabled

The value indicating if the mouse cursor is rendered.
## float ToolTipTime

The delay before tooltip appearing.
## float ToolTipAlpha

The alpha value of a tooltip.
## vec4 ToolTipColor

The font color of a tooltip.
## int ToolTipWidth

The width of the tooltip.
## int ToolTipSize

The font size of a tooltip.
## bool ToolTipEnabled

The value indicating if tooltips are available.
## float TransparentAlpha

The alpha value of a transparent widget. A widget is transparent, if it uses blending.
## vec4 TransparentColor

The font color of a transparent widget. A widget is transparent, if it uses blending.
## bool TransparentEnabled

The value indicating if a widget can be rendered as [transparent](../../../code/gui/rc.md#transparent) (i.e. change its color accordingly), when necessary. For example, it can indicate whether the drop-down list of combobox is transparent or not.
## float DisabledAlpha

The alpha value of a disabled widget.
## vec4 DisabledColor

The font color of a disabled widget.
## bool DisabledEnabled

The value indicating if a widget can be rendered as [disabled](../../../code/gui/rc.md#disabled) (i.e. change its color accordingly), when necessary.
## float FocusedAlpha

The alpha value of a focused widget.
## vec4 FocusedColor

The font color of a focused widget.
## bool FocusedPermanent

The value indicating if the permanent color of the focused widget is changed.
## bool FocusedEnabled

The value indicating if a widget can be rendered as [focused](../../../code/gui/rc.md#focused) on (i.e. change its color accordingly), when necessary.
## float DefaultAlpha

The standard alpha value of a widget.
## vec4 DefaultColor

The standard font color of a widget.
## int DefaultSize

The standard font size of a widget.
## float FadeOutSpeed

The duration of fade-out animation played when a widget loses focus.
## float FadeInSpeed

The duration of fade-in animation played when a widget gets focused.
## float ExposeSpeed

The duration of animation played when a widget appears.
## mat4 Transform

The global GUI transformation matrix. This 2D matrix can be tilted, rotated, moved or modified in many ways in 3D space.
## vec4 Color

The color of the global color multiplier.
## 🔒︎ int Height

The screen height.
## 🔒︎ int Width

The screen width.
## bool Hidden

The value indicating if the GUI is hidden (not rendered).
## bool Enabled

The value indicating if the GUI is enabled.
## 🔒︎ bool IsActive

The value indicating if any widget in the GUI is in focus.
## 🔒︎ WidgetVBox VBox

The root widget of the GUI (a [WidgetVBox](../../../api/library/gui/class.widgetvbox_cs.md)).
## 🔒︎ Widget PermanentFocus

The widget that is always in focus.
## 🔒︎ Widget OverlappedFocus

The widget placed under the currently focused widget.
## 🔒︎ Widget Focus

The widget that is currently in focus.
## 🔒︎ int MouseDY

The difference between the previous position of the mouse pointer and the current one along the Y axis in [logical units](../../../principles/dpi/index.md).
## 🔒︎ int MouseDX

The difference between the previous position of the mouse pointer and the current one along the X axis in [logical units](../../../principles/dpi/index.md).
## 🔒︎ int MouseY

The Y coordinate of the mouse pointer in the coordinate system of the application window in [logical units](../../../principles/dpi/index.md).
## 🔒︎ int MouseX

The X coordinate of the mouse pointer in the coordinate system of the application window in [logical units](../../../principles/dpi/index.md).
## int ToolTipY

The tooltip position along the Y axis.
## int ToolTipX

The tooltip position along the X axis.
## string ToolTipText

The GUI tooltip text.
## 🔒︎ bool IsUnderCursor

The value indicating if the GUI object is under cursor.
## 🔒︎ int MouseWheelHorizontal

The horizontal mouse scroll value.
## 🔒︎ int MouseWheel

The mouse scroll value. Negative values correspond to scrolling downwards; positive values correspond to scrolling upwards; the value is zero when the mouse wheel is not scrolled.
## bool MouseShow

The value indicating if the OS mouse pointer is displayed, or if the application cursor is used only.
## int MouseButtons

The mouse buttons the input of which is received.
## bool WorldObject

The value indicating if the GUI object is available in the hierarchy and rendered as a world object, or if it should have the window handle.
## ulong WinHandle

The engine handle of the window.
## ivec2 Position

The GUI object position (top left corner) in screen coordinates.
## ivec2 Size

The GUI object size in [logical units](../../../principles/dpi/index.md).
## float DpiScale

The DPI scale applied to the GUI.
## 🔒︎ Event EventUpdate

The event triggered when GUI is updated. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the Update event handler
void update_event_handler()
{
	Log.Message("\Handling Update event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections update_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventUpdate.Connect(update_event_connections, update_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventUpdate.Connect(update_event_connections, () => {
		Log.Message("Handling Update event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
update_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the Update event with a handler function
publisher.EventUpdate.Connect(update_event_handler);

// remove subscription to the Update event later by the handler function
publisher.EventUpdate.Disconnect(update_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection update_event_connection;

// subscribe to the Update event with a lambda handler function and keeping the connection
update_event_connection = publisher.EventUpdate.Connect(() => {
		Log.Message("Handling Update event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
update_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
update_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
update_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring Update events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventUpdate.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventUpdate.Enabled = true;

```

</details>

## Gui.CursorMode GlobalCursorMode

The default cursor movement mode applied to all text edit widgets of this GUI whose own *CursorMode* property is set to *CURSOR_MODE_AUTO*. Reading this property never returns *CURSOR_MODE_AUTO*: it resolves to *CURSOR_MODE_LOGICAL* (the effective default).
## Gui.TextDirection GlobalTextDirection

The default base text direction applied to all widgets of this GUI whose own *TextDirection* property is set to *TEXT_DIRECTION_AUTO*. The default value is *TEXT_DIRECTION_AUTO* (the direction is detected from the text content).
### Members

---

## Gui GetCurrent ( )

Returns the current GUI instance.
### Return value

Current GUI instance.
## Widget GetChild ( int num )

Returns a child widget with a given number.
### Arguments

- *int* **num** - Widget number.

### Return value

Child widget.
## int IsChild ( Widget widget )

Checks if a given widget belongs to the GUI.
### Arguments

- *[Widget](../../../api/library/gui/class.widget_cs.md)* **widget** - Widget to check.

### Return value

true if the widget belongs to the GUI; otherwise, false.
## int GetKeyActivity ( uint key )

Checks if a given key already has a special purpose for the widget in focus.
### Arguments

- *uint* **key** - One of the standard ASCII control codes or one of the *[KEY_*](../../../api/library/controls/class.input_cs.md#KEY_UNKNOWN)* pre-defined variables.

### Return value

**1** if the key cannot be used; otherwise, **0**.
## bool SetResource ( string name )

Changes the resource skin file used in the system GUI.
### Arguments

- *string* **name** - Path to the [*.rc](../../../code/gui/rc.md) file.

### Return value

true if the resource file is successfully changed; otherwise, false.
## void SetToolTip ( int x , int y , string str )

Sets a tooltip.
### Arguments

- *int* **x** - Screen position along the X axis.
- *int* **y** - Screen position along the Y axis.
- *string* **str** - Tooltip to display.

## int GetToolTipHeight ( string str )

Returns a height of the given tooltip.
> **Notice:** Height of a single-line tooltip is equal to 21 pixels.


### Arguments

- *string* **str** - A tooltip text.

### Return value

Height of the given tooltip (in pixels).
## int GetToolTipWidth ( string str )

Returns the current width of the tooltip.
### Arguments

- *string* **str** - A tooltip text.

### Return value

Width of the tooltip.
## void AddChild ( Widget widget , int flags = 0 )

Adds a given widget to the GUI.
### Arguments

- *[Widget](../../../api/library/gui/class.widget_cs.md)* **widget** - Widget to add.
- *int* **flags** - One of the *GUI_ALIGN_** pre-defined variables. This is an optional parameter.

## bool AddDictionary ( string name , string language = 0 )

Adds a new dictionary with localized interface strings. Dictionaries cannot be modified in run-time.
### Arguments

- *string* **name** - Path to the dictionary file.
- *string* **language** - Name of the dictionary language.

### Return value

Returns **1** if the dictionary is added successfully; otherwise, **0**.
## void ClearDictionaries ( )

Clears all dictionaries.
## bool ClearTexture ( string name )

Clears the specified GUI texture file cache.
### Arguments

- *string* **name** - Name of the texture.

### Return value

1 if the texture is successfully cleared; otherwise, 0.
## Gui create ( string name = 0 )

GUI constructor.
### Arguments

- *string* **name** - GUI skin name.

### Return value

Pointer to the created GUI.
## void Destroy ( )

Destroys all GUI resources.
## void Disable ( )

Disables GUI rendering.
## void Enable ( )

Enables GUI rendering.
## bool HasTranslation ( string arg1 )

Returns a value indicating if there is translation for a given string in the localization dictionary.
### Arguments

- *string* **arg1** - String to check.

### Return value

true if there is translation for the given string; otherwise, false.
## vec4 ParseColor ( string str )

Converts a color string in the Web format (RRGGBB / #RRGGBB or RRGGBBAA / #RRGGBBAA) into its *vec4* equivalent.
### Arguments

- *string* **str** - Color string in the Web format.

### Return value

Color value as a *vec4* vector (R, G, B, A).
## void RemoveChild ( Widget widget )

Removes the specified widget from the GUI.
### Arguments

- *[Widget](../../../api/library/gui/class.widget_cs.md)* **widget** - Child widget to be removed.

## void RemoveFocus ( )

Removes focus from the GUI.
## void ReplaceChild ( Widget widget , Widget old_widget , int flags = 0 )

Replaces a given widget in the GUI with another widget.
### Arguments

- *[Widget](../../../api/library/gui/class.widget_cs.md)* **widget** - Replacement widget.
- *[Widget](../../../api/library/gui/class.widget_cs.md)* **old_widget** - Widget to be replaced.
- *int* **flags** - One of the *GUI_ALIGN_** pre-defined variables. This is an optional parameter.

## bool SaveDictionary ( string name , string language = 0 )

Saves the current dictionary on disk. This function can be used to save the currently loaded dictionary into another file.
### Arguments

- *string* **name** - Path to a dictionary file.
- *string* **language** - Name of the dictionary language.

### Return value

true if the dictionary is saved successfully; otherwise, false.
## string Translate ( string str )

Returns the source string translated using the dictionary.
### Arguments

- *string* **str** - String to translate (source).

### Return value

Target (translated) string if it is found in the localization dictionary; otherwise, the source string.
## void Update ( )

Updates GUI.
## void PreRender ( )

Method executed after the *update()* and before the *render()* function. This method is used to make necessary preparations for rendering (e.g. prepare a texture) after the *update()* and is called automatically for *[WidgetSpriteViewport](../../../api/library/gui/class.widgetspriteviewport_cs.md)* and *[WidgetSpriteNode](../../../api/library/gui/class.widgetspriteviewport_cs.md)* to ensure proper rendering of the widgets during *render()*. In case you implement a custom GUI or widgets using the *[WidgetExtern](../../../api/library/gui/class.widgetextern_cs.md)* class you should put all such rendering preparations to **[WidgetExternBase.PreRender()](../../../api/library/gui/class.widgetexternbase_cs.md#preRender_void)** and call *preRender()* for GUI manually after *update()*.
## void Render ( )

Renders the GUI.
## void Render ( int custom_mouse_buttons )

Renders the GUI.
### Arguments

- *int* **custom_mouse_buttons** - Pressed mouse button.

## void UpdateHierarchy ( )

Updates the hierarchy for all widgets � the widgets are arranged, expanded to the required sizes and then their positions are updated. Updating the hierarchy may be required, for example, for getting the screen position immediately after the widget has been added to the hierarchy.
## bool IsRenderingBootScreen ( )

Returns a value indicating if the GUI currently renders the [boot screen](../../../code/gui/screens/index.md#boot).
### Return value

true if the GUI currently renders the [boot screen](../../../code/gui/screens/index.md#boot); otherwise, false.
## bool IsRenderingSplashScreen ( )

Returns a value indicating if the GUI currently renders the [splash screen](../../../code/gui/screens/index.md#splash).
### Return value

true if the GUI currently renders the [splash screen](../../../code/gui/screens/index.md#splash); otherwise, false.
## bool IsRenderingLoadingScreen ( )

Returns a value indicating if the GUI currently renders the [loading screen](../../../code/gui/screens/index.md#loading).
### Return value

true if the GUI currently renders the [loading screen](../../../code/gui/screens/index.md#loading); otherwise, false.
## void FocusGained ( )

The focus is set on the GUI object.
## void FocusLost ( )

The focus is removed from the GUI.
## bool IsHover ( int global_pos_x , int global_pos_y )

Returns a value indicating if the cursor is hovering over the GUI object.
### Arguments

- *int* **global_pos_x** - The X coordinate of the cursor in global coordinates.
- *int* **global_pos_y** - The Y coordinate of the cursor in global coordinates.

### Return value

true if the cursor is hovering over the GUI object; otherwise, false.
## Widget GetWidgetIntersection ( int global_pos_x , int global_pos_y )

Returns the intersected widget that is visually perceptible (not empty, not transparent).
### Arguments

- *int* **global_pos_x** - The X coordinate of the [cursor in global coordinates](../../../api/library/controls/class.input_cs.md#getMousePosition_ivec2).
- *int* **global_pos_y** - The Y coordinate of the [cursor in global coordinates](../../../api/library/controls/class.input_cs.md#getMousePosition_ivec2).

### Return value

The intersected widget that is visually perceptible.
## Widget GetUnderCursorWidget ( )

Returns the visually perceptible widget, over which the cursor is currently hovering.
### Return value

The widget, over which the cursor is currently hovering.
## Gui GetFocusGui ( )

Returns the GUI object that is currently in focus.
### Return value

The GUI object currently in focus.
## Gui GetGuiIntersection ( int global_pos_x , int global_pos_y )

Returns the intersected GUI object.
> **Notice:** This method takes Z-ordering into consideration: if the GUI object is overlapped by any other window, the method returns null.

### Arguments

- *int* **global_pos_x** - The X coordinate of the intersection point in global coordinates.
- *int* **global_pos_y** - The Y coordinate of the intersection point in global coordinates.

### Return value

The intersected GUI object.
## Gui GetUnderCursorGui ( )

Returns the GUI object that is currently under cursor.
> **Notice:** If case of dragging or resizing a window, this method returns null. To receive the intersected GUI in such a case, use [getGuiIntersection()](#getGuiIntersection_int_int_Gui).

### Return value

GUI object currently under cursor.
## void GetWorldGuiInstances ( Gui [] OUT_ret_instances )

Returns all GUI instances that are available in the scene hierarchy and rendered as world objects.
### Arguments

- *[Gui](../../../api/library/gui/class.gui_cs.md)[]* **OUT_ret_instances** - All GUI instances that are available in the scene hierarchy and rendered as world objects. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## int GetAndClearMouseWheel ( )

Returns the mouse scroll value and clears the mouse scroll state info.
### Return value

The mouse scroll value in the [-1;1] range.
## void ForceSetMouseWheel ( int value )

Sets the mouse scroll value.
### Arguments

- *int* **value** - The mouse scroll value in the [-1;1] range.

## int GetAndClearMouseWheelHorizontal ( )

Returns the mouse horizontal scroll value and clears the mouse scroll state info.
### Return value

The horizontal mouse scroll value in the [-1;1] range.
## void ForceSetMouseWheelHorizontal ( int value )

Sets the mouse vertical scroll value.
### Arguments

- *int* **value** - The horizontal mouse scroll value in the [-1;1] range.

## bool GetKey ( Input.KEY key )

Returns the value indicating if the specified key is pressed.
### Arguments

- *[Input.KEY](../../../api/library/controls/class.input_cs.md#KEY)* **key** - One of the standard ASCII control codes or one of the *[KEY_*](../../../api/library/controls/class.input_cs.md#KEY_UNKNOWN)* pre-defined variables.

### Return value

true if the key is pressed; otherwise, false.
## bool GetAndClearKey ( Input.KEY key )

Returns the value indicating if the specified key is pressed and clears the key state info.
### Arguments

- *[Input.KEY](../../../api/library/controls/class.input_cs.md#KEY)* **key** - One of the standard ASCII control codes or one of the *[KEY_*](../../../api/library/controls/class.input_cs.md#KEY_UNKNOWN)* pre-defined variables.

### Return value

true if the key is pressed; otherwise, false.
## int ToRenderSize ( int unit_size )

Transforms the unit value to the pixel value.
### Arguments

- *int* **unit_size** - Size in units.

### Return value

Size in pixels.
## int ToUnitSize ( int render_size )

Transforms the pixel value to the unit value.
### Arguments

- *int* **render_size** - Size in pixels.

### Return value

Size in units.
## bool SetFontPath ( string path )

Changes the regular font used in the system GUI.
### Arguments

- *string* **path** - Path to the font file.

### Return value

true if the font is set successfully, otherwise false.
## string GetFontPath ( )

Returns the path to the regular font currently used in the system GUI.
### Return value

Path to the font file.
## bool SetFontPaths ( string normal_path , string bold_path , string italic_path , string bold_italic_path )

Changes the set of fonts � regular, bold, italic, and italic bold � used in the system GUI.
### Arguments

- *string* **normal_path** - Path to the regular font file.
- *string* **bold_path** - Path to the bold font file.
- *string* **italic_path** - Path to the italic font file.
- *string* **bold_italic_path** - Path to the bold italic font file.

### Return value

true if the fonts are set successfully, otherwise false.
## bool SetFontRichBoldPath ( string path )

Changes the bold font used in the system GUI.
### Arguments

- *string* **path** - Path to the bold font file.

### Return value

true if the fonts are set successfully, otherwise false.
## string GetFontRichBoldPath ( )

Returns the path to the bold font currently used in the system GUI.
### Return value

Path to the bold font file.
## bool SetFontRichItalicPath ( string path )

Changes the italic font used in the system GUI.
### Arguments

- *string* **path** - Path to the italic font file.

### Return value

true if the font is set successfully, otherwise false.
## string GetFontRichItalicPath ( )

Returns the path to the italic font currently used in the system GUI.
### Return value

Path to the italic font file.
## bool SetFontRichBoldItalicPath ( string path )

Changes the bold italic font used in the system GUI.
### Arguments

- *string* **path** - Path to the bold italic font file.

### Return value

true if the font is set successfully, otherwise false.
## string GetFontRichBoldItalicPath ( )

Returns the path to the bold italic font currently used in the system GUI.
### Return value

Path to the bold italic font file.
## bool SetSkinPath ( string path )

Changes the GUI skin used in the system GUI.
### Arguments

- *string* **path** - Path to the directory where the skin files (an [RC file](../../../code/gui/rc.md) and textures) are stored.

### Return value

true if the skin is set successfully, otherwise false.
## string GetSkinPath ( )

Returns the path to the current GUI skin.
### Return value

Path to the directory where the skin files (an [RC file](../../../code/gui/rc.md) and textures) are stored.
## void SetGlobalFontFallback ( string[] fallbacks )

Sets the global list of fallback fonts. When a character is not found in the current font, the system searches these fonts in order. Global fallbacks apply to all fonts.
### Arguments

- *string[]* **fallbacks** - List of paths to fallback font files.

## void GetGlobalFontFallback ( string[] OUT_ret )

Returns the global list of fallback fonts.
### Arguments

- *string[]* **OUT_ret** - An array to store the paths to global fallback font files. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## void SetFontFallback ( string font , string[] fallbacks )

Sets the list of fallback fonts for a specific font. When a character is not found in the specified font, the system searches these fonts first, then the global fallbacks.
### Arguments

- *string* **font** - Path to the font file to set fallbacks for.
- *string[]* **fallbacks** - List of paths to fallback font files.

## void GetFontFallback ( string font , string[] OUT_ret )

Returns the list of fallback fonts for a specific font.
### Arguments

- *string* **font** - Path to the font file to get fallbacks for.
- *string[]* **OUT_ret** - An array to store the paths to fallback font files for the specified font. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.
