# Unigine::EngineWindowViewport Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** EngineWindow


The class to create and manage window viewports: setting cameras, specifying engine tools available (console, profiler, visualizer, etc.), add widgets to the client area.


## EngineWindowViewport Class

### Members

## Viewport getViewport () const

Returns the current window viewport.
### Return value

Current window viewport.
## void setCamera ( Camera camera )

Sets a new camera the image from which is rendered to the engine window viewport. This value has a higher priority over the [main camera flag](#setMain_int_void).
### Arguments

- *[Camera](../../../api/library/rendering/class.camera_usc.md)* **camera** - The camera the image from which is rendered to the engine window.

## Camera getCamera () const

Returns the current camera the image from which is rendered to the engine window viewport. This value has a higher priority over the [main camera flag](#setMain_int_void).
### Return value

Current camera the image from which is rendered to the engine window.
## void setMain ( int main )

Sets a new value indicating if the window is set as the main window in order to use its size in logic, render from the main player into it, grab controls, etc.
> **Notice:** There may be several windows that are set as main, or no main windows at all.


### Arguments

- *int* **main** - The the window as the main window

## int isMain () const

Returns the current value indicating if the window is set as the main window in order to use its size in logic, render from the main player into it, grab controls, etc.
> **Notice:** There may be several windows that are set as main, or no main windows at all.


### Return value

Current the window as the main window
## void setConsoleUsage ( )

Sets a new value indicating if the console is displayed for the window currently in focus.
### Arguments

- **usage** - The the console display for the window currently in focus

## isConsoleUsage () const

Returns the current value indicating if the console is displayed for the window currently in focus.
### Return value

Current the console display for the window currently in focus
## void setProfilerUsage ( )

Sets a new value indicating if the profiler is displayed for the window currently in focus.
### Arguments

- **usage** - The the profiler display for the window currently in focus

## isProfilerUsage () const

Returns the current value indicating if the profiler is displayed for the window currently in focus.
### Return value

Current the profiler display for the window currently in focus
## void setVisualizerUsage ( )

Sets a new value indicating if the visualizer is displayed for the window currently in focus.
### Arguments

- **usage** - The the visualizer display for the window currently in focus

## isVisualizerUsage () const

Returns the current value indicating if the visualizer is displayed for the window currently in focus.
### Return value

Current the visualizer display for the window currently in focus
## void setSkipRenderEngine ( )

Sets a new value indicating whether the Engine rendering for the current window is disabled (even if it has the [main camera flag](#setMain_int_void) or the [user camera](#setCamera_Camera_void) set). This doesn't disable the Gui instance, so widgets and the console remain available.
### Arguments

- **engine** - The true to disable Engine rendering; false to enable it.

## isSkipRenderEngine () const

Returns the current value indicating whether the Engine rendering for the current window is disabled (even if it has the [main camera flag](#setMain_int_void) or the [user camera](#setCamera_Camera_void) set). This doesn't disable the Gui instance, so widgets and the console remain available.
### Return value

Current true to disable Engine rendering; false to enable it.
## isFullscreen () const

Returns the current value indicating if the engine window is the fullscreen state. A nested window will be withdrawn from the group if set to fullscreen.
### Return value

Current true if the engine window is the fullscreen state, false if it is in the window mode.
## void setMouseGrab ( )

Sets a new value indicating if the mouse pointer is bound to the engine window viewport.
> **Notice:** This method can be applied to a separate or parent window, using this method for a nested window is not allowed (it returns false).

### Arguments

- **grab** - The the pointer cannot leave the engine window viewport

## isMouseGrab () const

Returns the current value indicating if the mouse pointer is bound to the engine window viewport.
> **Notice:** This method can be applied to a separate or parent window, using this method for a nested window is not allowed (it returns false).

### Return value

Current the pointer cannot leave the engine window viewport
## int getNumChildren () const

Returns the current total number of children widgets of the engine window.
### Return value

Current total number of children widgets of the engine window.
## getEventCustomRender () const

The event handler signature is as follows: *myhandler()*
### Return value

Event reference.
## void setAspectCorrection ( bool correction )

Sets a new value indicating if the aspect correction for the engine window viewport is enabled.
### Arguments

- *bool* **correction** - Set **true** to enable the aspect correction; **false** - to disable it.

## bool isAspectCorrection () const

Returns the current value indicating if the aspect correction for the engine window viewport is enabled.
### Return value

**true** if the aspect correction is enabled; otherwise **false**.
---

## static EngineWindowViewport ( ivec2 size , int flags = 0 )

Constructor. Creates the window viewport of the specified size with the specified flags.
### Arguments

- *ivec2* **size** - Window size (width and height).
- *int* **flags** - Mask containing window [flags](../../../api/library/gui/class.enginewindow_usc.md#FLAGS_MAIN).

## static EngineWindowViewport ( int width , int height , int flags = 0 )

Constructor. Creates the window viewport of the specified size with the specified flags.
### Arguments

- *int* **width** - Window width.
- *int* **height** - Window height.
- *int* **flags** - Mask containing window [flags](../../../api/library/gui/class.enginewindow_usc.md#FLAGS_MAIN).

## static EngineWindowViewport ( string window_title , int width , int height , int flags = 0 )

Constructor. Creates the window viewport of the specified size with the specified title and flags.
### Arguments

- *string* **window_title** - The title of the window, in UTF-8 encoding.
- *int* **width** - Window width.
- *int* **height** - Window height.
- *int* **flags** - Mask containing window [flags](../../../api/library/gui/class.enginewindow_usc.md#FLAGS_MAIN).

## void disableFullscreen ( )

Disables the fullscreen mode for the window in the fullscreen mode and sets the focus to this window. States and positions of other windows are restored.
> **Notice:** This method can't be applied to nested windows.


## int enableFullscreen ( int display = -1 , int mode = -1 )

Enables the specified fullscreen mode for the specified display. The states of other displayed windows are stored in order to restore their states and positions when the fullscreen mode is [disabled](#disableFullscreen_void). A nested window will be withdrawn from the group if set to fullscreen.
### Arguments

- *int* **display** - Display index.
- *int* **mode** - Index of the mode supported by the display.

### Return value

**1** if the specified fullscreen mode has been enabled for the specified display; otherwise, **0**.
## void addChild ( Widget widget , int flags = -1 )

Adds the specified widget as a child to the client area of the engine window.
### Arguments

- *[Widget](../../../api/library/gui/class.widget_usc.md)* **widget** - Child widget to be added.
- *int* **flags** - Widget flags: one of the [ALIGN_*](../../../api/library/gui/class.gui_usc.md#ALIGN_BACKGROUND) pre-defined variables. This is an optional parameter.

## void removeChild ( Widget widget )

Removes the specified widget from the engine window.
### Arguments

- *[Widget](../../../api/library/gui/class.widget_usc.md)* **widget** - Child widget to be removed.

## Widget getChild ( int index )

Returns the child widget by its index.
### Arguments

- *int* **index** - Widget index.

### Return value

Child widget.
## int isChild ( Widget widget )

Checks if the argument widget is the child of the current window viewport.
### Arguments

- *[Widget](../../../api/library/gui/class.widget_usc.md)* **widget** - Widget.

### Return value

**1** if the widget is the child of the current window viewport; otherwise, **0**.
