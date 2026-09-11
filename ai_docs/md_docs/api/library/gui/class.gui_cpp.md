# Unigine::Gui Class (CPP)

**Header:** #include <UnigineGui.h>


Creates a GUI. Different types of GUI widgets can be either added to one of the following:

- To the system GUI (Unigine user interface) that is rendered on top of application window.
- To the [GUI object](../../../api/library/objects/class.objectgui_cpp.md) positioned in the world. In this case, any postprocessing filter can be applied.

Default values returned by the following methods can be overridden via [RC files](../../../code/gui/rc.md) defining a custom GUI.
## Gui Class

### Enums

## CursorMode

Cursor movement and hit-test mode for text edit widgets, relevant for bidirectional (mixed left-to-right and right-to-left) text.
| Name | Description |
|---|---|
| **CURSOR_MODE_AUTO** = 0 | On a widget, the mode is inherited from the **[getGlobalCursorMode()](../../...md#getGlobalCursorMode_int)** property of the *Gui*; on the *Gui* itself, this value is treated as *CURSOR_MODE_LOGICAL*. |
| **CURSOR_MODE_VISUAL** = 1 | The cursor moves over glyphs in on-screen (visual) order: arrow keys move the caret in the pressed direction even across boundaries between left-to-right and right-to-left text runs. |
| **CURSOR_MODE_LOGICAL** = 2 | The cursor moves through the underlying character sequence in logical (storage) order. |

## TextDirection

Base paragraph direction used for laying out widget text with bidirectional content.
| Name | Description |
|---|---|
| **TEXT_DIRECTION_AUTO** = 0 | The base direction is detected automatically from the text content (default). |
| **TEXT_DIRECTION_LTR** = 1 | The text is laid out with the left-to-right base direction. |
| **TEXT_DIRECTION_RTL** = 2 | The text is laid out with the right-to-left base direction. |

### Members

## int getNumChildren () const

Returns the current number of widgets in the GUI.
### Return value

Current number of widgets in the GUI.
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
## void setMouseSprite ( const Ptr < WidgetSprite >& sprite )

Sets a new custom mouse pointer currently in use.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[WidgetSprite](../../../api/library/gui/class.widgetsprite_cpp.md)>&* **sprite** - The sprite with a custom mouse pointer, or NULL if the standard mouse pointer is used.

## Ptr < WidgetSprite > getMouseSprite () const

Returns the current custom mouse pointer currently in use.
### Return value

Current sprite with a custom mouse pointer, or NULL if the standard mouse pointer is used.
## void setMouseEnabled ( bool enabled )

Sets a new value indicating if the mouse cursor is rendered.
### Arguments

- *bool* **enabled** - Set **true** to enable rendering of the mouse cursor; **false** - to disable it.

## bool isMouseEnabled () const

Returns the current value indicating if the mouse cursor is rendered.
### Return value

**true** if rendering of the mouse cursor is enabled ; otherwise **false**.
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
## void setToolTipColor ( const Math:: vec4 & color )

Sets a new font color of a tooltip.
### Arguments

- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md)&* **color** - The font color of a tooltip. The default is equivalent to **#000000** (black).

## Math:: vec4 getToolTipColor () const

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
## void setToolTipEnabled ( bool enabled )

Sets a new value indicating if tooltips are available.
### Arguments

- *bool* **enabled** - Set **true** to enable tooltips display; **false** - to disable it.

## bool isToolTipEnabled () const

Returns the current value indicating if tooltips are available.
### Return value

**true** if tooltips display is enabled ; otherwise **false**.
## void setTransparentAlpha ( float alpha )

Sets a new alpha value of a transparent widget. A widget is transparent, if it uses blending.
### Arguments

- *float* **alpha** - The alpha value of a transparent widget. **0** means completely transparent.

## float getTransparentAlpha () const

Returns the current alpha value of a transparent widget. A widget is transparent, if it uses blending.
### Return value

Current alpha value of a transparent widget. **0** means completely transparent.
## void setTransparentColor ( const Math:: vec4 & color )

Sets a new font color of a transparent widget. A widget is transparent, if it uses blending.
### Arguments

- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md)&* **color** - The font color of a transparent widget. The default is equivalent to **#869caa** (light bluish).

