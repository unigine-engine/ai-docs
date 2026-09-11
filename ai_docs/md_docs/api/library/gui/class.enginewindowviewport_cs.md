# Unigine::EngineWindowViewport Class (CS)

**Inherits from:** EngineWindow


The class to create and manage window viewports: setting cameras, specifying engine tools available (console, profiler, visualizer, etc.), add widgets to the client area.


To create an engine window viewport, use one of the class constructors:

```csharp
// create an engine window of the specified size with the specified name
EngineWindowViewport window = new EngineWindowViewport("Window", 580, 300);


```


Then you can specify behavior of the window viewport and add widgets to its client area:

```csharp
// set the window viewport as the main one
window.Main = true;

// enable the console, profiler and visualizer for the window viewport
window.ConsoleUsage = true;
window.ProfilerUsage = true;
window.VisualizerUsage = true;

// add widgets to the client area
window.AddChild(new WidgetLabel(window.SelfGui,  String.Format("This is {0} window.", window.Title)));
window.AddChild(new WidgetButton(window.SelfGui, window.Title), Gui.ALIGN_CENTER);


```


## EngineWindowViewport Class

### Properties

## 🔒︎ Viewport Viewport

The window viewport.
## Camera Camera

The camera the image from which is rendered to the engine window viewport. This value has a higher priority over the [main camera flag](#setMain_int_void).
## bool Main

The value indicating if the window is set as the main window in order to use its size in logic, render from the main player into it, grab controls, etc.
> **Notice:** There may be several windows that are set as main, or no main windows at all.


## bool ConsoleUsage

The value indicating if the console is displayed for the window currently in focus.
## bool ProfilerUsage

The value indicating if the profiler is displayed for the window currently in focus.
## bool VisualizerUsage

The value indicating if the visualizer is displayed for the window currently in focus.
## bool SkipRenderEngine

The value indicating whether the Engine rendering for the current window is disabled (even if it has the [main camera flag](#setMain_int_void) or the [user camera](#setCamera_Camera_void) set). This doesn't disable the Gui instance, so widgets and the console remain available.
## 🔒︎ bool IsFullscreen

The value indicating if the engine window is the fullscreen state. A nested window will be withdrawn from the group if set to fullscreen.
## bool MouseGrab

The value indicating if the mouse pointer is bound to the engine window viewport.
> **Notice:** This method can be applied to a separate or parent window, using this method for a nested window is not allowed (it returns false).

## 🔒︎ int NumChildren

The total number of children widgets of the engine window.
## 🔒︎ Event< EngineWindowViewport > EventCustomRender

The Subscribing to this event makes the engine stop rendering the scene to this viewport � using this approach you may implement your own rendering to the viewport. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(EngineWindowViewport **viewport**)*
## bool AspectCorrection

The value indicating if the aspect correction for the engine window viewport is enabled.
### Members

---

## EngineWindowViewport ( ivec2 size , int flags = 0 )

Constructor. Creates the window viewport of the specified size with the specified flags.
### Arguments

- *ivec2* **size** - Window size (width and height).
- *int* **flags** - Mask containing window [flags](../../../api/library/gui/class.enginewindow_cs.md#FLAGS).

## EngineWindowViewport ( int width , int height , int flags = 0 )

Constructor. Creates the window viewport of the specified size with the specified flags.
### Arguments

- *int* **width** - Window width.
- *int* **height** - Window height.
- *int* **flags** - Mask containing window [flags](../../../api/library/gui/class.enginewindow_cs.md#FLAGS).

## EngineWindowViewport ( string window_title , int width , int height , int flags = 0 )

Constructor. Creates the window viewport of the specified size with the specified title and flags.
### Arguments

- *string* **window_title** - The title of the window, in UTF-8 encoding.
- *int* **width** - Window width.
- *int* **height** - Window height.
- *int* **flags** - Mask containing window [flags](../../../api/library/gui/class.enginewindow_cs.md#FLAGS).

## void DisableFullscreen ( )

Disables the fullscreen mode for the window in the fullscreen mode and sets the focus to this window. States and positions of other windows are restored.
> **Notice:** This method can't be applied to nested windows.


## bool EnableFullscreen ( int display = -1 , int mode = -1 )

Enables the specified fullscreen mode for the specified display. The states of other displayed windows are stored in order to restore their states and positions when the fullscreen mode is [disabled](#disableFullscreen_void). A nested window will be withdrawn from the group if set to fullscreen.
### Arguments

- *int* **display** - Display index.
- *int* **mode** - Index of the mode supported by the display.

### Return value

true if the specified fullscreen mode has been enabled for the specified display; otherwise, false.
## void AddChild ( Widget widget , int flags = -1 )

Adds the specified widget as a child to the client area of the engine window.
### Arguments

- *[Widget](../../../api/library/gui/class.widget_cs.md)* **widget** - Child widget to be added.
- *int* **flags** - Widget flags: one of the [ALIGN_*](../../../api/library/gui/class.gui_cs.md#ALIGN_BACKGROUND) pre-defined variables. This is an optional parameter.

## void RemoveChild ( Widget widget )

Removes the specified widget from the engine window.
### Arguments

- *[Widget](../../../api/library/gui/class.widget_cs.md)* **widget** - Child widget to be removed.

## Widget GetChild ( int index )

Returns the child widget by its index.
### Arguments

- *int* **index** - Widget index.

### Return value

Child widget.
## bool IsChild ( Widget widget )

Checks if the argument widget is the child of the current window viewport.
### Arguments

- *[Widget](../../../api/library/gui/class.widget_cs.md)* **widget** - Widget.

### Return value

true if the widget is the child of the current window viewport; otherwise, false.
## void CalculateEngineRenderResolution ( out ivec2 render_resolution_min , out ivec2 render_resolution_max , out ivec2 render_resolution )

Calculates the actual internal render resolutions for this viewport window based on the current client render size and the global render settings (render border, supersampling, dynamic resolution bounds, and the upscaler input resolution when the viewport renders the full pipeline).
### Arguments

- *out ivec2* **render_resolution_min** - Output value: the minimum resolution the engine may render at (differs from the maximum only when dynamic resolution is enabled).
- *out ivec2* **render_resolution_max** - Output value: the maximum resolution the engine may render at.
- *out ivec2* **render_resolution** - Output value: the resolution the next frame is going to be rendered at.
