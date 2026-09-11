# Unigine::CustomSystemProxy Class (CPP)

**Header:** #include <UnigineCustomSystemProxy.h>


This class is used for integration with third-party systems (for example, *Qt, SDL, WPF*). Most of its functions are virtual, so you need to override them when implementing your application.


In general, the *CustomSystemProxy*-based workflow is the following:


1. Include the `UnigineCustomSystemProxy.h` header file into the source code.
2. Create a custom class and inherit it from the *Unigine::CustomSystemProxy* class.
3. Override all of the virtual functions specified in the `include/UnigineCustomSystemProxy.h` file.
4. Define the supported features via the proxy constructor (the *[SYSTEM_PROXY_*](../../../api/library/engine/class.customsystemproxy_cpp.md#SYSTEM_PROXY_WINDOWS)* variables).
5. Implement the functions according to the list of the supported features, including [event handling](../../../code/cpp/usage/unigine_app/proxy.md#event_handling) and [rendering into an external window](../../../code/cpp/usage/unigine_app/proxy.md#external_window), if required.


> **Notice:** The full-featured example of integrating UNIGINE Engine into the QT framework can be found in the `source/apps/main_qt` folder (`SystemProxyQt.h`, `SystemProxyQt.cpp`).


The following code is the part of the *SystemProxyQt* example:


<details>
<summary>SystemProxyQt.h | Close</summary>

```cpp
// include the header file
#include <UnigineCustomSystemProxy.h>
#include <UnigineVector.h>

...

// create a custom class and inherit it from CustomSystemProxy
class SystemProxyQt final : public Unigine::CustomSystemProxy
{

public:

	SystemProxyQt();
	~SystemProxyQt() override;

// override the required virtual functions
protected:

	// main thread
	bool isEngineActive() override;
	void mainUpdate() override {}

	// windows (check support for create and remove only)
	Unigine::WIN_HANDLE createWindow(int width, int height) override;
	void removeWindow(Unigine::WIN_HANDLE win_handle) override;
	void setWindowTitle(Unigine::WIN_HANDLE win_handle, const char *title) override;
	void setWindowIcon(Unigine::WIN_HANDLE win_handle, const Unigine::ImagePtr &image) override;

	...

	// displays
	int getDisplayDefaultSystemDPI() const override;
	int getNumDisplays() const override;

	...

	// joysticks
	void getConnectedJoysticks(Unigine::Vector<int32_t> &connected_ids) override {}
	int getJoystickPlayerIndex(int32_t joy_id) const override { return -1; }
	int getJoystickDeviceType(int32_t joy_id) const override { return -1; }

	...

	// gamepads
	void getConnectedGamepads(Unigine::Vector<int32_t> &connected_ids) override {}

	...

	// other
	bool hasClipboardText() const override;

	...
}

```

</details>


<details>
<summary>SystemProxyQt.cpp | Close</summary>

```cpp
// ...

using namespace Unigine;

// create a proxy that can work with the mouse and keyboard and create windows
SystemProxyQt::SystemProxyQt()
	: CustomSystemProxy(SYSTEM_PROXY_WINDOWS | SYSTEM_PROXY_MOUSE | SYSTEM_PROXY_KEYBOARD)
{
	timestamp_timer_.begin();
}

SystemProxyQt::~SystemProxyQt()
{
	assert(external_windows_.empty());
	assert(window_by_id_.empty());
	window_by_id_.clear();
}

// functions implementation (window creation, events processing, rendering into an external window, etc.)
// ...

```

</details>


### See Also


- The [Integrating with Frameworks](../../../code/cpp/usage/unigine_app/proxy.md) article


## CustomSystemProxy Class

### Members

---

## CustomSystemProxy ( int features )

Constructor. Creates an instance of the CustomSustemProxy class and specifies the [supported features](#SYSTEM_PROXY_WINDOWS) (mouse, keyboard, joystick, etc.).
### Arguments

- *int* **features** - Supported features.

## CustomSystemProxy * get ( )

Returns the CustomSystemProxy instance.
### Return value

CustomSystemProxy instance.
## int getFeatures ( ) const

Returns the set of features CustomSystemProxy can perform.
### Return value

Mask specifying the set of [SYSTEM_PROXY_*](#SYSTEM_PROXY_WINDOWS) features CustomSystemProxy can perform.
## bool isWindowsSupported ( ) const

Returns the value indicating if CustomSystemProxy supports windows creation.
### Return value

true if CustomSystemProxy supports windows creation, otherwise false.
## bool isMouseSupported ( ) const

Returns the value indicating if CustomSystemProxy supports work with the mouse.
### Return value

true if CustomSystemProxy supports work with the mouse, otherwise false.
## bool isKeyboardSupported ( ) const

Returns the value indicating if CustomSystemProxy supports work with the keyboard.
### Return value

true if CustomSystemProxy supports work with the keyboard, otherwise false.
## bool isTouchesSupported ( ) const

Returns the value indicating if CustomSystemProxy supports work with the sensor input.
### Return value

true if CustomSystemProxy supports work with the sensor input, otherwise false.
## bool isDisplaysSupported ( ) const

Returns the value indicating if CustomSystemProxy can provide information on displays.
### Return value

true if CustomSystemProxy can provide information on displays, otherwise false.
## bool isJoysticksSupported ( ) const

Returns the value indicating if CustomSystemProxy supports work with the joystick input.
### Return value

true if CustomSystemProxy supports work with the joystick input, otherwise false.
## bool isGamepadsSupported ( ) const

Returns the value indicating if CustomSystemProxy supports work with the gamepad input.
### Return value

true if CustomSystemProxy supports work with the gamepad input, otherwise false.
## bool initExternalWindowBuffers ( WIN_HANDLE win_handle , const ivec2& size )

Initialization of the resources for rendering to the external window.
### Arguments

- *WIN_HANDLE* **win_handle** - Window handle.
- *const ivec2&* **size** - Window size.

### Return value

true if the operation is successful, otherwise false.
## bool resizeExternalWindowBuffers ( WIN_HANDLE win_handle , const ivec2& size )

Resizing of the external window in order to update the internal textures.
### Arguments

- *WIN_HANDLE* **win_handle** - Window handle.
- *const ivec2&* **size** - Window size.

### Return value

true if the operation is successful, otherwise false.
## bool shutdownExternalWindowBuffers ( WIN_HANDLE win_handle )

Shutdown of all resources required for rendering to the external window upon closing the window.
### Arguments

- *WIN_HANDLE* **win_handle** - Window handle.

### Return value

true if the operation is successful, otherwise false.
## void onExternalWindowRender ( WIN_HANDLE win_handle )

Rendering into the specified external window.
### Arguments

- *WIN_HANDLE* **win_handle** - Handle of the window into which the image is rendered.

## void invokeWindowEvent ( WindowEvent Ptr e )

Conveys the window event to Window Manager.
### Arguments

- *[WindowEvent](../../../api/library/gui/class.windowevent_cpp.md)Ptr* **e** - Window event.

## void invokeInputEvent ( InputEvent Ptr e )

Conveys the input event to Window Manager.
### Arguments

- *[InputEvent](../../../api/library/controls/class.inputevent_cpp.md)Ptr* **e** - Input event.

## void mainUpdate ( )

Callback from the main thread before the update.
## WIN_HANDLE createWindow ( int width , int height )

Returns the engine handle of the created window.
### Arguments

- *int* **width** - Window width.
- *int* **height** - Window height.

### Return value

Engine window handle.
## void removeWindow ( WIN_HANDLE win_handle )

Destroys the window using its handle.
### Arguments

- *WIN_HANDLE* **win_handle** - Engine window handle.

## void setWindowTitle ( WIN_HANDLE win_handle , const char* title )

Sets the window title.
### Arguments

- *WIN_HANDLE* **win_handle** - Engine window handle.
- *const char** **title** - Window title.

## void setWindowIcon ( WIN_HANDLE win_handle , const ImagePtr& image )

Sets the window icon.
### Arguments

- *WIN_HANDLE* **win_handle** - Engine window handle.
- *const ImagePtr&* **image** - Image to be used as the icon.

## void setWindowSize ( WIN_HANDLE win_handle , const ivec2& size )

Sets the window size.
### Arguments

- *WIN_HANDLE* **win_handle** - Engine window handle.
- *const ivec2&* **size** - Window size (width and height).

## void setWindowMinSize ( WIN_HANDLE win_handle , const ivec2& size )

Sets the minimum possible size of the window.
### Arguments

- *WIN_HANDLE* **win_handle** - Engine window handle.
- *const ivec2&* **size** - Window size (width and height).

## void setWindowMaxSize ( WIN_HANDLE win_handle , const ivec2& size )

Sets the maximum possible size of the window.
### Arguments

- *WIN_HANDLE* **win_handle** - Engine window handle.
- *const ivec2&* **size** - Window size (width and height).

## void setWindowPosition ( WIN_HANDLE win_handle , const ivec2& pos )

Sets the window position (top left corner) in screen coordinates.
### Arguments

- *WIN_HANDLE* **win_handle** - Engine window handle.
- *const ivec2&* **pos** - Window position.

## void showWindow ( WIN_HANDLE win_handle )

Renders the window.
### Arguments

- *WIN_HANDLE* **win_handle** - Engine window handle.

## void hideWindow ( WIN_HANDLE win_handle )

Hides the window.
### Arguments

- *WIN_HANDLE* **win_handle** - Engine window handle.

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

## void setWindowOpacity ( WIN_HANDLE win_handle , float opacity )

Sets the window opacity.
### Arguments

- *WIN_HANDLE* **win_handle** - Engine window handle.
- *float* **opacity** - Window opacity.

## int getWindowDisplayIndex ( WIN_HANDLE win_handle ) const

Returns the index of the display in which the window is rendered.
### Arguments

- *WIN_HANDLE* **win_handle** - Engine window handle.

### Return value

Display index.
## ivec4 getWindowSystemBorderSize ( WIN_HANDLE win_handle )

Returns the size of the system window borders.
### Arguments

- *WIN_HANDLE* **win_handle** - Engine window handle.

### Return value

Size of the system window borders.
## int getHitTestAreaIntersection ( uint64_t win_handle , int global_pos_x , int global_pos_y )

Returns a value indicating if intersection of the cursor with the window drag area is detected.
### Arguments

- *uint64_t* **win_handle** - Engine window handle.
- *int* **global_pos_x** - X coordinate of the cursor in global coordinates.
- *int* **global_pos_y** - Y coordinate of the cursor in global coordinates.

### Return value

1 if intersection is detected; otherwise 0.
## void setGlobalMousePosition ( const ivec2& pos )

Sets the mouse position in global coordinates relative to the main system display.
### Arguments

- *const ivec2&* **pos** - Mouse position in global coordinates.

## ivec2 getGlobalMousePosition ( ) const

Returns the mouse position in global coordinates relative to the main system display.
### Return value

Mouse position in global coordinates.
## void showCursor ( bool state )

Sets a value indicating if the cursor is shown.
### Arguments

- *bool* **state** - true to show the cursor, false to hide it.

## void showMouseCursorSystemArrow ( )

Sets the system arrow as the mouse cursor.
## void setMouseCursorSkinCustom ( const ImagePtr& mouse_skin )

Sets the specified [skin image](../../../code/gui/skin/index.md#gui_mouse_layout) as the mouse cursor.
### Arguments

- *const ImagePtr&* **mouse_skin** - [Image](../../../code/gui/skin/index.md#gui_mouse_layout) containing pointer shapes to be set for the mouse cursor (e.g., select, move, resize, etc.).

## void setMouseCursorSkinSystem ( )

Sets the current OS cursor skin (pointer shapes like select, move, resize, etc.).
## void setMouseCursorCustom ( const ImagePtr& image , int x , int y )

Sets a custom image for the OS mouse cursor. The image must be of the square size and *RGBA8* format. This method of setting cursor has the priority over other cursor setting methods. The image set by this method can be cleared only using the [clearMouseCursorCustom()](#clearMouseCursorCustom_void) method.
### Arguments

- *const ImagePtr&* **image** - [Image](../../../code/gui/skin/index.md#gui_mouse_layout) containing pointer shapes to be set for the mouse cursor (e.g., select, move, resize, etc.).
- *int* **x** - X coordinate of the cursor's hot spot.
- *int* **y** - Y coordinate of the cursor's hot spot.

## void clearMouseCursorCustom ( )

Clears the custom mouse cursor set via the [setMouseCursorCustom()](#setMouseCursorCustom_const_ImagePtr_ref_int_int_void) method.
## void changeMouseCursorSkinNumber ( int number )

Changes the cursor skin using the [skin number](../../../code/gui/skin/index.md#gui_mouse_layout).
### Arguments

- *int* **number** - Cursor skin number, one of the [CURSOR_*](../../../api/library/gui/class.gui_cpp.md#CURSOR_ARROW) pre-defined variables.

## int getDisplayDefaultSystemDPI ( ) const

Returns the default system dots/pixels-per-inch value.
### Return value

Dots/pixels-per-inch value.
## int getNumDisplays ( ) const

Returns the total number of displays.
### Return value

Number of displays.
## ivec2 getDisplayPosition ( int display_index ) const

Returns the position of the specified display.
### Arguments

- *int* **display_index** - Display index.

### Return value

Display position.
## ivec2 getDisplayResolution ( int display_index ) const

Returns the resolution of the specified display.
### Arguments

- *int* **display_index** - Display index.

### Return value

Display resolution.
## int getDisplayDPI ( int display_index ) const

Returns the DPI of the specified display.
### Arguments

- *int* **display_index** - Display index.

### Return value

Display DPI.
## int getMainDisplay ( ) const

Returns the index of the main display.
### Return value

Display index.
## int getDisplayNumModes ( int display_index ) const

Returns the total number of available display modes.
### Arguments

- *int* **display_index** - Display index.

### Return value

Number of available display modes.
## ivec2 getDisplayModeResolution ( int display_index , int mode_index ) const

Returns the DPI of the specified mode for the selected display.
### Arguments

- *int* **display_index** - Display index.
- *int* **mode_index** - Index of the display mode.

### Return value

Display DPI.
## int getDisplayModeRefreshRate ( int display_index , int mode_index ) const

Returns the refresh rate of the specified display mode.
### Arguments

- *int* **display_index** - Display index.
- *int* **mode_index** - Index of the display mode.

### Return value

Refresh rate of the specified display mode.
## const char * getDisplayName ( int display_index ) const

Returns the system name of the specified display.
### Arguments

- *int* **display_index** - Display index.

### Return value

Display name.
## bool hasClipboardText ( ) const

Returns the value showing if the clipboard contains anything.
### Return value

true if there is text in the clipboard, otherwise false.
## void setClipboardText ( const char* str )

Updates the contents of the system clipboard.
### Arguments

- *const char** **str** - Contents to set.

## const char* getClipboardText ( )

Retrieves the contents of the system clipboard.
### Return value

Contents of the system clipboard.
## bool showDialogMessage ( const char* title , const char* message , WIN_HANDLE parent_window_handle )

Displays a message dialog with the specified title and text.
### Arguments

- *const char** **title** - Title of the message window.
- *const char** **message** - Text of the message.
- *WIN_HANDLE* **parent_window_handle** - Handle of the parent window.

### Return value

true if the dialog message is displayed successfully, otherwise false.
## bool showDialogWarning ( const char* title , const char* warning , WIN_HANDLE parent_window_handle )

Displays a warning dialog with the specified title and text.
### Arguments

- *const char** **title** - Title of the warning window.
- *const char** **warning** - Text of the warning.
- *WIN_HANDLE* **parent_window_handle** - Handle of the parent window.

### Return value

true if the dialog warning is displayed successfully, otherwise false.
## bool showDialogError ( const char* title , const char* error , WIN_HANDLE parent_window_handle )

Displays an error dialog with the specified title and text.
### Arguments

- *const char** **title** - Title of the error window.
- *const char** **error** - Text of the error.
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

## void getConnectedJoysticks ( Vector <int32_t>& connected_ids )

Returns identifiers of all connected joysticks.
### Arguments

- *[Vector](../../../api/library/containers/vector/class.vector_cpp.md)<int32_t>&* **connected_ids** - Vector of IDs.

## int getJoystickPlayerIndex ( int32_t joy_id ) const

Returns the joystick player index.
### Arguments

- *int32_t* **joy_id** - Joystick ID.

### Return value

Player index.
## int getJoystickDeviceType ( int32_t joy_id ) const

Returns the type of the joystick.
### Arguments

- *int32_t* **joy_id** - Joystick ID.

### Return value

Joystick type.
## int getJoystickVendor ( int32_t joy_id ) const

Returns the vendor ID of the joystick.
### Arguments

- *int32_t* **joy_id** - Joystick ID.

### Return value

Joystick vendor ID.
## int getJoystickProduct ( int32_t joy_id ) const

Returns the product ID of the joystick.
### Arguments

- *int32_t* **joy_id** - Joystick ID.

### Return value

Joystick product ID.
## int getJoystickProductVersion ( int32_t joy_id ) const

Returns the product version of the joystick.
### Arguments

- *int32_t* **joy_id** - Joystick ID.

### Return value

Joystick product version.
## const char * getJoystickName ( int32_t joy_id ) const

Returns the name of the joystick.
### Arguments

- *int32_t* **joy_id** - Joystick ID.

### Return value

Joystick name.
## const char * getJoystickModelGUID ( int32_t joy_id ) const

Returns the name of the joystick.
### Arguments

- *int32_t* **joy_id** - Joystick ID.

### Return value

Model GUID of the joystick.
## int getJoystickNumButtons ( int32_t joy_id ) const

Returns the number of the joystick buttons.
### Arguments

- *int32_t* **joy_id** - Joystick ID.

### Return value

Number of buttons.
## int getJoystickNumAxes ( int32_t joy_id ) const

Returns the number of the joystick axes.
### Arguments

- *int32_t* **joy_id** - Joystick ID.

### Return value

Number of axes.
## int getJoystickNumPovs ( int32_t joy_id ) const

Returns the number of the joystick POV hats.
### Arguments

- *int32_t* **joy_id** - Joystick ID.

### Return value

Number of POV hats.
## float getJoystickAxisInitValue ( int32_t joy_id , int axis ) const

Returns the initial value of the joystick axis control.
### Arguments

- *int32_t* **joy_id** - Joystick ID.
- *int* **axis** - Axis index.

### Return value

Initial value of the axis control.
## const char * getJoystickButtonName ( int32_t joy_id , int button )

Returns the name of the joystick button.
### Arguments

- *int32_t* **joy_id** - Joystick ID.
- *int* **button** - Button index.

### Return value

Button name.
## const char * getJoystickAxisName ( int32_t joy_id , int axis )

Returns the name of the joystick axis.
### Arguments

- *int32_t* **joy_id** - Joystick ID.
- *int* **axis** - Axis index.

### Return value

Axis name.
## const char * getJoystickPovName ( int32_t joy_id , int pov )

Returns the name of the joystick POV hat.
### Arguments

- *int32_t* **joy_id** - Joystick ID.
- *int* **pov** - POV hat index.

### Return value

POV hat name.
## void getConnectedGamepads ( Vector <int32_t>& connected_ids )

Returns identifiers of all connected gamepads.
### Arguments

- *[Vector](../../../api/library/containers/vector/class.vector_cpp.md)<int32_t>&* **connected_ids** - Vector of IDs.

## int getGamepadPlayerIndex ( int32_t pad_id ) const

Returns the player index of the gamepad.
### Arguments

- *int32_t* **pad_id** - Gamepad ID.

### Return value

Player index.
## int getGamepadDeviceType ( int32_t pad_id ) const

Returns the type of the gamepad.
### Arguments

- *int32_t* **pad_id** - Gamepad ID.

### Return value

Gamepad type.
## int getGamepadModelType ( int32_t pad_id ) const

Returns the model type of the joystick.
### Arguments

- *int32_t* **pad_id** - Gamepad ID.

### Return value

Model type.
## const char * getGamepadName ( int32_t pad_id ) const

Return the name of the gamepad.
### Arguments

- *int32_t* **pad_id** - Gamepad ID.

### Return value

Gamepad name.
## const char * getGamepadModelGUID ( int32_t pad_id ) const

Returns the model GUID of the gamepad.
### Arguments

- *int32_t* **pad_id** - Gamepad ID.

### Return value

Model GUID.
## void setGamepadVibration ( int32_t pad_id , float low_frequency , float high_frequency , float duration_ms )

Starts vibration of the gamepad.
### Arguments

- *int32_t* **pad_id** - Gamepad ID.
- *float* **low_frequency** - Low-frequency (left) motor speed.
- *float* **high_frequency** - High-frequency (right) motor speed.
- *float* **duration_ms** - Duration of vibration, in milliseconds.

## int getGamepadNumTouches ( int32_t pad_id ) const

Returns the total number of touch panels for the specified gamepad.
### Arguments

- *int32_t* **pad_id** - Gamepad ID.

### Return value

Total number of touch panels for the specified gamepad.
## int getGamepadNumTouchFingers ( int32_t pad_id , int touch ) const

Returns the total number of fingers supported by the specified gamepad touch panel.
### Arguments

- *int32_t* **pad_id** - Gamepad ID.
- *int* **touch** - Index of the gamepad touch panel, the number from 0 to the total number of touch panels.

### Return value

Total number of the fingers supported by the specified gamepad touch panel.
## int getDisplayRefreshRate ( int display_index ) const

Returns the refresh rate of the display.
### Arguments

- *int* **display_index** - Display index.

### Return value

Refresh rate.
## int getDisplayCurrentMode ( int display_index ) const

Returns the number of the current display mode.
### Arguments

- *int* **display_index** - Display index.

### Return value

Number of the current display mode.
## int getDisplayDesktopMode ( int display_index ) const

Returns the number of the desktop's display mode.
### Arguments

- *int* **display_index** - Display index.

### Return value

Number of the desktop's display mode.
## int getDisplayOrientation ( int display_index ) const

Returns the orientation of the display.
### Arguments

- *int* **display_index** - Display index.

### Return value

Display orientation.
## bool isDpiAwarenessSupported ( int32_t mode ) const

Returns a value indicating if the specified DPI awareness mode is supported.
### Arguments

- *int32_t* **mode** - DPI awareness mode, the value indicating how the application processes the DPI scaling.

### Return value

true the specified DPI awareness mode is supported; otherwise, false.
## bool isKeyboardModifierEnabled ( int modifier ) const

Returns a value indicating if the specified keyboard modifier is enabled.
### Arguments

- *int* **modifier** - Keyboard modifier (one of the *[Input::MODIFIER_*](../../../api/library/controls/class.input_cpp.md#MODIFIER)* variables).

### Return value

true if the keyboard modifier is enabled; otherwise, false.
## unsigned int keyToUnicode ( unsigned int key ) const

Returns the specified key transformed to Unicode.
### Arguments

- *unsigned int* **key** - Key (one of the *[Input::KEY_*](../../../api/library/controls/class.input_cpp.md#KEY)* variables).

### Return value

Unicode symbol.
## unsigned int unicodeToKey ( unsigned int unicode ) const

Returns the key transformed from the specified Unicode symbol.
### Arguments

- *unsigned int* **unicode** - Unicode symbol.

### Return value

Key (one of the *[Input::KEY_*](../../../api/library/controls/class.input_cpp.md#KEY)* variables).
## void setIMETextInputEnabled ( bool enabled )

Enables or disables the input method editor, which is used to compose text in languages that need it, such as Chinese, Japanese and Korean. Implement it for the platform you support; leave it empty if the platform has no input method editor.
### Arguments

- *bool* **enabled** - true to start accepting composed text input, false to stop.

## bool isIMETextInputEnabled ( ) const

Returns a value indicating whether the input method editor is currently accepting text. Return false if the platform has no input method editor.
### Return value

true if the input method editor accepts text, false if it does not.
## void setIMETextInputRect ( int position_x , int position_y , int width , int height )

Sets the rectangle the text is composed in, so that the input method editor puts its candidate window beside it rather than over it.
### Arguments

- *int* **position_x** - X coordinate of the rectangle, in pixels.
- *int* **position_y** - Y coordinate of the rectangle, in pixels.
- *int* **width** - Width of the rectangle, in pixels.
- *int* **height** - Height of the rectangle, in pixels.

## bool isFocus ( )

Returns the value indicating if focus is set on the window.
### Return value

true if focus is set on the window; otherwise, false.
## void focusGained ( )

The focus is set on the window.
## void focusLost ( )

The focus is removed from the window.
## void updateWindowOrders ( )

Updates the Z order of all windows.
> **Notice:** It is recommended to use this method only when required, because it is very slow.

## int getWindowOrder ( WIN_HANDLE win_handle ) const

Returns the window Z-order.
### Arguments

- *WIN_HANDLE* **win_handle** - Engine window handle.

### Return value

Window order (a lower value means that the window is closer to the viewer).
## void windowToTop ( WIN_HANDLE win_handle )

Brings the window with the specified handle to top (atop of all other windows).
### Arguments

- *WIN_HANDLE* **win_handle** - Engine window handle.

## WIN_HANDLE getWindowIntersection ( const ivec2& global_pos , const Vector <WIN_HANDLE>& excludes )

Returns the handle of the window the intersection with which is detected.
### Arguments

- *const ivec2&* **global_pos** - The coordinates of the intersection point in global coordinates.
- *const [Vector](../../../api/library/containers/vector/class.vector_cpp.md)<WIN_HANDLE>&* **excludes** - The windows to be excluded from the intersection detection.

### Return value

The handle of the window the intersection with which is detected.
## bool isJoystickForceFeedbackEffectSupported ( int32_t joy_id , int effect )

Returns a value indicating whether the specified type of force-feedback effect is supported by the joystick with the given ID.
### Arguments

- *int32_t* **joy_id** - Joystick ID.
- *int* **effect** - Type of a force-feedback effect.

### Return value

true if the specified type of force-feedback effect is supported by the joystick with the given ID; otherwise, false.
## void playJoystickForceFeedbackEffectConstant ( int32_t joy_id , float force )

Applies the constant force-feedback effect with the specified parameters to the joystick with the given ID. Force is applied at a constant level for the duration of the effect.
### Arguments

- *int32_t* **joy_id** - Joystick ID.
- *float* **force** - Amount of force being applied by a force-feedback effect. The value in range [-1, 1]. Negative values mean that the initial direction of the force-feedback effect is towards the left, positive values � to the right.

## void playJoystickForceFeedbackEffectRamp ( int32_t joy_id , float force , unsigned long duration_us )

Applies the ramp force-feedback effect with the specified parameters to the joystick with the given ID. Force is applied gradually by being increased or decreased over the duration of the effect.
### Arguments

- *int32_t* **joy_id** - Joystick ID.
- *float* **force** - Amount of force being applied by a force-feedback effect. The value in range [-1, 1]. Negative values mean that the initial direction of the force-feedback effect is towards the left, positive values � to the right.
- *unsigned long* **duration_us** - Force-feedback effect duration, in microseconds.

## void playJoystickForceFeedbackEffectSineWave ( int32_t joy_id , float force , float attack_force , float fade_force , int phase , unsigned int period_ms , unsigned int attack_length_ms , unsigned int fade_length_ms , unsigned int effect_duration_ms )

Applies the sine-wave force-feedback effect with the specified parameters to the joystick with the given ID. Force is applied in a sine-wave pattern.
### Arguments

- *int32_t* **joy_id** - Joystick ID.
- *float* **force** - Sustain value � the force value in the middle of the force-feedback effect in range [-1, 1]. Negative values mean that the initial direction of the force-feedback effect is towards the left, positive values � to the right.
- *float* **attack_force** - Value at the start of the attack, in range [0, 1].
- *float* **fade_force** - Value at the end of the fade, in range [0, 1].
- *int* **phase** - Positive phase shift, in degrees in range [0, 360].
- *unsigned int* **period_ms** - Period of the wave, in ms.
- *unsigned int* **attack_length_ms** - Duration of the attack � time period in ms defining how long it takes to reach the force value (the value in the middle of the effect).
- *unsigned int* **fade_length_ms** - Duration of the fade out � time period in ms defining how long it takes to fall away from the force value (the value in the middle of the effect).
- *unsigned int* **effect_duration_ms** - Duration of the effect, in ms.

## void playJoystickForceFeedbackEffectSquareWave ( int32_t joy_id , float force , float attack_force , float fade_force , int phase , unsigned int period_ms , unsigned int attack_length_ms , unsigned int fade_length_ms , unsigned int effect_duration_ms )

Applies the square-wave force-feedback effect with the specified parameters to the joystick with the given ID. Force is applied in a square-wave pattern.
### Arguments

- *int32_t* **joy_id** - Joystick ID.
- *float* **force** - Sustain value � the force value in the middle of the force-feedback effect in range [-1, 1]. Negative values mean that the initial direction of the force-feedback effect is towards the left, positive values � to the right.
- *float* **attack_force** - Value at the start of the attack, in range [0, 1].
- *float* **fade_force** - Value at the end of the fade, in range [0, 1].
- *int* **phase** - Positive phase shift, in degrees in range [0, 360].
- *unsigned int* **period_ms** - Period of the wave, in ms.
- *unsigned int* **attack_length_ms** - Duration of the attack � time period in ms defining how long it takes to reach the force value (the value in the middle of the effect).
- *unsigned int* **fade_length_ms** - Duration of the fade out � time period in ms defining how long it takes to fall away from the force value (the value in the middle of the effect).
- *unsigned int* **effect_duration_ms** - Duration of the effect, in ms.

## void playJoystickForceFeedbackEffectTriangleWave ( int32_t joy_id , float force , float attack_force , float fade_force , int phase , unsigned int period_ms , unsigned int attack_length_ms , unsigned int fade_length_ms , unsigned int effect_duration_ms )

Applies the triangle-wave force-feedback effect with the specified parameters to the joystick with the given ID. Force is applied in a triangle-wave pattern.
### Arguments

- *int32_t* **joy_id** - Joystick ID.
- *float* **force** - Sustain value � the force value in the middle of the force-feedback effect in range [-1, 1]. Negative values mean that the initial direction of the force-feedback effect is towards the left, positive values � to the right.
- *float* **attack_force** - Value at the start of the attack. Value in range [0, 1].
- *float* **fade_force** - Value at the end of the fade. Value in range [0, 1].
- *int* **phase** - Positive phase shift, in degrees in range [0, 360].
- *unsigned int* **period_ms** - Period of the wave, in ms.
- *unsigned int* **attack_length_ms** - Duration of the attack � time period in ms defining how long it takes to reach the force value (the value in the middle of the effect).
- *unsigned int* **fade_length_ms** - Duration of the fade out � time period in ms defining how long it takes to fall away from the force value (the value in the middle of the effect).
- *unsigned int* **effect_duration_ms** - Duration of the effect, in ms.

## void playJoystickForceFeedbackEffectSawtoothUpWave ( int32_t joy_id , float force , float attack_force , float fade_force , int phase , unsigned int period_ms , unsigned int attack_length_ms , unsigned int fade_length_ms , unsigned int effect_duration_ms )

Applies the upward-sawtooth-wave force-feedback effect with the specified parameters to the joystick with the given ID. Force is applied in a upward-sawtooth-wave pattern.
### Arguments

- *int32_t* **joy_id** - Joystick ID.
- *float* **force** - Sustain value � the force value in the middle of the force-feedback effect in range [-1, 1]. Negative values mean that the initial direction of the force-feedback effect is towards the left, positive values � to the right.
- *float* **attack_force** - Value at the start of the attack. Value in range [0, 1].
- *float* **fade_force** - Value at the end of the fade. Value in range [0, 1].
- *int* **phase** - Positive phase shift, in degrees in range [0, 360].
- *unsigned int* **period_ms** - Period of the wave, in ms.
- *unsigned int* **attack_length_ms** - Duration of the attack � time period in ms defining how long it takes to reach the force value (the value in the middle of the effect).
- *unsigned int* **fade_length_ms** - Duration of the fade out � time period in ms defining how long it takes to fall away from the force value (the value in the middle of the effect).
- *unsigned int* **effect_duration_ms** - Duration of the effect, in ms.

## void playJoystickForceFeedbackEffectSawtoothDownWave ( int32_t joy_id , float force , float attack_force , float fade_force , int phase , unsigned int period_ms , unsigned int attack_length_ms , unsigned int fade_length_ms , unsigned int effect_duration_ms )

Applies the downward-sawtooth-wave force-feedback effect with the specified parameters to the joystick with the given ID. Force is applied in a downward-sawtooth-wave pattern.
### Arguments

- *int32_t* **joy_id** - Joystick ID.
- *float* **force** - Sustain value � the force value in the middle of the force-feedback effect in range [-1, 1]. Negative values mean that the initial direction of the force-feedback effect is towards the left, positive values � to the right.
- *float* **attack_force** - Value at the start of the attack. Value in range [0, 1].
- *float* **fade_force** - Value at the end of the fade. Value in range [0, 1].
- *int* **phase** - Positive phase shift, in degrees in range [0, 360].
- *unsigned int* **period_ms** - Period of the wave, in ms.
- *unsigned int* **attack_length_ms** - Duration of the attack � time period in ms defining how long it takes to reach the force value (the value in the middle of the effect).
- *unsigned int* **fade_length_ms** - Duration of the fade out � time period in ms defining how long it takes to fall away from the force value (the value in the middle of the effect).
- *unsigned int* **effect_duration_ms** - Duration of the effect, in ms.

## void playJoystickForceFeedbackEffectSpring ( int32_t joy_id , float left_force , float left_saturation , float right_force , float right_saturation , float offset , float deadband )

Applies the spring force-feedback effect with the specified parameters to the joystick with the given ID. Force is applied in opposition to a set state.
### Arguments

- *int32_t* **joy_id** - Joystick ID.
- *float* **left_force** - Strength of the force-feedback effect that occurs when turning to the left. Value in range [0, 1].
- *float* **left_saturation** - Maximum possible force for the force-feedback effect on turning left. Value in range [0, 1]. Not all devices support saturation.
- *float* **right_force** - Strength of the force-feedback effect that occurs when turning to the right. Value in range [0, 1].
- *float* **right_saturation** - Maximum possible force for the force-feedback effect on turning right. Value in range [0, 1]. Not all devices support saturation.
- *float* **offset** - The offset from the zero reading of the appropriate sensor value at which the condition begins to be applied. For a spring effect, the neutral point - that is, the point along the axis at which the spring would be considered at rest - would be defined by the offset for the condition.
- *float* **deadband** - Zone around the offset of an axis at which the condition is not active. In the case of a spring that is at rest in the middle of an axis, the deadband enlarges this area of rest. Not all devices support deadband.

## void playJoystickForceFeedbackEffectFriction ( int32_t joy_id , float left_force , float left_saturation , float right_force , float right_saturation )

Applies the friction force-feedback effect with the specified parameters to the joystick with the given ID. Force is applied to mimic friction.
### Arguments

- *int32_t* **joy_id** - Joystick ID.
- *float* **left_force** - Strength of the force-feedback effect that occurs when turning to the left. Value in range [0, 1].
- *float* **left_saturation** - Maximum possible force for the force-feedback effect on turning left. Value in range [0, 1]. Not all devices support saturation.
- *float* **right_force** - Strength of the force-feedback effect that occurs when turning to the right. Value in range [0, 1].
- *float* **right_saturation** - Maximum possible force for the force-feedback effect on turning right. Value in range [0, 1]. Not all devices support saturation.

## void playJoystickForceFeedbackEffectDamper ( int32_t joy_id , float left_force , float left_saturation , float right_force , float right_saturation )

Applies the damper force-feedback effect with the specified parameters to the joystick with the given ID. Force is applied to mimic a damper effect.
### Arguments

- *int32_t* **joy_id** - Joystick ID.
- *float* **left_force** - Strength of the force-feedback effect that occurs when turning to the left. Value in range [0, 1].
- *float* **left_saturation** - Maximum possible force for the force-feedback effect on turning left. Value in range [0, 1]. Not all devices support saturation.
- *float* **right_force** - Strength of the force-feedback effect that occurs when turning to the right. Value in range [0, 1].
- *float* **right_saturation** - Maximum possible force for the force-feedback effect on turning right. Value in range [0, 1]. Not all devices support saturation.

## void playJoystickForceFeedbackEffectInertia ( int32_t joy_id , float force )

Applies the inertia force-feedback effect with the specified parameters to the joystick with the given ID. Force is applied to mimic an inertia effect.
### Arguments

- *int32_t* **joy_id** - Joystick ID.
- *float* **force** - Amount of force being applied by a force-feedback effect. Value in range [0, 1].

## void stopJoystickForceFeedbackEffect ( int32_t joy_id , int effect )

Stops application of the specified type of force-feedback effect to the joystick with the given ID.
### Arguments

- *int32_t* **joy_id** - Joystick ID.
- *int* **effect** - Type of a force-feedback effect.
