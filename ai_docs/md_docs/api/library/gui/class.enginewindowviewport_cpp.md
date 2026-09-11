# Unigine::EngineWindowViewport Class (CPP)

**Header:** #include <UnigineWindowManager.h>

**Inherits from:** EngineWindow


The class to create and manage window viewports: setting cameras, specifying engine tools available (console, profiler, visualizer, etc.), add widgets to the client area.


To create an engine window viewport, use one of the class constructors:

```cpp
// create an engine window of the specified size with the specified name
EngineWindowViewportPtr window = EngineWindowViewport::create("New window", 580, 300);


```


Then you can specify behavior of the window viewport and add widgets to its client area:

```cpp
// set the window viewport as the main one
window->setMain(true);

// enable the console, profiler and visualizer for the window viewport
window->setConsoleUsage(true);
window->setProfilerUsage(true);
window->setVisualizerUsage(true);

// add widgets to the client area
window->addChild(WidgetLabel::create(window->getSelfGui(), String::format("This is %s window.", window->getTitle())));
window->addChild(WidgetButton::create(window->getSelfGui(), window->getTitle()), Gui::ALIGN_CENTER);


```


## EngineWindowViewport Class

### Members

## Ptr < Viewport > getViewport () const

Returns the current window viewport.
### Return value

Current window viewport.
## void setCamera ( const Ptr < Camera >& camera )

Sets a new camera the image from which is rendered to the engine window viewport. This value has a higher priority over the [main camera flag](#setMain_int_void).
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Camera](../../../api/library/rendering/class.camera_cpp.md)>&* **camera** - The camera the image from which is rendered to the engine window.

## Ptr < Camera > getCamera () const

