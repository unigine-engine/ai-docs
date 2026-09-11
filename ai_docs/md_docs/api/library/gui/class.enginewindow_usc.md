# Unigine::EngineWindow Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


This base class operates with engine windows: their components, relations with other windows, size, position, visual representation and other features.


When you create [a window viewport](../../../api/library/gui/class.enginewindowviewport_usc.md) or [a window group](../../../api/library/gui/class.enginewindowgroup_usc.md), the engine window is created.


The image below demonstrates the window components that can be controlled by the EngineWindow class methods.


![Window components](window_structure.png)


To create the engine window, use one of the *[EngineWindowViewport](../../../api/library/gui/class.enginewindowviewport_usc.md)* or *[EngineWindowGroup](../../../api/library/gui/class.enginewindowgroup_usc.md)* class constructors. For example:


Then, by using methods of the *EngineWindow* class, you can specify the window appearance (for example, set a title, an icon, change opacity, add borders, and so on), and properties (whether the window can be nested, or whether it can become a group), define its style (system or engine), change the window state (whether it is shown/hidden, minimized/maximized, focused, etc.), manage window intersections and events.


### Setting Up Position and Size


In UNIGINE, the window size and position coordinates are measured in both [logical units](../../../principles/dpi/index.md) and pixels:


- The size and position in *units* don't depend on the [DPI scale](#getDpiScale_float) and always remain the same. You can change the window and client area size via **[setSize()](../../...md#setSize_ivec2_void)**and **[setClientSize()](../../...md#setClientSize_ivec2_void)**, adjust the [minimum](#setMinSize_ivec2_void) and [maximum size](#setMaxSize_ivec2_void) and set the window and client position via the corresponding methods. All of them work with units.
- The size and position in *pixels* are calculated by multiplying the size in units by the current [DPI scale](#getDpiScale_float). You can get it using one of the *RenderSize*-related methods/properties (e.g., **[getRenderSize()](../../...md#getRenderSize_ivec2)**, and so on). When the DPI scale is 100%, *1 unit corresponds to 1 pixel*. > **Notice:** DPI scaling is applied only when the `auto_dpi` flag is enabled. You can check the current flag value via the console or by using **[WindowManager.isAutoDpiScaling()](../../../api/library/gui/class.windowmanager_usc.md#isAutoDpiScaling_int)**. >  To determine how the OS handles the DPI scale, specify the *[DPI awareness mode](../../../api/library/gui/class.windowmanager_usc.md#DPI_AWARENESS)*.


You should consider this information when resizing textures, calculating mouse intersections, etc. The window size and position should be set individually, depending on the situation.


> **Notice:** If necessary, you can convert the size and position coordinates *from units to pixels* and visa versa:
> - Use one of the **[toRenderSize()](../../...md#toRenderSize_int_int)**or **[toUnitSize()](../../...md#toUnitSize_int_int)**to convert the size.
> - Use **[globalToLocalUnitPosition()](../../...md#globalToLocalUnitPosition_ivec2_ivec2)**to transform the coordinates in pixels into units or **[localUnitToGlobalPosition()](../../...md#localUnitToGlobalPosition_ivec2_ivec2)**to do the opposite.


In the following example, the positions of the window and client area (in units) change to the mouse cursor when you press the **P** or **C** respectively:


### Adjusting Visual Representation


The window visual representation includes all available window parameters such as title and title bar, icon, borders, opacity, and window style (the engine or system one).


Here are some window examples:


| ![](system_style.jpg) *A system-style window* | ![](borders_bar_disabled.jpg) *A window (either system or engine style),borders and title bar disabled* |
|---|---|
| ![](engine_style_borders_disabled.jpg) *An engine-style window, borders disabled* | ![](engine_style_borders_enabled.jpg) *An engine-style window, borders enabled* |


The *system* and *engine* style windows have the same component layout except the sizing border: in the engine style, it is in the visual part of the window.


The ability to customize the window style makes it possible to create a standard set of window settings for different systems and frameworks.


### Setting Up Order


In the following example, the order of the window under the cursor changes when you press the specific button: **T** to make the window appear on top of all other windows, **A** to always render the window above the other windows.


### Changing Behavior


With the set of behavior-related functions, you can do the following:


- Force the engine to [stop operating](#setHoldEngine_int_void) while the engine window is opened.
- Ignore or allow [using the OS methods for windows closing](#setIgnoreSystemClose_int_void).
- Specify whether the window is [resizable](#setResizable_int_void).
- Specify the sizing border size.
- Control rendering of the engine window - [show, hide, focus, minimize, maximize, restore, or close](#show_void).


### Working with Modal Windows


The following example demonstrates how to create modal windows and add modal children to the main window. Additionally, the main window includes a message that informs the user whether they can close the window or not.


## EngineWindow Class

### Members

## Gui getGui () const

Returns the current parent Gui for a window. If the window is nested, this Gui differs from [SelfGui](#getSelfGui_Gui).
### Return value

Current Gui instance.
## int getDisplayIndex () const

Returns the current number of the display, on which the window is currently displayed. For separate windows, this index is requested from the system proxy; for nested windows, the index is provided based on the location of the client center point.
### Return value

Current number of the display, on which the window is currently displayed.
## int isNested () const

Returns the current value indicating if this is a nested window or group of windows.
### Return value

Current this is a nested window or group of windows
## int isSeparate () const

Returns the current value indicating if this is a separate window or group of windows.
### Return value

Current this is a separate window or group of windows
## Gui getSelfGui () const

Returns the current Gui instance for a window. This Gui remains unchanged during the whole lifecycle of the window.
### Return value

Current Gui instance.
## void setPosition ( ivec2 position )

Sets a new position of the [top left corner](#window_structure) of the window in the screen coordinates (pixels). In case of several displays, the position is relative to the main display.
> **Notice:** This method should be applied to a separate or parent window, using this method for a nested window is not allowed.


### Arguments

- *ivec2* **position** - The window screen position (coordinates of the top left corner).

## ivec2 getPosition () const

Returns the current position of the [top left corner](#window_structure) of the window in the screen coordinates (pixels). In case of several displays, the position is relative to the main display.
> **Notice:** This method should be applied to a separate or parent window, using this method for a nested window is not allowed.


### Return value

Current window screen position (coordinates of the top left corner).
## void setClientPosition ( ivec2 position )

Sets a new position of the [top left corner](#window_structure) of the client (the window content area without the top bar and borders) in the screen coordinates (pixels). In case of several displays, the position is relative to the main display.
> **Notice:** This method should be applied to a separate or parent window, using this method for a nested window is not allowed.


### Arguments

- *ivec2* **position** - The screen position of the client (coordinates of the top left corner).

## ivec2 getClientPosition () const

Returns the current position of the [top left corner](#window_structure) of the client (the window content area without the top bar and borders) in the screen coordinates (pixels). In case of several displays, the position is relative to the main display.
> **Notice:** This method should be applied to a separate or parent window, using this method for a nested window is not allowed.


### Return value

Current screen position of the client (coordinates of the top left corner).
## ivec2 getClientLocalPosition () const

Returns the current position of the [top left corner](#window_structure) of the client (the window content area without the top bar and borders) relative to the window position in the screen coordinates (pixels).
### Return value

Current screen position of the client (coordinates of the top left corner) relative to the window position in the screen coordinates (pixels).
## void setSize ( ivec2 size )

Sets a new engine [window size](#window_structure) in [logical units](../../../principles/dpi/index.md) (including the sizing border).
> **Notice:** This method is for a separate or parent window, using this method for a nested window is not allowed (when requesting the current value, it will return the value of the global parent group).


### Arguments

- *ivec2* **size** - The engine [window size](#window_structure) in [logical units](../../../principles/dpi/index.md) (including the sizing border).

## ivec2 getSize () const

Returns the current engine [window size](#window_structure) in [logical units](../../../principles/dpi/index.md) (including the sizing border).
> **Notice:** This method is for a separate or parent window, using this method for a nested window is not allowed (when requesting the current value, it will return the value of the global parent group).


### Return value

Current engine [window size](#window_structure) in [logical units](../../../principles/dpi/index.md) (including the sizing border).
## void setClientSize ( ivec2 size )

Sets a new size of the window [client (content) area](#window_structure) in [logical units](../../../principles/dpi/index.md).
### Arguments

- *ivec2* **size** - The size of the window client (content) area in logical units

## ivec2 getClientSize () const

Returns the current size of the window [client (content) area](#window_structure) in [logical units](../../../principles/dpi/index.md).
### Return value

Current size of the window client (content) area in logical units
## void setMinSize ( ivec2 size )

Sets a new minimum possible window size in [logical units](../../../principles/dpi/index.md) when resizing the window. If the value is more than the current maximum size, use the [setMinAndMaxSize()](#setMinAndMaxSize_ivec2_ivec2_void) method, to change both values at once. Otherwise the value will be clamped to the current maximum size.
> **Notice:** This method should be applied to a separate or parent window, using this method for a nested window is not allowed (it will return zero values).


### Arguments

- *ivec2* **size** - The minimum possible size of the window.

## ivec2 getMinSize () const

Returns the current minimum possible window size in [logical units](../../../principles/dpi/index.md) when resizing the window. If the value is more than the current maximum size, use the [setMinAndMaxSize()](#setMinAndMaxSize_ivec2_ivec2_void) method, to change both values at once. Otherwise the value will be clamped to the current maximum size.
> **Notice:** This method should be applied to a separate or parent window, using this method for a nested window is not allowed (it will return zero values).


### Return value

Current minimum possible size of the window.
## void setMaxSize ( ivec2 size )

Sets a new maximum possible window size in [logical units](../../../principles/dpi/index.md) when resizing the window. If the value is less than the current minimum size, use the [setMinAndMaxSize()](#setMinAndMaxSize_ivec2_ivec2_void) method, to change both values at once. Otherwise the value will be clamped to the current minimum size.
> **Notice:** This method should be applied to a separate or parent window, using this method for a nested window is not allowed.


### Arguments

- *ivec2* **size** - The maximum possible size of the window.

## ivec2 getMaxSize () const

Returns the current maximum possible window size in [logical units](../../../principles/dpi/index.md) when resizing the window. If the value is less than the current minimum size, use the [setMinAndMaxSize()](#setMinAndMaxSize_ivec2_ivec2_void) method, to change both values at once. Otherwise the value will be clamped to the current minimum size.
> **Notice:** This method should be applied to a separate or parent window, using this method for a nested window is not allowed.


### Return value

Current maximum possible size of the window.
## void setTitle ( string title )

Sets a new text of the title for the window. For a separate window, the title is set via system proxy in the title bar only; for a nested window, it is also set in the tab of the parent group.
### Arguments

- *string* **title** - The title of the window.

## const char * getTitle () const

Returns the current text of the title for the window. For a separate window, the title is set via system proxy in the title bar only; for a nested window, it is also set in the tab of the parent group.
### Return value

Current title of the window.
## void setOpacity ( float opacity )

Sets a new opacity for the window.
> **Notice:** This method should be applied to a separate or parent window, using this method for a nested window is not allowed (it will always return 1.0f).


### Arguments

- *float* **opacity** - The opacity for the window.

## float getOpacity () const

Returns the current opacity for the window.
> **Notice:** This method should be applied to a separate or parent window, using this method for a nested window is not allowed (it will always return 1.0f).


### Return value

Current opacity for the window.
## void setBordersEnabled ( int enabled )

Sets a new value indicating if the borders are enabled for the engine window.
> **Notice:** This method should be applied to a separate or parent window, using this method for a nested window is not allowed (it will return false).


### Arguments

- *int* **enabled** - The borders for the window

## int isBordersEnabled () const

Returns the current value indicating if the borders are enabled for the engine window.
> **Notice:** This method should be applied to a separate or parent window, using this method for a nested window is not allowed (it will return false).


### Return value

Current borders for the window
## void setBorderSize ( int size )

Sets a new engine window border size.
> **Notice:** - This value is applied to the windows in the [engine style](#isEngineStyle_int) only. For system-style windows system settings are applied.
> - This method should be applied to a separate or parent window, using this method for a nested window is not allowed (it will return 0).


### Arguments

- *int* **size** - The engine window border size.

## int getBorderSize () const

Returns the current engine window border size.
> **Notice:** - This value is applied to the windows in the [engine style](#isEngineStyle_int) only. For system-style windows system settings are applied.
> - This method should be applied to a separate or parent window, using this method for a nested window is not allowed (it will return 0).


### Return value

Current engine window border size.
## void setResizable ( int resizable )

Sets a new value indicating if the engine window is resizable by the mouse.
> **Notice:** This method should be applied to a separate or parent window, using this method for a nested window is not allowed (it will return false).


### Arguments

- *int* **resizable** - The resizing of the engine window with the mouse

## int isResizable () const

Returns the current value indicating if the engine window is resizable by the mouse.
> **Notice:** This method should be applied to a separate or parent window, using this method for a nested window is not allowed (it will return false).


### Return value

Current resizing of the engine window with the mouse
## int isShown () const

Returns the current value indicating if the engine window is rendered.
> **Notice:** This method should be applied to a separate or parent window, for a nested window it will return the value of the global parent group.


### Return value

Current the engine window is rendered
## int isHidden () const

Returns the current value indicating if the engine window isn't rendered.
> **Notice:** This method should be applied to a separate or parent window, for a nested window it will return the value of the global parent group.


### Return value

Current the engine window isn't rendered
## int isFocused () const

Returns the current value indicating if the engine window is in focus.
> **Notice:** This method should be applied to a separate or parent window, for a nested window it will return the value of the global parent group.


### Return value

Current the engine window is in focus
## int isMinimized () const

Returns the current value indicating if the engine window is minimized.
> **Notice:** This method should be applied to a separate or parent window, for a nested window it will return the value of the global parent group.


### Return value

Current the engine window is minimized
## int isMaximized () const

Returns the current value indicating if the engine window is maximized.
> **Notice:** This method should be applied to a separate or parent window, for a nested window it will return the value of the global parent group.


### Return value

Current the engine window is maximized
## int getOrder () const

Returns the current order of the window. This value allows comparing which window is closer to the viewer (a relatively smaller value).
> **Notice:** This method should be applied to a separate or parent window, for a nested window it will return the value of the global parent group.


### Return value

Current order of the window.
## EngineWindowGroup getParentGroup () const

Returns the current group into which the current window is nested, or NULL if it is a separate window.
### Return value

Current group into which the current window is nested, or NULL if it is a separate window.
## EngineWindowGroup getGlobalParentGroup () const

Returns the current top group of the hierarchy into which the current window is nested, or NULL if it is a separate window.
### Return value

Current top group of the hierarchy into which the current window is nested, or NULL if it is a separate window.
## int getNumDroppedItems () const

Returns the current total number of files and/or folders dropped to the window.
### Return value

Current number of dropped files and/or folders.
## int getNumModalWindows () const

Returns the current total number of modal windows for this window. The concept of **modal** assumes that if a window has modal children, it cannot be closed. Any other interaction with a parent window is possible.
> **Notice:** This method should be applied to a separate or parent window, for a nested window it will return 0.


### Return value

Current total number of modal windows.
## getModalParent () const

Returns the current modal parent of the window. The concept of **modal** assumes that if a window has modal children, it cannot be closed. Any other interaction with a parent window is possible.
> **Notice:** This method should be applied to a separate or parent window, for a nested window it will return nullptr.


### Return value

Current modal parent of the window.
## bool isModalParent () const

Returns the current value indicating if the window is parent for any modal window. The concept of **modal** assumes that if a window has modal children, it cannot be closed. Any other interaction with a parent window is possible.
> **Notice:** This method should be applied to a separate or parent window, for a nested window it will return false.


### Return value

**true** if the window is parent for any modal window; otherwise **false**.
## bool isModal () const

Returns the current value indicating if the window is modal. The concept of **modal** assumes that if a window has modal children, it cannot be closed. Any other interaction with a parent window is possible.
> **Notice:** This method should be applied to a separate or parent window, for a nested window it will return false.


### Return value

**true** if the window is modal; otherwise **false**.
## void setIgnoreSystemClose ( bool close )

Sets a new value indicating if closing the window using the OS methods is ignored (*ALT+F4* or cross in the top-right corner of the window).
### Arguments

- *bool* **close** - Set **true** to enable ignoring OS methods for closing the window; **false** - to disable it.

## bool isIgnoreSystemClose () const

Returns the current value indicating if closing the window using the OS methods is ignored (*ALT+F4* or cross in the top-right corner of the window).
### Return value

**true** if ignoring OS methods for closing the window is enabled ; otherwise **false**.
## void setHoldEngine ( bool engine )

Sets a new value indicating if the engine operation can't be stopped while this window is open.
### Arguments

- *bool* **engine** - Set **true** to enable the engine can't stop operating while this window is open; **false** - to disable it.

## bool isHoldEngine () const

Returns the current value indicating if the engine operation can't be stopped while this window is open.
### Return value

**true** if the engine can't stop operating while this window is open; otherwise **false**.
## getID () const

Returns the current ID of the engine window, which is unchanged during the whole lifecycle of the window.
### Return value

Current ID of the engine window, if the window is external.
## void setAlwaysOnTop ( bool top )

Sets a new value indicating if the window is always rendered above the other windows.
> **Notice:** This method should be applied to a separate or parent window, using this method for a nested window is not allowed (it will return the value of the global parent group).


### Arguments

- *bool* **top** - Set **true** to enable the window is always on top; **false** - to disable it.

## bool isAlwaysOnTop () const

Returns the current value indicating if the window is always rendered above the other windows.
> **Notice:** This method should be applied to a separate or parent window, using this method for a nested window is not allowed (it will return the value of the global parent group).


### Return value

**true** if the window is always on top; otherwise **false**.
## bool isHiddenByTab () const

Returns the current value indicating if the window is overlapped by any other tab (either by switching to another tab or resizing this window to have zero client area).
### Return value

**true** if the window is overlapped by any other tab; otherwise **false**.
## void setCanCreateGroup ( bool group )

Sets a new value indicating if the engine window can become a group.
### Arguments

- *bool* **group** - Set **true** to enable usage of the engine window as a group; **false** - to disable it.

## bool isCanCreateGroup () const

Returns the current value indicating if the engine window can become a group.
### Return value

**true** if usage of the engine window as a group is enabled ; otherwise **false**.
## void setCanBeNested ( bool nested )

Sets a new value indicating if the engine window can be used as a nested window.
### Arguments

- *bool* **nested** - Set **true** to enable usage of the engine window as a nested window; **false** - to disable it.

## bool isCanBeNested () const

Returns the current value indicating if the engine window can be used as a nested window.
### Return value

**true** if usage of the engine window as a nested window is enabled ; otherwise **false**.
## bool isSystemFocused () const

Returns the current value indicating if the engine window is currently in focus.
> **Notice:** This method should be applied to a separate or parent window, for a nested window it will return the value of the global parent group.


### Return value

**true** if the engine window is in focus; otherwise **false**.
## void setSizingBorderSize ( int size )

Sets a new [size of the border](#window_examples) in the widget that is manipulated to resize the window.
> **Notice:** - This method should not be applied to a system-style window with enabled borders, as the system settings cannot be changed (for an unmodified system-style window (i.e. with the enabled border size), the system value is applied).
> - This method should not be applied to nested windows (it will return 0).


### Arguments

- *int* **size** - The size of the border in the widget that is manipulated to resize the window, in pixels.

## int getSizingBorderSize () const

Returns the current [size of the border](#window_examples) in the widget that is manipulated to resize the window.
> **Notice:** - This method should not be applied to a system-style window with enabled borders, as the system settings cannot be changed (for an unmodified system-style window (i.e. with the enabled border size), the system value is applied).
> - This method should not be applied to nested windows (it will return 0).


### Return value

Current size of the border in the widget that is manipulated to resize the window, in pixels.
## void setEngineStyle ( bool style )

Sets a new value indicating if the [engine style](#window_examples) or the default system style is set for the engine window.
> **Notice:** This method should be applied to a separate or parent window, using this method for a nested window is not allowed (it will return true).


### Arguments

- *bool* **style** - Set **true** to enable the engine style for the engine window; **false** - to disable it.

## bool isEngineStyle () const

Returns the current value indicating if the [engine style](#window_examples) or the default system style is set for the engine window.
> **Notice:** This method should be applied to a separate or parent window, using this method for a nested window is not allowed (it will return true).


### Return value

**true** if the engine style for the engine window is enabled ; otherwise **false**.
## void setSystemStyle ( bool style )

Sets a new value indicating if the default [system style](#window_examples) or the engine style is set for the engine window.
> **Notice:** This method should be applied to a separate or parent window, using this method for a nested window is not allowed (it will return true).


### Arguments

- *bool* **style** - Set **true** to enable the default system style for the engine window; **false** - to disable it.

## bool isSystemStyle () const

Returns the current value indicating if the default [system style](#window_examples) or the engine style is set for the engine window.
> **Notice:** This method should be applied to a separate or parent window, using this method for a nested window is not allowed (it will return true).


### Return value

**true** if the default system style for the engine window is enabled ; otherwise **false**.
## void setTitleBarHeight ( int height )

Sets a new height of the window title bar.
> **Notice:** - This value is applied to the windows in the [engine style](#isEngineStyle_int) only. For system-style windows system settings are applied.
> - This method can be applied to a separate or parent window, using this method for a nested window is not allowed (it will return 0).


### Arguments

- *int* **height** - The engine window title bar height.

## int getTitleBarHeight () const

Returns the current height of the window title bar.
> **Notice:** - This value is applied to the windows in the [engine style](#isEngineStyle_int) only. For system-style windows system settings are applied.
> - This method can be applied to a separate or parent window, using this method for a nested window is not allowed (it will return 0).


### Return value

Current engine window title bar height.
## void setTitleBarEnabled ( bool enabled )

Sets a new value indicating if the title bar is enabled for the engine window.
> **Notice:** - This value is applied to the windows in the [engine style](#isEngineStyle_int) only. For system-style windows system settings are applied.
> - This method should be applied to a separate or parent window, using this method for a nested window is not allowed (it will return 0).


### Arguments

- *bool* **enabled** - Set **true** to enable the title bar for the engine window; **false** - to disable it.

## bool isTitleBarEnabled () const

Returns the current value indicating if the title bar is enabled for the engine window.
> **Notice:** - This value is applied to the windows in the [engine style](#isEngineStyle_int) only. For system-style windows system settings are applied.
> - This method should be applied to a separate or parent window, using this method for a nested window is not allowed (it will return 0).


### Return value

**true** if the title bar for the engine window is enabled ; otherwise **false**.
## const char * getTypeName () const

Returns the current name of the engine window type as a string.
### Return value

Current string representation of the engine window type.
## getType () const

Returns the current type of the engine window.
### Return value

Current type of the engine window.
## float getDpiScale () const

Returns the current DPI scale applied to the elements inside the window.
### Return value

Current DPI scale applied to the elements inside the window.
## int getDpi () const

Returns the current DPI level for the window.
### Return value

Current DPI level for the window.
## getMaxRenderSize () const

Returns the current maximum window size in pixels.
### Return value

Current maximum window size in pixels.
## getMinRenderSize () const

Returns the current minimum window size in pixels.
### Return value

Current minimum window size in pixels.
## getClientRenderSize () const

Returns the current client area size in pixels.
### Return value

Current client area size in pixels.
## getRenderSize () const

Returns the current engine window frame size in pixels.
### Return value

Current engine window frame size in pixels.
## getEventUnstack () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## getEventStack () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## getEventUnstackMove () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## getEventItemDrop () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## getEventClose () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## getEventRestored () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## getEventMaximized () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## getEventMinimized () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## getEventHidden () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## getEventShown () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## getEventMouseLeave () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## getEventMouseEnter () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## getEventUnfocused () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## getEventFocused () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## getEventResized () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## getEventMoved () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## getEventFuncSwap () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## getEventFuncEndRender () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## getEventFuncEndRenderGui () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## getEventFuncBeginRenderGui () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## getEventFuncRender () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## getEventFuncBeginRender () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## getEventFuncUpdate () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## getEventWindowEvent () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
---

## void moveToCenter ( )

Positions the window so that the client center coincides with the center of the current display.
> **Notice:** This method should be applied to a separate or parent window, using this method for a nested window is not allowed.


## void setMinAndMaxSize ( ivec2 min_size , ivec2 max_size )

Sets the minimum and maximum possible window size when resizing the window.
> **Notice:** This method should be applied to a separate or parent window, using this method for a nested window is not allowed.


### Arguments

- *ivec2* **min_size** - The minimum possible size of the window.
- *ivec2* **max_size** - The maximum possible size of the window.

## int setIcon ( Image image )

Sets the icon for the window.
### Arguments

- *[Image](../../../api/library/common/class.image_usc.md)* **image** - The icon for the window.

### Return value

1 if the specified icon is successfully set for the window, otherwise 0.
## int getIcon ( Image image )

Gets the icon for the engine window and puts it to the specified target Image.
### Arguments

- *[Image](../../../api/library/common/class.image_usc.md)* **image** - Target image for the window icon.

### Return value

1 if the icon for the window is returned successfully, otherwise 0.
## void show ( )

Enables rendering of the engine window.
> **Notice:** This method should be applied to a separate or parent window, using this method for a nested window is not allowed.


## void hide ( )

Disables rendering of the engine window.
> **Notice:** This method should be applied to a separate or parent window, using this method for a nested window is not allowed.


## void setFocus ( )

Sets the focus to the window.
## void setSystemFocus ( )

Sets the focus to the engine window.
> **Notice:** This method is applied to a separate or parent window, for nested windows use [setFocus()](#setFocus_void).


## void minimize ( )

Minimizes the engine window to an iconic representation.
> **Notice:** This method should be applied to a separate or parent window, using this method for a nested window is not allowed.


## void maximize ( )

Makes the engine window as large as possible.
> **Notice:** This method should be applied to a separate or parent window, using this method for a nested window is not allowed.


## void restore ( )

Restores the size and position of the minimized or maximized engine window via the system proxy.
> **Notice:** This method should be applied to a separate or parent window, using this method for a nested window is not allowed.


## int getHitTestResult ( ivec2 global_pos )

Returns a value indicating in which area of the engine window the mouse is located.
> **Notice:** This method is used for interaction with system windows only, i.e. it cannot be used for nested windows.


### Arguments

- *ivec2* **global_pos** - Global coordinates of the hit-test point.

### Return value

Value indicating the window area, one of the [ENGINE_WINDOW_HITTEST_*](#HITTEST_NORMAL) values.
## string getHitTestResultName ( int hit_test )

Returns the string representation of the hit test result value.
### Arguments

- *int* **hit_test** - Value indicating the window area, one of the [ENGINE_WINDOW_HITTEST_*](#HITTEST_NORMAL) values.

### Return value

The string representation of the hit test result value (e.g., HITTEST_RESIZE_RIGHT is RESIZE RIGHT).
## void toTop ( )

Makes the window appear on top of all other windows.
> **Notice:** This method should be applied to a separate or parent window, using this method for a nested window is not allowed.


## int isGlobalChildOf ( EngineWindowGroup group )

Returns the value specifying if the current window is a part of a hierarchy of the specified window.
### Arguments

- *[EngineWindowGroup](../../../api/library/gui/class.enginewindowgroup_usc.md)* **group** - Window to be checked.

### Return value

**1** if the current window is globally a child of the specified one, otherwise **0**.
## void updateGuiHierarchy ( )

Updates the hierarchy for all widgets � the widgets are arranged, expanded to the required sizes and then their positions are updated. Updating the hierarchy may be required, for example, for getting the screen position immediately after the widget has been added to the hierarchy. For a separate window, the hierarchy in [self gui](#getSelfGui_Gui) is updated; for a nested window, the hierarchy in [self gui](#getSelfGui_Gui) of the global parent group is updated.
## string getDroppedItem ( int index )

Returns the absolute path to the file or folder dropped to the window.
### Arguments

- *int* **index** - Index of the dropped file or folder.

### Return value

Absolute path to the dropped file or folder.
## void screenshot ( string path )

Creates a screenshot after the rendering stage is completed.
> **Notice:** This method should be applied to a separate or parent window, using this method for a nested window is not allowed.


### Arguments

- *string* **path** - Path to save the screenshot.

## void setModal ( EngineWindow parent_window )

Sets the current window modal to the specified parent window. Both the parent and the child windows must be separate. The concept of **modal** assumes that if a window has modal children, it cannot be closed. Any other interaction with a parent window is possible.
> **Notice:** This method should be applied to a separate or parent window, a nested window can't be a parent for a modal window.


### Arguments

- *[EngineWindow](../../../api/library/gui/class.enginewindow_usc.md)* **parent_window** - Parent window.

## void addModalWindow ( EngineWindow window )

Adds the argument window as modal to the current window. Both the parent and the child windows must be separate. The concept of **modal** assumes that if a window has modal children, it cannot be closed. Any other interaction with a parent window is possible.
> **Notice:** This method should be applied to a separate or parent window, a nested window can't be a parent for a modal window.


### Arguments

- *[EngineWindow](../../../api/library/gui/class.enginewindow_usc.md)* **window** - Window to be added as modal.

## void removeModalWindow ( EngineWindow window )

Removes the argument modal window from this window. The concept of **modal** assumes that if a window has modal children, it cannot be closed. Any other interaction with a parent window is possible.
> **Notice:** This method should be applied to a separate or parent window, a nested window can't be a parent for a modal window.


### Arguments

- *[EngineWindow](../../../api/library/gui/class.enginewindow_usc.md)* **window** - Engine window.

## EngineWindow getModalWindow ( int index )

Returns the modal window for this window by its index. The concept of **modal** assumes that if a window has modal children, it cannot be closed. Any other interaction with a parent window is possible.
> **Notice:** This method should be applied to a separate or parent window, for a nested window it will return nullptr.


### Arguments

- *int* **index** - Index of the modal window.

### Return value

Modal window.
## void unstack ( )

Removes the current window from a parent group.
## void close ( )

Deletes the window if this window is not a [modal parent](#getModalParent_EngineWindow) or a member of a [fixed group](../../../api/library/gui/class.enginewindowgroup_usc.md#isFixed_int). If a window is a member of a fixed group, it cannot be closed (i.e. deleted).
## int getIntersection ( ivec2 global_mouse_pos )

Returns the value indicating if the mouse is hovering over the window.
### Arguments

- *ivec2* **global_mouse_pos** - Global screen coordinates of the mouse relative to the main display.

### Return value

**1** if the mouse hovers over the current window, otherwise **0**.
## int getClientIntersection ( ivec2 global_mouse_pos )

### Arguments

- *ivec2* **global_mouse_pos** - Global screen coordinates of the mouse relative to the main display.

### Return value

**1** if the mouse hovers over the client area of the window, otherwise **0**.
## int getClient9Area ( ivec2 global_mouse_pos )

Returns the area over which the mouse hovers, one of the nine areas into which the window is segmented.
### Arguments

- *ivec2* **global_mouse_pos** - Global screen coordinates of the mouse relative to the main display.

### Return value

One of the nine segments the screen area is split into.
## string get9AreaName ( int area )

Returns the name of the screen segment as a string.
### Arguments

- *int* **area** - One of the nine segments the screen area is split into.

### Return value

The string representation of the segment value (e.g., AREA_TOP_LEFT is TOP LEFT).
## ivec2 globalToLocalUnitPosition ( ivec2 global_pos )

Transforms the global screen coordinates in pixels into [logical units](../../../principles/dpi/index.md) relative to the window client area.
### Arguments

- *ivec2* **global_pos** - The position in global coordinates.

### Return value

The coordinates in [logical units](../../../principles/dpi/index.md) relative to the window client area.
## ivec2 localUnitToGlobalPosition ( ivec2 unit_pos )

Transforms the position in [logical units](../../../principles/dpi/index.md) relative to the window client area into the global screen coordinates in pixels.
### Arguments

- *ivec2* **unit_pos** - The coordinates in [logical units](../../../principles/dpi/index.md) relative to the window client area.

### Return value

The position in global coordinates.
