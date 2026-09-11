# Unigine::WindowManager Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

> **Notice:** This class is a singleton.


The class to manage windows enabling you to access any window of the appllication, group or stack windows, create various dialogs and so on.


### Accessing Windows


### Grouping Windows


The engine windows created via the *[EngineWindow](../../../api/library/gui/class.enginewindow_usc.md)* class can be grouped. There are three types of the **window groups**:


- Vertical
- Horizontal
- Group of tabs


The number of windows in the group is unlimited.


### Creating Dialog Windows


## WindowManager Class

### Members

## EngineWindowViewport getMainWindow () const

Returns the current window viewport that is set as the main window by default.
> **Notice:** There may be several windows that are set as main, or no main windows at all.


### Return value

Current engine window viewport.
## int getNumWindows () const

Returns the current number of windows.
### Return value

Current number of windows.
## bool isFullscreenMode () const

Returns the current value indicating if the window is the fullscreen state, or in the window mode.
### Return value

**true** if the window is the fullscreen state; otherwise **false**.
## bool isMultipleWindowsSupported () const

Returns the current value indicating if the engine can create more than one window.
### Return value

**true** if multiple windows are supported; otherwise **false**.
## getFocusedWindow () const

Returns the current window viewport which is currently in focus.
### Return value

Current window viewport which is currently in focus.
## getUnderCursorWindow () const

Returns the current window viewport which is currently under cursor.
### Return value

Current window viewport which is currently under cursor.
## getSystemFocusedWindow () const

Returns the current
### Return value

Current
## bool isAutoDpiScaling () const

Returns the current value specifying if automatic DPI scaling is applied to the window. If automatic DPI scaling is disabled, all GUI elements have the 100% size, only the system window size is scaled.
> **Notice:** This value is stored in the boot config file and can be changed only at the application startup. It cannot be changed at runtime, thus at an attempt to change the value the console will show the corresponding warning.


### Return value

**true** if all GUI elements of the window are scaled is enabled ; otherwise **false**.
## getDpiAwareness () const