Returns the current camera the image from which is rendered to the engine window viewport. This value has a higher priority over the [main camera flag](#setMain_int_void).
### Return value

Current camera the image from which is rendered to the engine window.
## void setMain ( bool main )

Sets a new value indicating if the window is set as the main window in order to use its size in logic, render from the main player into it, grab controls, etc.
> **Notice:** There may be several windows that are set as main, or no main windows at all.


### Arguments

- *bool* **main** - Set **true** to enable the window as the main window; **false** - to disable it.

## bool isMain () const

Returns the current value indicating if the window is set as the main window in order to use its size in logic, render from the main player into it, grab controls, etc.
> **Notice:** There may be several windows that are set as main, or no main windows at all.


### Return value

**true** if the window as the main window; otherwise **false**.
## void setConsoleUsage ( bool usage )

Sets a new value indicating if the console is displayed for the window currently in focus.
### Arguments

- *bool* **usage** - Set **true** to enable the console display for the window currently in focus; **false** - to disable it.

## bool isConsoleUsage () const

Returns the current value indicating if the console is displayed for the window currently in focus.
### Return value

**true** if the console display for the window currently in focus is enabled ; otherwise **false**.
## void setProfilerUsage ( bool usage )

Sets a new value indicating if the profiler is displayed for the window currently in focus.
### Arguments

- *bool* **usage** - Set **true** to enable the profiler display for the window currently in focus; **false** - to disable it.

## bool isProfilerUsage () const

Returns the current value indicating if the profiler is displayed for the window currently in focus.
### Return value

**true** if the profiler display for the window currently in focus is enabled ; otherwise **false**.
## void setVisualizerUsage ( bool usage )

Sets a new value indicating if the visualizer is displayed for the window currently in focus.
### Arguments

- *bool* **usage** - Set **true** to enable the visualizer display for the window currently in focus; **false** - to disable it.

## bool isVisualizerUsage () const

Returns the current value indicating if the visualizer is displayed for the window currently in focus.
### Return value

**true** if the visualizer display for the window currently in focus is enabled ; otherwise **false**.
## void setSkipRenderEngine ( bool engine )

Sets a new value indicating whether the Engine rendering for the current window is disabled (even if it has the [main camera flag](#setMain_int_void) or the [user camera](#setCamera_Camera_void) set). This doesn't disable the Gui instance, so widgets and the console remain available.
### Arguments

- *bool* **engine** - value indicating whether the Engine rendering for the current window is disabled

## bool isSkipRenderEngine () const

Returns the current value indicating whether the Engine rendering for the current window is disabled (even if it has the [main camera flag](#setMain_int_void) or the [user camera](#setCamera_Camera_void) set). This doesn't disable the Gui instance, so widgets and the console remain available.
### Return value

value indicating whether the Engine rendering for the current window is disabled
## bool isFullscreen () const

Returns the current value indicating if the engine window is the fullscreen state. A nested window will be withdrawn from the group if set to fullscreen.
### Return value

true if the engine window is the fullscreen state, false if it is in the window mode.
## void setMouseGrab ( bool grab )

Sets a new value indicating if the mouse pointer is bound to the engine window viewport.
> **Notice:** This method can be applied to a separate or parent window, using this method for a nested window is not allowed (it returns false).

### Arguments

- *bool* **grab** - Set **true** to enable the pointer cannot leave the engine window viewport; **false** - to disable it.

## bool isMouseGrab () const

Returns the current value indicating if the mouse pointer is bound to the engine window viewport.
> **Notice:** This method can be applied to a separate or parent window, using this method for a nested window is not allowed (it returns false).

### Return value

**true** if the pointer cannot leave the engine window viewport; otherwise **false**.
## int getNumChildren () const

Returns the current total number of children widgets of the engine window.
### Return value

Current total number of children widgets of the engine window.
## Event<const Ptr < EngineWindowViewport > &> getEventCustomRender () const

Subscribing to this event makes the engine stop rendering the scene to this viewport � using this approach you may implement your own rendering to the viewport. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(const Ptr<EngineWindowViewport> & **viewport**)*
### Return value

Event instance.
## void setAspectCorrection ( bool correction )

Sets a new value indicating if the aspect correction for the engine window viewport is enabled.
### Arguments

- *bool* **correction** - Set **true** to enable the aspect correction; **false** - to disable it.

## bool isAspectCorrection () const

Returns the current value indicating if the aspect correction for the engine window viewport is enabled.
### Return value

**true** if the aspect correction is enabled ; otherwise **false**.
---

## static EngineWindowViewportPtr create ( const Math:: ivec2 & size , int flags = 0 )

Constructor. Creates the window viewport of the specified size with the specified flags.
### Arguments

- *const  Math::[ivec2](../../../api/library/math/class.ivec2_cpp.md) &* **size** - Window size (width and height).
- *int* **flags** - Mask containing window [flags](../../../api/library/gui/class.enginewindow_cpp.md#FLAGS_MAIN).

## static EngineWindowViewportPtr create ( int width , int height , int flags = 0 )

Constructor. Creates the window viewport of the specified size with the specified flags.
### Arguments

- *int* **width** - Window width.
- *int* **height** - Window height.
- *int* **flags** - Mask containing window [flags](../../../api/library/gui/class.enginewindow_cpp.md#FLAGS_MAIN).

## static EngineWindowViewportPtr create ( const char * window_title , int width , int height , int flags = 0 )

Constructor. Creates the window viewport of the specified size with the specified title and flags.
### Arguments

- *const char ** **window_title** - The title of the window, in UTF-8 encoding.
- *int* **width** - Window width.
- *int* **height** - Window height.
- *int* **flags** - Mask containing window [flags](../../../api/library/gui/class.enginewindow_cpp.md#FLAGS_MAIN).

## void disableFullscreen ( )

Disables the fullscreen mode for the window in the fullscreen mode and sets the focus to this window. States and positions of other windows are restored.
> **Notice:** This method can't be applied to nested windows.


## bool enableFullscreen ( int display = -1 , int mode = -1 )

Enables the specified fullscreen mode for the specified display. The states of other displayed windows are stored in order to restore their states and positions when the fullscreen mode is [disabled](#disableFullscreen_void). A nested window will be withdrawn from the group if set to fullscreen.
### Arguments

- *int* **display** - Display index.
- *int* **mode** - Index of the mode supported by the display.

### Return value

true if the specified fullscreen mode has been enabled for the specified display; otherwise, false.
## void addChild ( const Ptr < Widget > & widget , int flags = -1 )

Adds the specified widget as a child to the client area of the engine window.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Widget](../../../api/library/gui/class.widget_cpp.md)> &* **widget** - Child widget to be added.
- *int* **flags** - Widget flags: one of the [ALIGN_*](../../../api/library/gui/class.gui_cpp.md#ALIGN_BACKGROUND) pre-defined variables. This is an optional parameter.

## void removeChild ( const Ptr < Widget > & widget )

Removes the specified widget from the engine window.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Widget](../../../api/library/gui/class.widget_cpp.md)> &* **widget** - Child widget to be removed.

## Ptr < Widget > getChild ( int index )

Returns the child widget by its index.
### Arguments

- *int* **index** - Widget index.

### Return value

Child widget.
## bool isChild ( const Ptr < Widget > & widget )

Checks if the argument widget is the child of the current window viewport.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Widget](../../../api/library/gui/class.widget_cpp.md)> &* **widget** - Widget.

### Return value

true if the widget is the child of the current window viewport; otherwise, false.
## void calculateEngineRenderResolution ( Math:: ivec2 & render_resolution_min , Math:: ivec2 & render_resolution_max , Math:: ivec2 & render_resolution ) const

Calculates the actual internal render resolutions for this viewport window based on the current client render size and the global render settings (render border, supersampling, dynamic resolution bounds, and the upscaler input resolution when the viewport renders the full pipeline).
### Arguments

- *Math::[ivec2](../../../api/library/math/class.ivec2_cpp.md) &* **render_resolution_min** - Output value: the minimum resolution the engine may render at (differs from the maximum only when dynamic resolution is enabled).
- *Math::[ivec2](../../../api/library/math/class.ivec2_cpp.md) &* **render_resolution_max** - Output value: the maximum resolution the engine may render at.
- *Math::[ivec2](../../../api/library/math/class.ivec2_cpp.md) &* **render_resolution** - Output value: the resolution the next frame is going to be rendered at.
