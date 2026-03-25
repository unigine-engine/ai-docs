# Unigine::CustomSystemProxy Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


This class is used for integration with third-party systems (for example, *Qt, SDL, WPF*). Most of its functions are virtual, so you need to override them when implementing your application.


### See Also


## CustomSystemProxy Class

### Members

---

## CustomSystemProxy ( int features )

Constructor. Creates an instance of the CustomSustemProxy class and specifies the [supported features](#SYSTEM_PROXY_WINDOWS) (mouse, keyboard, joystick, etc.).
### Arguments

- *int* **features** - Supported features.

## int getFeatures ( )

Returns the set of features CustomSystemProxy can perform.
### Return value

Mask specifying the set of [CUSTOMSYSTEMPROXY_SYSTEM_PROXY_*](#SYSTEM_PROXY_WINDOWS) features CustomSystemProxy can perform.
## isWindowsSupported ( )

Returns the value indicating if CustomSystemProxy supports windows creation.
### Return value

true if CustomSystemProxy supports windows creation, otherwise false.
## isMouseSupported ( )

Returns the value indicating if CustomSystemProxy supports work with the mouse.
### Return value

true if CustomSystemProxy supports work with the mouse, otherwise false.
## isKeyboardSupported ( )

Returns the value indicating if CustomSystemProxy supports work with the keyboard.
### Return value

true if CustomSystemProxy supports work with the keyboard, otherwise false.
## isTouchesSupported ( )

Returns the value indicating if CustomSystemProxy supports work with the sensor input.
### Return value

true if CustomSystemProxy supports work with the sensor input, otherwise false.
## isDisplaysSupported ( )

Returns the value indicating if CustomSystemProxy can provide information on displays.
### Return value

true if CustomSystemProxy can provide information on displays, otherwise false.
## isJoysticksSupported ( )

Returns the value indicating if CustomSystemProxy supports work with the joystick input.
### Return value

true if CustomSystemProxy supports work with the joystick input, otherwise false.
## isGamepadsSupported ( )

Returns the value indicating if CustomSystemProxy supports work with the gamepad input.
### Return value

true if CustomSystemProxy supports work with the gamepad input, otherwise false.
## void setWindowFocus ( WIN_HANDLE win_handle )

Sets the focus to the engine window.
### Arguments

- *WIN_HANDLE* **win_handle** - Engine window handle.

## void setWindowMouseGrab ( WIN_HANDLE win_handle , bool state )

Sets a value indicating if the mouse pointer is bound to the window.
### Arguments

- *WIN_HANDLE* **win_handle** - Engine window handle.
- *bool* **state** - true if the mouse cannot leave the window; otherwise, **false**.

## void setWindowResizable ( WIN_HANDLE win_handle , bool state )

Sets a value indicating if the window can be resized.
### Arguments

- *WIN_HANDLE* **win_handle** - Engine window handle.
- *bool* **state** - true if the window can be resized; otherwise, **false**.

## void setWindowBordered ( WIN_HANDLE win_handle , bool state )

Sets a value indicating if the window has borders.
### Arguments

- *WIN_HANDLE* **win_handle** - Engine window handle.
- *bool* **state** - true if the window has borders; otherwise, **false**.

## void disableWindowFullscreen ( WIN_HANDLE win_handle )

Disables the fullscreen mode for the window with the specified handle and returns it to window mode.
### Arguments

- *WIN_HANDLE* **win_handle** - Engine window handle.

## bool enableWindowFullscreen ( WIN_HANDLE win_handle , int display , int mode )

Maximizes the window with the specified handle to the fullscreen mode on the specified display with the specified mode.
### Arguments

- *WIN_HANDLE* **win_handle** - Engine window handle.
- *int* **display** - Display index.
- *int* **mode** - Mode index.

### Return value

true if the window with the specified handle is successfully maximized to the fullscreen mode on the specified display with the specified mode; otherwise, false.
## void minimizeWindow ( WIN_HANDLE win_handle )

Minimizes the window to tray.
### Arguments

- *WIN_HANDLE* **win_handle** - Engine window handle.

## void maximizeWindow ( WIN_HANDLE win_handle )

Maximizes the window to the whole screen.
### Arguments

- *WIN_HANDLE* **win_handle** - Engine window handle.

## void restoreWindow ( WIN_HANDLE win_handle )

Restores the window from the minimized or maximized state.
### Arguments

- *WIN_HANDLE* **win_handle** - Engine window handle.

## int getWindowDisplayIndex ( WIN_HANDLE win_handle )

Returns the index of the display in which the window is rendered.
### Arguments

- *WIN_HANDLE* **win_handle** - Engine window handle.

### Return value

Display index.
## ivec2 getGlobalMousePosition ( )

Returns the mouse position in global coordinates relative to the main system display.
### Return value

Mouse position in global coordinates.
## void showCursor ( bool state )

Sets a value indicating if the cursor is shown.
### Arguments

- *bool* **state** - true to show the cursor, false to hide it.

## void showMouseCursorSystemArrow ( )

Sets the system arrow as the mouse cursor.
## void setMouseCursorSkinCustom ( )

Sets the specified [skin image](../../../code/gui/skin/index.md#gui_mouse_layout) as the mouse cursor.
### Arguments

## int getDisplayDefaultSystemDPI ( )

Returns the default system dots/pixels-per-inch value.
### Return value

Dots/pixels-per-inch value.
## int getNumDisplays ( )

Returns the total number of displays.
### Return value

Number of displays.
## ivec2 getDisplayPosition ( int display_index )

Returns the position of the specified display.
### Arguments

- *int* **display_index** - Display index.

### Return value

Display position.
## ivec2 getDisplayResolution ( int display_index )

Returns the resolution of the specified display.
### Arguments

- *int* **display_index** - Display index.

### Return value

Display resolution.
## int getDisplayDPI ( int display_index )

Returns the DPI of the specified display.
### Arguments

- *int* **display_index** - Display index.

### Return value

Display DPI.
## int getMainDisplay ( )

Returns the index of the main display.
### Return value

Display index.
## int getDisplayNumModes ( int display_index )

Returns the total number of available display modes.
### Arguments

- *int* **display_index** - Display index.

### Return value

Number of available display modes.
## ivec2 getDisplayModeResolution ( int display_index , int mode_index )

Returns the DPI of the specified mode for the selected display.
### Arguments

- *int* **display_index** - Display index.
- *int* **mode_index** - Index of the display mode.

### Return value

Display DPI.
## int getDisplayModeRefreshRate ( int display_index , int mode_index )

Returns the refresh rate of the specified display mode.
### Arguments

- *int* **display_index** - Display index.
- *int* **mode_index** - Index of the display mode.

### Return value

Refresh rate of the specified display mode.
## getDisplayName ( int display_index )

Returns the system name of the specified display.
### Arguments

- *int* **display_index** - Display index.

### Return value

Display name.
## bool hasClipboardText ( )

Returns the value showing if the clipboard contains anything.
### Return value

true if there is text in the clipboard, otherwise false.
## void setClipboardText ( )

Updates the contents of the system clipboard.
### Arguments

## getClipboardText ( )

Retrieves the contents of the system clipboard.
### Return value

Contents of the system clipboard.
## bool showDialogMessage ( WIN_HANDLE parent_window_handle )

Displays a message dialog with the specified title and text.
### Arguments

- *WIN_HANDLE* **parent_window_handle** - Handle of the parent window.

### Return value

true if the dialog message is displayed successfully, otherwise false.
## bool showDialogWarning ( WIN_HANDLE parent_window_handle )

Displays a warning dialog with the specified title and text.
### Arguments

- *WIN_HANDLE* **parent_window_handle** - Handle of the parent window.

### Return value

true if the dialog warning is displayed successfully, otherwise false.
## bool showDialogError ( WIN_HANDLE parent_window_handle )

Displays an error dialog with the specified title and text.
### Arguments

- *WIN_HANDLE* **parent_window_handle** - Handle of the parent window.

### Return value

true if the dialog error is displayed successfully, otherwise false.
## bool needRenderExternalWindow ( WIN_HANDLE win_handle )

Checks rendering of the external window. If the window is minimized, occluded by other windows and so on, this information can be passed to the Engine (to stop rendering, for example).
### Arguments

- *WIN_HANDLE* **win_handle** - Handle of the external window into which the image is rendered.

### Return value

true if the window is rendered, otherwise, false.
## void setWindowModal ( WIN_HANDLE win_handle , WIN_HANDLE parent_handle )

Sets the window as a modal for the parent window.
### Arguments

- *WIN_HANDLE* **win_handle** - Window to be set modal.
- *WIN_HANDLE* **parent_handle** - Parent window for the modal window.

## void setWindowAlwaysOnTop ( WIN_HANDLE win_handle , bool state )

Places the window above all other windows. The window maintains its topmost position even when it is deactivated.
### Arguments

- *WIN_HANDLE* **win_handle** - Window to be set modal.
- *bool* **state** - true to make the engine window topmost, false to set the default engine window behavior.

## int getJoystickPlayerIndex ( )

Returns the joystick player index.
### Arguments

### Return value

Player index.
## int getJoystickDeviceType ( )

Returns the type of the joystick.
### Arguments

### Return value

Joystick type.
## int getJoystickVendor ( )

Returns the vendor ID of the joystick.
### Arguments

### Return value

Joystick vendor ID.
## int getJoystickProduct ( )

Returns the product ID of the joystick.
### Arguments

### Return value

Joystick product ID.
## int getJoystickProductVersion ( )

Returns the product version of the joystick.
### Arguments

### Return value

Joystick product version.
## getJoystickName ( )

Returns the name of the joystick.
### Arguments

### Return value

Joystick name.
## getJoystickModelGUID ( )

Returns the name of the joystick.
### Arguments

### Return value

Model GUID of the joystick.
## int getJoystickNumButtons ( )

Returns the number of the joystick buttons.
### Arguments

### Return value

Number of buttons.
## int getJoystickNumAxes ( )

Returns the number of the joystick axes.
### Arguments

### Return value

Number of axes.
## int getJoystickNumPovs ( )

Returns the number of the joystick POV hats.
### Arguments

### Return value

Number of POV hats.
## float getJoystickAxisInitValue ( int axis )

Returns the initial value of the joystick axis control.
### Arguments

- *int* **axis** - Axis index.

### Return value

Initial value of the axis control.
## int getGamepadPlayerIndex ( )

Returns the player index of the gamepad.
### Arguments

### Return value

Player index.
## int getGamepadDeviceType ( )

Returns the type of the gamepad.
### Arguments

### Return value

Gamepad type.
## int getGamepadModelType ( )

Returns the model type of the joystick.
### Arguments

### Return value

Model type.
## getGamepadName ( )

Return the name of the gamepad.
### Arguments

### Return value

Gamepad name.
## getGamepadModelGUID ( )

Returns the model GUID of the gamepad.
### Arguments

### Return value

Model GUID.
## int getDisplayRefreshRate ( int display_index )

Returns the refresh rate of the display.
### Arguments

- *int* **display_index** - Display index.

### Return value

Refresh rate.
## int getDisplayCurrentMode ( int display_index )

Returns the number of the current display mode.
### Arguments

- *int* **display_index** - Display index.

### Return value

Number of the current display mode.
## int getDisplayDesktopMode ( int display_index )

Returns the number of the desktop's display mode.
### Arguments

- *int* **display_index** - Display index.

### Return value

Number of the desktop's display mode.
## int getDisplayOrientation ( int display_index )

Returns the orientation of the display.
### Arguments

- *int* **display_index** - Display index.

### Return value

Display orientation.