Returns the current DPI awareness mode, the value indicating how the application processes the DPI scaling. The value is set to [PER_MONITOR_AWARE](#DPI_AWARENESS_PER_MONITOR_AWARE) by default. On Windows, if a specified mode cannot be set, it will switch to a possible lower value with a corresponding warning. On Linux, [PER_MONITOR_AWARE](#DPI_AWARENESS_PER_MONITOR_AWARE) is currently not supported, setting this value will switch the mode to the [SYSTEM_AWARE](#DPI_AWARENESS_SYSTEM_AWARE) mode with the corresponding warning in the console.
> **Notice:** This value is stored in the boot config file and can be changed only at the application startup. It cannot be changed at runtime, thus at an attempt to change the value the console will show the corresponding warning.


### Return value

Current DPI awareness mode, the value indicating how the application processes the DPI scaling.
## getCurrentDpiAwareness () const

Returns the current actual DPI awareness mode, the value indicating how the application processes the DPI scaling. The value is set to [PER_MONITOR_AWARE](#DPI_AWARENESS_PER_MONITOR_AWARE) by default. On Windows, if a specified mode cannot be set, it will switch to a possible lower value with a corresponding warning. On Linux, [PER_MONITOR_AWARE](#DPI_AWARENESS_PER_MONITOR_AWARE) is currently not supported, setting this value will switch the mode to the [SYSTEM_AWARE](#DPI_AWARENESS_SYSTEM_AWARE) mode with the corresponding warning in the console.
> **Notice:** This is an actual value, it may differ from the mode stored in the boot config file (in case the system cannot set the specified mode it will try to use the one that is suitable instead).


### Return value

Current actual DPI awareness mode
## static getEventImmediateWindowEvent () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static getEventWindowUnstacked () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static getEventWindowStacked () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static getEventWindowRemoved () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static getEventWindowCreated () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## getFullscreenWindow () const

Returns the current first engine window viewport that is in the fullscreen state.
### Return value

Current first engine window viewport that is in the fullscreen state, or NULL if none
---

## EngineWindow getWindow ( int index )

Returns the window by its index.
### Arguments

- *int* **index** - Index of the window.

### Return value

Engine window.
## int getWindowIndex ( EngineWindow window )

Returns the index of the specified window.
### Arguments

- *[EngineWindow](../../../api/library/gui/class.enginewindow_usc.md)* **window** - Engine window.

### Return value

Index of the window.
## EngineWindowGroup stack ( EngineWindow first_window , EngineWindow second_window , int group_type , int index = -1 , int decompose_second = false )

### Arguments

- *[EngineWindow](../../../api/library/gui/class.enginewindow_usc.md)* **first_window** - The parent window to which another window is stacked.
- *[EngineWindow](../../../api/library/gui/class.enginewindow_usc.md)* **second_window** - The window to be stacked.
- *int* **group_type** - Type of a group to be created.
- *int* **index**
- *int* **decompose_second** - Flag to decompose the second argument of the merge, if it is a group, and combine with the first group.

### Return value

Group of stacked windows.
## EngineWindowGroup stackToParentGroup ( EngineWindow window_in_group , EngineWindow window , int index = -1 , int decompose_second = false )

### Arguments

- *[EngineWindow](../../../api/library/gui/class.enginewindow_usc.md)* **window_in_group** - The window into the parent group of which the other window is stacked.
- *[EngineWindow](../../../api/library/gui/class.enginewindow_usc.md)* **window** - The window to be stacked.
- *int* **index** - A place where a window or a group should be placed in a group.
- *int* **decompose_second** - Flag to decompose the second argument of the merge, if it is a group, and combine with the first window or a group.

### Return value

Group of windows.
## EngineWindowGroup stackWindows ( EngineWindowViewport first_viewport , EngineWindowViewport second_viewport , int group_type = Enum.EngineWindowGroup.GROUP_TYPE.TAB )

### Arguments

- *[EngineWindowViewport](../../../api/library/gui/class.enginewindowviewport_usc.md)* **first_viewport** - The window to be stacked.
- *[EngineWindowViewport](../../../api/library/gui/class.enginewindowviewport_usc.md)* **second_viewport** - The window to be stacked.
- *int* **group_type** - Type of a group to be created.

### Return value

Group of windows.
## EngineWindowGroup stackWithWindow ( EngineWindowViewport window_viewport , EngineWindow window , int group_type , int decompose_second = false )

Returns a newly created group of the engine window viewport and any other engine window � another viewport or a window group.
### Arguments

- *[EngineWindowViewport](../../../api/library/gui/class.enginewindowviewport_usc.md)* **window_viewport** - The window viewport to be stacked.
- *[EngineWindow](../../../api/library/gui/class.enginewindow_usc.md)* **window** - The window to be stacked.
- *int* **group_type** - Type of a window group to be created.
- *int* **decompose_second** - Flag to decompose the second argument of the merge, if it is a group, and combine with the first group.

### Return value

Group of windows.
## EngineWindowGroup stackGroups ( EngineWindowGroup first_group , EngineWindowGroup second_group , int group_type )

### Arguments

- *[EngineWindowGroup](../../../api/library/gui/class.enginewindowgroup_usc.md)* **first_group** - The first window group for merging.
- *[EngineWindowGroup](../../../api/library/gui/class.enginewindowgroup_usc.md)* **second_group** - The second window group for merging.
- *int* **group_type** - Type of a group to be created.

### Return value

Group of windows.
## EngineWindowGroup stackToGroup ( EngineWindowGroup destination_group , EngineWindow group , int index = -1 , int decompose_second = false )

### Arguments

- *[EngineWindowGroup](../../../api/library/gui/class.enginewindowgroup_usc.md)* **destination_group** - The parent group to which another group is stacked.
- *[EngineWindow](../../../api/library/gui/class.enginewindow_usc.md)* **group** - The window or window group to be stacked.
- *int* **index** - A place where a window or a group should be placed in a group.
- *int* **decompose_second** - Flag to decompose the second argument of the merge and combine with the first group.

### Return value

Group of stacked windows.
## void unstack ( EngineWindow unstacked )

Removes a window or a group from a parent group. If there is only one window left, the group is automatically deleted after removing the window from it.
### Arguments

- *[EngineWindow](../../../api/library/gui/class.enginewindow_usc.md)* **unstacked** - A window or a group to be removed from a parent group.

## int isFullscreenWindow ( EngineWindow window )

Returns the value indicating if the specified window is in a fullscreen state.
### Arguments

- *[EngineWindow](../../../api/library/gui/class.enginewindow_usc.md)* **window** - The window to be checked.

### Return value

**1** if the engine window is the fullscreen state, **0** if it is in the window mode.
## EngineWindow getWindowByID ( long win_id )

Returns the window by its ID.
### Arguments

- *long* **win_id** - Window ID.

### Return value

Window with the specified ID, or null if the window is not found.
## int dialogMessage ( string title , string message )

Displays a message dialog with the specified title and text.
### Arguments

- *string* **title** - Title of the message dialog to be displayed.
- *string* **message** - Message text to be displayed.

### Return value

**1** if the message is displayed successfully; otherwise, **0**.
## int dialogWarning ( string title , string warning )

Displays a warning dialog with the specified title and text.
### Arguments

- *string* **title** - Title of the warning dialog to be displayed.
- *string* **warning** - Warning message text to be displayed.

### Return value

**1** if the message is displayed successfully; otherwise, **0**.
## int dialogError ( string title , string error )

Displays an error dialog with the specified title and text.
### Arguments

- *string* **title** - Title of the error dialog to be displayed.
- *string* **error** - Error message text to be displayed.

### Return value

**1** if the message is displayed successfully; otherwise, **0**.
## int showSystemDialog ( SystemDialog dialog )

Displays a custom [system dialog](../../../api/library/engine/class.systemdialog_usc.md) with an arbitrary set of buttons.
### Arguments

- *[SystemDialog](../../../api/library/engine/class.systemdialog_usc.md)* **dialog** - [*SystemDialog*](../../../api/library/engine/class.systemdialog_usc.md) class instance representing the custom system dialog to be shown.

### Return value

Number of the dialog button clicked by the user; or **-1** if an error has occurred.
## string dialogOpenFolder ( string path )

Opens a common dialog enabling the user to specify a folder to open. When the dialog opens the specified default path shall be set displaying the corresponding elements.
### Arguments

- *string* **path** - Path to be set by default when the dialog opens.

### Return value

Resulting folder name specified by the user.
## string dialogOpenFolder ( )

Opens a common dialog enabling the user to specify a folder to open.
### Return value

Resulting folder name specified by the user.
## string dialogOpenFile ( string path , string filter )

Opens a common dialog enabling the user to specify a filename to open a file. When the dialog opens the specified default path and file filter shall be set displaying the corresponding elements.
### Arguments

- *string* **path** - Path to be set by default when the dialog opens.
- *string* **filter** - File name filter string to be set by default when the dialog opens. This filter string determines file type choices to be displayed in the *Files of type* box.

### Return value

Resulting filename specified by the user.
## string dialogOpenFile ( string path )

Opens a common dialog enabling the user to specify a filename to open a file. When the dialog opens the specified default path shall be set displaying the corresponding elements.
### Arguments

- *string* **path** - Path to be set by default when the dialog opens.

### Return value

Resulting filename specified by the user.
## string dialogOpenFile ( )

Opens a common dialog enabling the user to specify a filename to open a file.
### Return value

Resulting filename specified by the user.
## string dialogSaveFile ( string path , string filter )

Opens a common dialog enabling the user to specify a filename to save a file as. When the dialog opens the specified default path and file filter shall be set displaying the corresponding elements.
### Arguments

- *string* **path** - Path to be set by default when the dialog opens.
- *string* **filter** - File name filter string to be set by default when the dialog opens. This filter string determines file type choices to be displayed in the *Save as file type* or *Files of type* box.

### Return value

Resulting filename specified by the user.
## string dialogSaveFile ( string path )

Opens a common dialog enabling the user to specify a filename to save a file as. When the dialog opens the specified default path shall be set displaying the corresponding elements.
### Arguments

- *string* **path** - Path to be set by default when the dialog opens.

### Return value

Resulting filename specified by the user.
## string dialogSaveFile ( )

Opens a common dialog enabling the user to specify a filename to save a file as.
### Return value

Resulting filename specified by the user.
## void forceUpdateWindowOrders ( )

Updates the Z order of all windows.
> **Notice:** It is recommended to use this method only when required, because it is very slow.


## void setEventsFilter ( IntPtr func )

Sets a callback function to be executed on receiving input events. This input event filter enables you to reject certain input events for the Engine and get necessary information on all input events.
### Arguments

- *IntPtr* **func** - Input event callback.