## Math:: vec4 getTransparentColor () const

Returns the current font color of a transparent widget. A widget is transparent, if it uses blending.
### Return value

Current font color of a transparent widget. The default is equivalent to **#869caa** (light bluish).
## void setTransparentEnabled ( bool enabled )

Sets a new value indicating if a widget can be rendered as [transparent](../../../code/gui/rc.md#transparent) (i.e. change its color accordingly), when necessary. For example, it can indicate whether the drop-down list of combobox is transparent or not.
### Arguments

- *bool* **enabled** - Set **true** to enable rendering of a widget as transparent; **false** - to disable it.

## bool isTransparentEnabled () const

Returns the current value indicating if a widget can be rendered as [transparent](../../../code/gui/rc.md#transparent) (i.e. change its color accordingly), when necessary. For example, it can indicate whether the drop-down list of combobox is transparent or not.
### Return value

**true** if rendering of a widget as transparent is enabled ; otherwise **false**.
## void setDisabledAlpha ( float alpha )

Sets a new alpha value of a disabled widget.
### Arguments

- *float* **alpha** - The alpha value of a disabled widget. **0** means completely transparent.

## float getDisabledAlpha () const

Returns the current alpha value of a disabled widget.
### Return value

Current alpha value of a disabled widget. **0** means completely transparent.
## void setDisabledColor ( const Math:: vec4 & color )

Sets a new font color of a disabled widget.
### Arguments

- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md)&* **color** - The font color of a disabled widget. The default is equivalent to **#869caa** (light bluish).

## Math:: vec4 getDisabledColor () const

Returns the current font color of a disabled widget.
### Return value

Current font color of a disabled widget. The default is equivalent to **#869caa** (light bluish).
## void setDisabledEnabled ( bool enabled )

Sets a new value indicating if a widget can be rendered as [disabled](../../../code/gui/rc.md#disabled) (i.e. change its color accordingly), when necessary.
### Arguments

- *bool* **enabled** - Set **true** to enable rendering of a widget as disabled; **false** - to disable it.

## bool isDisabledEnabled () const

Returns the current value indicating if a widget can be rendered as [disabled](../../../code/gui/rc.md#disabled) (i.e. change its color accordingly), when necessary.
### Return value

**true** if rendering of a widget as disabled is enabled ; otherwise **false**.
## void setFocusedAlpha ( float alpha )

Sets a new alpha value of a focused widget.
### Arguments

- *float* **alpha** - The alpha value of a focused widget. **0** means completely transparent.

## float getFocusedAlpha () const

Returns the current alpha value of a focused widget.
### Return value

Current alpha value of a focused widget. **0** means completely transparent.
## void setFocusedColor ( const Math:: vec4 & color )

Sets a new font color of a focused widget.
### Arguments

- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md)&* **color** - The font color of a focused widget. The default is equivalent to **#ffffff** (white).

## Math:: vec4 getFocusedColor () const

Returns the current font color of a focused widget.
### Return value

Current font color of a focused widget. The default is equivalent to **#ffffff** (white).
## void setFocusedPermanent ( bool permanent )

Sets a new value indicating if the permanent color of the focused widget is changed.
### Arguments

- *bool* **permanent** - Set **true** to enable change of the permanent color of the focused widget; **false** - to disable it.

## bool isFocusedPermanent () const

Returns the current value indicating if the permanent color of the focused widget is changed.
### Return value

**true** if change of the permanent color of the focused widget is enabled ; otherwise **false**.
## void setFocusedEnabled ( bool enabled )

Sets a new value indicating if a widget can be rendered as [focused](../../../code/gui/rc.md#focused) on (i.e. change its color accordingly), when necessary.
### Arguments

- *bool* **enabled** - Set **true** to enable rendering of a widget as focused on; **false** - to disable it.

## bool isFocusedEnabled () const

Returns the current value indicating if a widget can be rendered as [focused](../../../code/gui/rc.md#focused) on (i.e. change its color accordingly), when necessary.
### Return value

**true** if rendering of a widget as focused on is enabled ; otherwise **false**.
## void setDefaultAlpha ( float alpha )

Sets a new standard alpha value of a widget.
### Arguments

- *float* **alpha** - The standard alpha value of a widget. **0** means completely transparent.

## float getDefaultAlpha () const

Returns the current standard alpha value of a widget.
### Return value

Current standard alpha value of a widget. **0** means completely transparent.
## void setDefaultColor ( const Math:: vec4 & color )

Sets a new standard font color of a widget.
### Arguments

- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md)&* **color** - The standard font color of a widget. The default is equivalent to **#ddddff** (blue-white).

## Math:: vec4 getDefaultColor () const

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
## void setTransform ( const Math:: mat4 & transform )

Sets a new global GUI transformation matrix. This 2D matrix can be tilted, rotated, moved or modified in many ways in 3D space.
### Arguments

- *const  Math::[mat4](../../../api/library/math/class.mat4_cpp.md)&* **transform** - The global GUI transformation matrix.

## Math:: mat4 getTransform () const

Returns the current global GUI transformation matrix. This 2D matrix can be tilted, rotated, moved or modified in many ways in 3D space.
### Return value

Current global GUI transformation matrix.
## void setColor ( const Math:: vec4 & color )

Sets a new color of the global color multiplier.
### Arguments

- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md)&* **color** - The color of the global color multiplier. The default is equivalent to #ffffff (white).

## Math:: vec4 getColor () const

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
## void setHidden ( bool hidden )

Sets a new value indicating if the GUI is hidden (not rendered).
### Arguments

- *bool* **hidden** - true if the GUI is hidden, false if it is shown

## bool isHidden () const

Returns the current value indicating if the GUI is hidden (not rendered).
### Return value

true if the GUI is hidden, false if it is shown
## void setEnabled ( bool enabled )

Sets a new value indicating if the GUI is enabled.
### Arguments

- *bool* **enabled** - Set **true** to enable the GUI; **false** - to disable it.

## bool isEnabled () const

Returns the current value indicating if the GUI is enabled.
### Return value

**true** if the GUI is enabled ; otherwise **false**.
## bool isActive () const

Returns the current value indicating if any widget in the GUI is in focus.
### Return value

**true** if any widget in the GUI is in focus; otherwise **false**.
## Ptr < WidgetVBox > getVBox () const

Returns the current root widget of the GUI (a [WidgetVBox](../../../api/library/gui/class.widgetvbox_cpp.md)).
### Return value

Current root widget of the GUI.
## Ptr < Widget > getPermanentFocus () const

Returns the current widget that is always in focus.
### Return value

Current widget that is always in focus.
## Ptr < Widget > getOverlappedFocus () const

Returns the current widget placed under the currently focused widget.
### Return value

Current overlapped widget.
## Ptr < Widget > getFocus () const

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

Sets a new tooltip position along the Y axis.
### Arguments

- *int* **y** - The tooltip position along the Y axis.

## int getToolTipY () const

Returns the current tooltip position along the Y axis.
### Return value

Current tooltip position along the Y axis.
## void setToolTipX ( int x )

Sets a new tooltip position along the X axis.
### Arguments

- *int* **x** - The tooltip position along the X axis.

## int getToolTipX () const

Returns the current tooltip position along the X axis.
### Return value

Current tooltip position along the X axis.
## void setToolTipText ( const char * text )

Sets a new GUI tooltip text.
### Arguments

- *const char ** **text** - The GUI tooltip text.

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

- *int* **buttons** - The *[Input::MOUSE_BUTTON_LEFT](../../../api/library/controls/class.input_cpp.md#MOUSE_BUTTON_LEFT)* or *[Input::MOUSE_BUTTON_RIGHT](../../../api/library/controls/class.input_cpp.md#MOUSE_BUTTON_RIGHT)*, or *[Input::MOUSE_BUTTON_MIDDLE](../../../api/library/controls/class.input_cpp.md#MOUSE_BUTTON_MIDDLE)*.

## int getMouseButtons () const

Returns the current mouse buttons the input of which is received.
### Return value

Current *[Input::MOUSE_BUTTON_LEFT](../../../api/library/controls/class.input_cpp.md#MOUSE_BUTTON_LEFT)* or *[Input::MOUSE_BUTTON_RIGHT](../../../api/library/controls/class.input_cpp.md#MOUSE_BUTTON_RIGHT)*, or *[Input::MOUSE_BUTTON_MIDDLE](../../../api/library/controls/class.input_cpp.md#MOUSE_BUTTON_MIDDLE)*.
## void setWorldObject ( bool object )

Sets a new value indicating if the GUI object is available in the hierarchy and rendered as a world object, or if it should have the window handle.
### Arguments

- *bool* **object** - Set **true** to enable the GUI object is available in the hierarchy and rendered as a world object; **false** - to disable it.

## bool isWorldObject () const

Returns the current value indicating if the GUI object is available in the hierarchy and rendered as a world object, or if it should have the window handle.
### Return value

**true** if the GUI object is available in the hierarchy and rendered as a world object; otherwise **false**.
## void setWinHandle ( unsigned long long handle )

Sets a new engine handle of the window.
### Arguments

- *unsigned long long* **handle** - The window handle.

## unsigned long long getWinHandle () const

Returns the current engine handle of the window.
### Return value

Current window handle.
## void setPosition ( const Math:: ivec2 & position )

Sets a new GUI object position (top left corner) in screen coordinates.
### Arguments

- *const  Math::[ivec2](../../../api/library/math/class.ivec2_cpp.md)&* **position** - The GUI object position (top left corner) in screen coordinates.

## Math:: ivec2 getPosition () const

Returns the current GUI object position (top left corner) in screen coordinates.
### Return value

Current GUI object position (top left corner) in screen coordinates.
## void setSize ( const Math:: ivec2 & size )

Sets a new GUI object size in [logical units](../../../principles/dpi/index.md).
### Arguments

- *const  Math::[ivec2](../../../api/library/math/class.ivec2_cpp.md)&* **size** - The GUI object size (width and height) in [logical units](../../../principles/dpi/index.md).

## Math:: ivec2 getSize () const

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
## Event<> getEventUpdate () const

event triggered when GUI is updated. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the Update event handler
void update_event_handler()
{
	Log::message("\Handling Update event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections update_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventUpdate().connect(update_event_connections, update_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventUpdate().connect(update_event_connections, []() {
		Log::message("\Handling Update event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
update_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection update_event_connection;

// subscribe to the Update event with a handler function keeping the connection
publisher->getEventUpdate().connect(update_event_connection, update_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
update_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
update_event_connection.setEnabled(true);

// ...

// remove subscription to the Update event via the connection
update_event_connection.disconnect();

//////////////////////////////////////////////////////////////////////////////
//  3. You can add EventConnection/EventConnections instance as a member of the
//  class that handles the event. In this case all linked subscriptions will be
//  automatically removed when class destructor is called
//////////////////////////////////////////////////////////////////////////////

// Class handling the event
class SomeClass
{
public:
	// instance of the EventConnections class as a class member
	EventConnections e_connections;

	// A Update event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling Update event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventUpdate().connect(sc->e_connections, sc, &SomeClass::event_handler);

// ...

// handler class instance is deleted with all its subscriptions removed automatically
delete sc;

//////////////////////////////////////////////////////////////////////////////
//   4. Subscribe to an event saving a particular connection ID
//   and unsubscribe later by this ID
//////////////////////////////////////////////////////////////////////////////
// instance of the EventConnections class to manage event connections
EventConnections e_connections;

// define a particular connection ID to be used to unsubscribe later
EventConnectionId update_handler_id;

// subscribe to the Update event with a lambda handler function and keeping connection ID
update_handler_id = publisher->getEventUpdate().connect(e_connections, []() {
		Log::message("\Handling Update event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventUpdate().disconnect(update_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all Update events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventUpdate().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventUpdate().setEnabled(true);

```

</details>

### Return value

Event instance.
## void setGlobalCursorMode ( Gui::CursorMode mode )

Sets a new default cursor movement mode applied to all text edit widgets of this GUI whose own *CursorMode* property is set to *CURSOR_MODE_AUTO*. Reading this property never returns *CURSOR_MODE_AUTO*: it resolves to *CURSOR_MODE_LOGICAL* (the effective default).
### Arguments

- *[Gui::CursorMode](../../../api/library/gui/class.gui_cpp.md#CursorMode)* **mode** - The default cursor mode for text edit widgets

## Gui::CursorMode getGlobalCursorMode () const

Returns the current default cursor movement mode applied to all text edit widgets of this GUI whose own *CursorMode* property is set to *CURSOR_MODE_AUTO*. Reading this property never returns *CURSOR_MODE_AUTO*: it resolves to *CURSOR_MODE_LOGICAL* (the effective default).
### Return value

Current default cursor mode for text edit widgets
## void setGlobalTextDirection ( Gui::TextDirection direction )

Sets a new default base text direction applied to all widgets of this GUI whose own *TextDirection* property is set to *TEXT_DIRECTION_AUTO*. The default value is *TEXT_DIRECTION_AUTO* (the direction is detected from the text content).
### Arguments

- *[Gui::TextDirection](../../../api/library/gui/class.gui_cpp.md#TextDirection)* **direction** - The default base text direction for widgets

## Gui::TextDirection getGlobalTextDirection () const

Returns the current default base text direction applied to all widgets of this GUI whose own *TextDirection* property is set to *TEXT_DIRECTION_AUTO*. The default value is *TEXT_DIRECTION_AUTO* (the direction is detected from the text content).
### Return value

Current default base text direction for widgets
---

## Ptr < Gui > getCurrent ( )

Returns the current GUI instance.
### Return value

Current GUI instance.
## Ptr < Widget > getChild ( int num ) const

Returns a child widget with a given number.
### Arguments

- *int* **num** - Child widget number.

### Return value

Child widget.
## int isChild ( const Ptr < Widget > & widget ) const

Checks if a given widget belongs to the GUI.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Widget](../../../api/library/gui/class.widget_cpp.md)> &* **widget** - Widget to check.

### Return value

true if the widget belongs to the GUI; otherwise, false.
## int getKeyActivity ( unsigned int key ) const

Checks if a given key already has a special purpose for the widget in focus.
### Arguments

- *unsigned int* **key** - One of the standard ASCII control codes or one of the *[KEY_*](../../../api/library/controls/class.input_cpp.md#KEY_UNKNOWN)* pre-defined variables.

### Return value

**1** if the key cannot be used; otherwise, **0**.
## bool setResource ( const char * name )

Changes the resource skin file used in the system GUI.
### Arguments

- *const char ** **name** - Path to the rc file.

### Return value

true if the resource file is successfully changed; otherwise, false.
## void setToolTip ( int x , int y , const char * str )

Sets a tooltip.
### Arguments

- *int* **x** - X coordinate of the tooltip position.
- *int* **y** - Y coordinate of the tooltip position.
- *const char ** **str** - ToolTip text.

## int getToolTipHeight ( const char * str ) const

Returns a height of the given tooltip.
> **Notice:** Height of a single-line tooltip is equal to 21 pixels.


### Arguments

- *const char ** **str** - A tooltip text.

### Return value

Height of the given tooltip (in pixels).
## int getToolTipWidth ( const char * str ) const

Returns the current width of the tooltip.
### Arguments

- *const char ** **str** - A tooltip text.

### Return value

Width of the tooltip.
## void addChild ( const Ptr < Widget > & widget , int flags = 0 )

Adds a given widget to the GUI.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Widget](../../../api/library/gui/class.widget_cpp.md)> &* **widget** - Widget to add.
- *int* **flags** - One of the ALIGN_* pre-defined variables. This is an optional parameter.

## bool addDictionary ( const char * name , const char * language = 0 )

Adds a new dictionary with localized interface strings. Dictionaries cannot be modified in run-time.
### Arguments

- *const char ** **name** - Path to the dictionary file.
- *const char ** **language** - Name of the dictionary language.

### Return value

Returns **1** if the dictionary is added successfully; otherwise, **0**.
## void clearDictionaries ( )

Clears all dictionaries.
## bool clearTexture ( const char * name )

Clears the specified GUI texture file cache.
### Arguments

- *const char ** **name** - Texture name.

### Return value

1 if the texture is successfully cleared; otherwise, 0.
## Ptr&lt;Gui&gt; create ( const char * name = 0 )

GUI constructor.
### Arguments

- *const char ** **name** - GUI skin name.

### Return value

Pointer to the created GUI.
## void destroy ( )

Destroys all GUI resources.
## void disable ( )

Disables GUI rendering.
## void enable ( )

Enables GUI rendering.
## bool hasTranslation ( const char * arg1 ) const

Returns a value indicating if there is translation for a given string in the localization dictionary.
### Arguments

- *const char ** **arg1** - String to check.

### Return value

true if there is translation for the given string; otherwise, false.
## Math:: vec4 parseColor ( const char * str ) const

Converts a color string in the Web format (RRGGBB / #RRGGBB or RRGGBBAA / #RRGGBBAA) into its *vec4* equivalent.
### Arguments

- *const char ** **str** - Color string in the Web format.

### Return value

Color value as a *vec4* vector (R, G, B, A).
## void removeChild ( const Ptr < Widget > & widget )

Removes the specified widget from the GUI.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Widget](../../../api/library/gui/class.widget_cpp.md)> &* **widget** - Child widget to be removed.

## void removeFocus ( )

Removes focus from the GUI.
## void replaceChild ( const Ptr < Widget > & widget , const Ptr < Widget > & old_widget , int flags = 0 )

Replaces a given widget in the GUI with another widget.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Widget](../../../api/library/gui/class.widget_cpp.md)> &* **widget** - Replacement widget.
- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Widget](../../../api/library/gui/class.widget_cpp.md)> &* **old_widget** - Widget to be replaced.
- *int* **flags** - One of the *ALIGN_** pre-defined variables. This is an optional parameter.

## bool saveDictionary ( const char * name , const char * language = 0 )

Saves the current dictionary on disk. This function can be used to save the currently loaded dictionary into another file.
### Arguments

- *const char ** **name** - Name of the dictionary language.
- *const char ** **language** - Dictionary language name.

### Return value

true if the dictionary is saved successfully; otherwise, false.
## const char * translate ( const char * str )

Returns the source string translated using the dictionary.
### Arguments

- *const char ** **str** - String to translate (source).

### Return value

Target (translated) string if it is found in the localization dictionary; otherwise, the source string.
## void update ( )

Updates GUI.
## void preRender ( )

Method executed after the *update()* and before the *render()* function. This method is used to make necessary preparations for rendering (e.g. prepare a texture) after the *update()* and is called automatically for *[WidgetSpriteViewport](../../../api/library/gui/class.widgetspriteviewport_cpp.md)* and *[WidgetSpriteNode](../../../api/library/gui/class.widgetspriteviewport_cpp.md)* to ensure proper rendering of the widgets during *render()*. In case you implement a custom GUI or widgets using the *[WidgetExtern](../../../api/library/gui/class.widgetextern_cpp.md)* class you should put all such rendering preparations to **[WidgetExternBase::preRender()](../../../api/library/gui/class.widgetexternbase_cpp.md#preRender_void)** and call *preRender()* for GUI manually after *update()*.
## void render ( )

Renders the GUI.
## void render ( int custom_mouse_buttons )

Renders the GUI.
### Arguments

- *int* **custom_mouse_buttons** - Pressed mouse button.

## void updateHierarchy ( )

Updates the hierarchy for all widgets � the widgets are arranged, expanded to the required sizes and then their positions are updated. Updating the hierarchy may be required, for example, for getting the screen position immediately after the widget has been added to the hierarchy.
## bool isRenderingBootScreen ( )

Returns a value indicating if the GUI currently renders the [boot screen](../../../code/gui/screens/index.md#boot).
### Return value

true if the GUI currently renders the [boot screen](../../../code/gui/screens/index.md#boot); otherwise, false.
## bool isRenderingSplashScreen ( )

Returns a value indicating if the GUI currently renders the [splash screen](../../../code/gui/screens/index.md#splash).
### Return value

true if the GUI currently renders the [splash screen](../../../code/gui/screens/index.md#splash); otherwise, false.
## bool isRenderingLoadingScreen ( )

Returns a value indicating if the GUI currently renders the [loading screen](../../../code/gui/screens/index.md#loading).
### Return value

true if the GUI currently renders the [loading screen](../../../code/gui/screens/index.md#loading); otherwise, false.
## void focusGained ( )

The focus is set on the GUI object.
## void focusLost ( )

The focus is removed from the GUI.
## bool isHover ( int global_pos_x , int global_pos_y ) const

Returns a value indicating if the cursor is hovering over the GUI object.
### Arguments

- *int* **global_pos_x** - The X coordinate of the cursor in global coordinates.
- *int* **global_pos_y** - The Y coordinate of the cursor in global coordinates.

### Return value

true if the cursor is hovering over the GUI object; otherwise, false.
## Ptr < Widget > getWidgetIntersection ( int global_pos_x , int global_pos_y )

Returns the intersected widget that is visually perceptible (not empty, not transparent).
### Arguments

- *int* **global_pos_x** - The X coordinate of the [cursor in global coordinates](../../../api/library/controls/class.input_cpp.md#getMousePosition_ivec2).
- *int* **global_pos_y** - The Y coordinate of the [cursor in global coordinates](../../../api/library/controls/class.input_cpp.md#getMousePosition_ivec2).

### Return value

The intersected widget that is visually perceptible.
## Ptr < Widget > getUnderCursorWidget ( )

Returns the visually perceptible widget, over which the cursor is currently hovering.
### Return value

The widget, over which the cursor is currently hovering.
## Ptr < Gui > getFocusGui ( )

Returns the GUI object that is currently in focus.
### Return value

The GUI object currently in focus.
## Ptr < Gui > getGuiIntersection ( int global_pos_x , int global_pos_y )

Returns the intersected GUI object.
> **Notice:** This method takes Z-ordering into consideration: if the GUI object is overlapped by any other window, the method returns nullptr.

### Arguments

- *int* **global_pos_x** - The X coordinate of the intersection point in global coordinates.
- *int* **global_pos_y** - The Y coordinate of the intersection point in global coordinates.

### Return value

The intersected GUI object.
## Ptr < Gui > getUnderCursorGui ( )

Returns the GUI object that is currently under cursor.
> **Notice:** If case of dragging or resizing a window, this method returns nullptr. To receive the intersected GUI in such a case, use [getGuiIntersection()](#getGuiIntersection_int_int_Gui).

### Return value

GUI object currently under cursor.
## void getWorldGuiInstances ( Vector < Ptr < Gui >> & OUT_ret_instances )

Returns all GUI instances that are available in the scene hierarchy and rendered as world objects.
### Arguments

- *[Vector](../../../api/library/containers/vector/class.vector_cpp.md)<[Ptr](../../../api/library/common/class.ptr_cpp.md)<[Gui](../../../api/library/gui/class.gui_cpp.md)>> &* **OUT_ret_instances** - All GUI instances that are available in the scene hierarchy and rendered as world objects. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## int getAndClearMouseWheel ( )

Returns the mouse scroll value and clears the mouse scroll state info.
### Return value

The mouse scroll value in the [-1;1] range.
## void forceSetMouseWheel ( int value )

Sets the mouse scroll value.
### Arguments

- *int* **value** - The mouse scroll value in the [-1;1] range.

## int getAndClearMouseWheelHorizontal ( )

Returns the mouse horizontal scroll value and clears the mouse scroll state info.
### Return value

The horizontal mouse scroll value in the [-1;1] range.
## void forceSetMouseWheelHorizontal ( int value )

Sets the mouse vertical scroll value.
### Arguments

- *int* **value** - The horizontal mouse scroll value in the [-1;1] range.

## bool getKey ( Input::KEY key )

Returns the value indicating if the specified key is pressed.
### Arguments

- *[Input::KEY](../../../api/library/controls/class.input_cpp.md#KEY)* **key** - One of the standard ASCII control codes or one of the *[KEY_*](../../../api/library/controls/class.input_cpp.md#KEY_UNKNOWN)* pre-defined variables.

### Return value

true if the key is pressed; otherwise, false.
## bool getAndClearKey ( Input::KEY key )

Returns the value indicating if the specified key is pressed and clears the key state info.
### Arguments

- *[Input::KEY](../../../api/library/controls/class.input_cpp.md#KEY)* **key** - One of the standard ASCII control codes or one of the *[KEY_*](../../../api/library/controls/class.input_cpp.md#KEY_UNKNOWN)* pre-defined variables.

### Return value

true if the key is pressed; otherwise, false.
## int toRenderSize ( int unit_size ) const

Transforms the unit value to the pixel value.
### Arguments

- *int* **unit_size** - Size in units.

### Return value

Size in pixels.
## int toUnitSize ( int render_size ) const

Transforms the pixel value to the unit value.
### Arguments

- *int* **render_size** - Size in pixels.

### Return value

Size in units.
## bool setFontPath ( const char * path )

Changes the regular font used in the system GUI.
### Arguments

- *const char ** **path** - Path to the font file.

### Return value

true if the font is set successfully, otherwise false.
## const char * getFontPath ( ) const

Returns the path to the regular font currently used in the system GUI.
### Return value

Path to the font file.
## bool setFontPaths ( const char * normal_path , const char * bold_path , const char * italic_path , const char * bold_italic_path )

Changes the set of fonts � regular, bold, italic, and italic bold � used in the system GUI.
### Arguments

- *const char ** **normal_path** - Path to the regular font file.
- *const char ** **bold_path** - Path to the bold font file.
- *const char ** **italic_path** - Path to the italic font file.
- *const char ** **bold_italic_path** - Path to the bold italic font file.

### Return value

true if the fonts are set successfully, otherwise false.
## bool setFontRichBoldPath ( const char * path )

Changes the bold font used in the system GUI.
### Arguments

- *const char ** **path** - Path to the bold font file.

### Return value

true if the fonts are set successfully, otherwise false.
## const char * getFontRichBoldPath ( ) const

Returns the path to the bold font currently used in the system GUI.
### Return value

Path to the bold font file.
## bool setFontRichItalicPath ( const char * path )

Changes the italic font used in the system GUI.
### Arguments

- *const char ** **path** - Path to the italic font file.

### Return value

true if the font is set successfully, otherwise false.
## const char * getFontRichItalicPath ( ) const

Returns the path to the italic font currently used in the system GUI.
### Return value

Path to the italic font file.
## bool setFontRichBoldItalicPath ( const char * path )

Changes the bold italic font used in the system GUI.
### Arguments

- *const char ** **path** - Path to the bold italic font file.

### Return value

true if the font is set successfully, otherwise false.
## const char * getFontRichBoldItalicPath ( ) const

Returns the path to the bold italic font currently used in the system GUI.
### Return value

Path to the bold italic font file.
## bool setSkinPath ( const char * path )

Changes the GUI skin used in the system GUI.
### Arguments

- *const char ** **path** - Path to the directory where the skin files (an [RC file](../../../code/gui/rc.md) and textures) are stored.

### Return value

true if the skin is set successfully, otherwise false.
## const char * getSkinPath ( ) const

Returns the path to the current GUI skin.
### Return value

Path to the directory where the skin files (an [RC file](../../../code/gui/rc.md) and textures) are stored.
## Ptr < Gui > get ( )

Returns the pointer to the current GUI.
### Return value

Pointer to GUI.
## void setGlobalFontFallback ( const Vector < String > & fallbacks )

Sets the global list of fallback fonts. When a character is not found in the current font, the system searches these fonts in order. Global fallbacks apply to all fonts.
### Arguments

- *const [Vector](../../../api/library/containers/vector/class.vector_cpp.md)<[String](../../../api/library/common/class.string_cpp.md)> &* **fallbacks** - List of paths to fallback font files.

## void getGlobalFontFallback ( Vector < String > & OUT_ret )

Returns the global list of fallback fonts.
### Arguments

- *[Vector](../../../api/library/containers/vector/class.vector_cpp.md)<[String](../../../api/library/common/class.string_cpp.md)> &* **OUT_ret** - An array to store the paths to global fallback font files. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## void setFontFallback ( const char * font , const Vector < String > & fallbacks )

Sets the list of fallback fonts for a specific font. When a character is not found in the specified font, the system searches these fonts first, then the global fallbacks.
### Arguments

- *const char ** **font** - Path to the font file to set fallbacks for.
- *const [Vector](../../../api/library/containers/vector/class.vector_cpp.md)<[String](../../../api/library/common/class.string_cpp.md)> &* **fallbacks** - List of paths to fallback font files.

## void getFontFallback ( const char * font , Vector < String > & OUT_ret )

Returns the list of fallback fonts for a specific font.
### Arguments

- *const char ** **font** - Path to the font file to get fallbacks for.
- *[Vector](../../../api/library/containers/vector/class.vector_cpp.md)<[String](../../../api/library/common/class.string_cpp.md)> &* **OUT_ret** - An array to store the paths to fallback font files for the specified font. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.
