# Unigine::CustomSystemProxy Class (CS)


This class is used for integration with third-party systems (for example, *Qt, SDL, WPF*). Most of its functions are virtual, so you need to override them when implementing your application.


In general, the *CustomSystemProxy*-based workflow is the following:


1. Create a custom class and inherit it from the *[Unigine.CustomSystemProxy](../../../api/library/engine/class.customsystemproxy_cs.md)* class.
2. Define the supported features via the proxy constructor (*SYSTEM_PROXY_FEATURES.**).
3. Override all of the virtual functions of the class.
4. Implement the functions according to the list of the supported features, including [event handling](../../../code/csharp/usage/unigine_app/proxy.md#event_handling) and [rendering into an external window](../../../code/csharp/usage/unigine_app/proxy.md#external_window), if required.


> **Notice:** The full-featured example of integrating UNIGINE Engine into the WPF framework can be found in the `source/csharp/proxy/wpf` folder.


The following code is the part of the *SystemProxyWPF* example:


<details>
<summary>SystemProxyWPF.cs | Close</summary>

```csharp
// ...

using Unigine;

namespace UnigineWPF
{
	// inherit from CustomSystemProxy
	public partial class SystemProxyWPF : CustomSystemProxy
	{
		// create a proxy instance
		private static readonly SystemProxyWPF instance = new SystemProxyWPF();

		// create a proxy that can work with the mouse and keyboard and create windows
		public SystemProxyWPF() : base(
			(int)SYSTEM_PROXY_FEATURES.WINDOWS |
			(int)SYSTEM_PROXY_FEATURES.MOUSE |
			(int)SYSTEM_PROXY_FEATURES.KEYBOARD
			)
		{
			...
		}

		public static SystemProxyWPF Instance => instance;
		public delegate void ExternalRenderDelegate(IntPtr hwnd);
		public event ExternalRenderDelegate onExternalRender;

		// override functions of the CustomSystemProxy class
		public override void onExternalWindowRender(IntPtr hwnd)
		{
			onExternalRender?.Invoke(hwnd);
		}

		// main thread
		protected override bool isEngineActive() { return true; }

		protected override void mainUpdate() {}

		// windows
		protected override void createWindow(int width, int height, out WIN_HANDLE out_handle)
		{
			// implementation
		}

		protected override void removeWindow(WIN_HANDLE win_handle)
		{
			// implementation
		}
		protected override void setWindowTitle(WIN_HANDLE win_handle, string title)
		{
			// implementation
		}

		// mouse
		protected override void setGlobalMousePosition(in ivec2 pos)
		{
			// implementation
		}
		protected override ivec2 getGlobalMousePosition()
		{
			// implementation
		}

		// ...

		// displays
		protected override int getDisplayDefaultSystemDPI()
		{
			return 96;
		}

		protected override int getNumDisplays()
		{
			return Screen.AllScreens.Length;
		}

		// other
		protected override bool hasClipboardText()
		{
			return System.Windows.Clipboard.ContainsData(System.Windows.DataFormats.Text);
		}
	}
}

```

</details>


### See Also


- The [Integrating with Frameworks](../../../code/csharp/usage/unigine_app/proxy.md) article


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

Mask specifying the set of [SYSTEM_PROXY_*](#SYSTEM_PROXY_WINDOWS) features CustomSystemProxy can perform.
## bool isWindowsSupported ( )

Returns the value indicating if CustomSystemProxy supports windows creation.
### Return value

true if CustomSystemProxy supports windows creation, otherwise false.
## bool isMouseSupported ( )

Returns the value indicating if CustomSystemProxy supports work with the mouse.
### Return value

true if CustomSystemProxy supports work with the mouse, otherwise false.
## bool isKeyboardSupported ( )

Returns the value indicating if CustomSystemProxy supports work with the keyboard.
### Return value

true if CustomSystemProxy supports work with the keyboard, otherwise false.
## bool isTouchesSupported ( )

Returns the value indicating if CustomSystemProxy supports work with the sensor input.
### Return value

true if CustomSystemProxy supports work with the sensor input, otherwise false.
## bool isDisplaysSupported ( )

Returns the value indicating if CustomSystemProxy can provide information on displays.
### Return value

true if CustomSystemProxy can provide information on displays, otherwise false.
## bool isJoysticksSupported ( )

Returns the value indicating if CustomSystemProxy supports work with the joystick input.
### Return value

true if CustomSystemProxy supports work with the joystick input, otherwise false.
## bool isGamepadsSupported ( )

Returns the value indicating if CustomSystemProxy supports work with the gamepad input.
### Return value

true if CustomSystemProxy supports work with the gamepad input, otherwise false.
## bool initExternalWindowBuffers ( WIN_HANDLE win_handle , ivec2 size )

Initialization of the resources for rendering to the external window.
### Arguments

- *WIN_HANDLE* **win_handle** - Window handle.
- *ivec2* **size** - Window size.

### Return value

true if the operation is successful, otherwise false.
## bool resizeExternalWindowBuffers ( WIN_HANDLE win_handle , ivec2 size )

Resizing of the external window in order to update the internal textures.
### Arguments

- *WIN_HANDLE* **win_handle** - Window handle.
- *ivec2* **size** - Window size.

### Return value

true if the operation is successful, otherwise false.
## bool shutdownExternalWindowBuffers ( WIN_HANDLE win_handle )

Shutdown of all resources required for rendering to the external window upon closing the window.
### Arguments

- *WIN_HANDLE* **win_handle** - Window handle.

### Return value

true if the operation is successful, otherwise false.
## void removeWindow ( WIN_HANDLE win_handle )

Destroys the window using its handle.
### Arguments

- *WIN_HANDLE* **win_handle** - Engine window handle.

## void setWindowTitle ( WIN_HANDLE win_handle , string title )

Sets the window title.
### Arguments

- *WIN_HANDLE* **win_handle** - Engine window handle.
- *string* **title** - Window title.

## void setWindowIcon ( WIN_HANDLE win_handle , Image image )

Sets the window icon.
### Arguments

- *WIN_HANDLE* **win_handle** - Engine window handle.
- *[Image](../../../api/library/common/class.image_cs.md)* **image** - Image to be used as the icon.

## void setWindowSize ( WIN_HANDLE win_handle , ivec2 size )

Sets the window size.
### Arguments

- *WIN_HANDLE* **win_handle** - Engine window handle.
- *ivec2* **size** - Window size (width and height).

## void setWindowMinSize ( WIN_HANDLE win_handle , ivec2 size )

Sets the minimum possible size of the window.
### Arguments

- *WIN_HANDLE* **win_handle** - Engine window handle.
- *ivec2* **size** - Window size (width and height).

## void setWindowMaxSize ( WIN_HANDLE win_handle , ivec2 size )

Sets the maximum possible size of the window.
### Arguments

- *WIN_HANDLE* **win_handle** - Engine window handle.
- *ivec2* **size** - Window size (width and height).

## void setWindowPosition ( WIN_HANDLE win_handle , ivec2 pos )

Sets the window position (top left corner) in screen coordinates.
### Arguments

- *WIN_HANDLE* **win_handle** - Engine window handle.
- *ivec2* **pos** - Window position.

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

## int getWindowDisplayIndex ( WIN_HANDLE win_handle )

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
## void setGlobalMousePosition ( ivec2 pos )

Sets the mouse position in global coordinates relative to the main system display.
### Arguments

- *ivec2* **pos** - Mouse position in global coordinates.

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
## void setMouseCursorSkinCustom ( Image mouse_skin )

Sets the specified [skin image](../../../code/gui/skin/index.md#gui_mouse_layout) as the mouse cursor.
### Arguments

- *[Image](../../../api/library/common/class.image_cs.md)* **mouse_skin** - [Image](../../../code/gui/skin/index.md#gui_mouse_layout) containing pointer shapes to be set for the mouse cursor (e.g., select, move, resize, etc.).

## void setMouseCursorSkinSystem ( )

Sets the current OS cursor skin (pointer shapes like select, move, resize, etc.).
## void setMouseCursorCustom ( Image image , int x , int y )

Sets a custom image for the OS mouse cursor. The image must be of the square size and *RGBA8* format. This method of setting cursor has the priority over other cursor setting methods. The image set by this method can be cleared only using the [clearMouseCursorCustom()](#clearMouseCursorCustom_void) method.
### Arguments

- *[Image](../../../api/library/common/class.image_cs.md)* **image** - [Image](../../../code/gui/skin/index.md#gui_mouse_layout) containing pointer shapes to be set for the mouse cursor (e.g., select, move, resize, etc.).
- *int* **x** - X coordinate of the cursor's hot spot.
- *int* **y** - Y coordinate of the cursor's hot spot.

## void clearMouseCursorCustom ( )

Clears the custom mouse cursor set via the [setMouseCursorCustom()](#setMouseCursorCustom_const_ImagePtr_ref_int_int_void) method.
## void changeMouseCursorSkinNumber ( int number )

Changes the cursor skin using the [skin number](../../../code/gui/skin/index.md#gui_mouse_layout).
### Arguments

- *int* **number** - Cursor skin number, one of the [CURSOR_*](../../../api/library/gui/class.gui_cs.md#CURSOR_ARROW) pre-defined variables.

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
## string getDisplayName ( int display_index )

Returns the system name of the specified display.
### Arguments

- *int* **display_index** - Display index.

### Return value

Display name.
## bool hasClipboardText ( )

Returns the value showing if the clipboard contains anything.
### Return value

true if there is text in the clipboard, otherwise false.
## void setClipboardText ( string str )

Updates the contents of the system clipboard.
### Arguments

- *string* **str** - Contents to set.

## string getClipboardText ( )

Retrieves the contents of the system clipboard.
### Return value

Contents of the system clipboard.
## bool showDialogMessage ( string title , string message , WIN_HANDLE parent_window_handle )

Displays a message dialog with the specified title and text.
### Arguments

- *string* **title** - Title of the message window.
- *string* **message** - Text of the message.
- *WIN_HANDLE* **parent_window_handle** - Handle of the parent window.

### Return value

true if the dialog message is displayed successfully, otherwise false.
## bool showDialogWarning ( string title , string warning , WIN_HANDLE parent_window_handle )

Displays a warning dialog with the specified title and text.
### Arguments

- *string* **title** - Title of the warning window.
- *string* **warning** - Text of the warning.
- *WIN_HANDLE* **parent_window_handle** - Handle of the parent window.

### Return value

true if the dialog warning is displayed successfully, otherwise false.
## bool showDialogError ( string title , string error , WIN_HANDLE parent_window_handle )

Displays an error dialog with the specified title and text.
### Arguments

- *string* **title** - Title of the error window.
- *string* **error** - Text of the error.
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

## void getConnectedJoysticks ( Vector<int32_t>& connected_ids )

Returns identifiers of all connected joysticks.
### Arguments

- *Vector<int32_t>&* **connected_ids** - Vector of IDs.

## int getJoystickPlayerIndex ( Int32 joy_id )

Returns the joystick player index.
### Arguments

- *Int32* **joy_id** - Joystick ID.

### Return value

Player index.
## int getJoystickDeviceType ( Int32 joy_id )

Returns the type of the joystick.
### Arguments

- *Int32* **joy_id** - Joystick ID.

### Return value

Joystick type.
## int getJoystickVendor ( Int32 joy_id )

Returns the vendor ID of the joystick.
### Arguments

- *Int32* **joy_id** - Joystick ID.

### Return value

Joystick vendor ID.
## int getJoystickProduct ( Int32 joy_id )

Returns the product ID of the joystick.
### Arguments

- *Int32* **joy_id** - Joystick ID.

### Return value

Joystick product ID.
## int getJoystickProductVersion ( Int32 joy_id )

Returns the product version of the joystick.
### Arguments

- *Int32* **joy_id** - Joystick ID.

### Return value

Joystick product version.
## string getJoystickName ( Int32 joy_id )

Returns the name of the joystick.
### Arguments

- *Int32* **joy_id** - Joystick ID.

### Return value

Joystick name.
## string getJoystickModelGUID ( Int32 joy_id )

Returns the name of the joystick.
### Arguments

- *Int32* **joy_id** - Joystick ID.

### Return value

Model GUID of the joystick.
## int getJoystickNumButtons ( Int32 joy_id )

Returns the number of the joystick buttons.
### Arguments

- *Int32* **joy_id** - Joystick ID.

### Return value

Number of buttons.
## int getJoystickNumAxes ( Int32 joy_id )

Returns the number of the joystick axes.
### Arguments

- *Int32* **joy_id** - Joystick ID.

### Return value

Number of axes.
## int getJoystickNumPovs ( Int32 joy_id )

Returns the number of the joystick POV hats.
### Arguments

- *Int32* **joy_id** - Joystick ID.

### Return value

Number of POV hats.
## float getJoystickAxisInitValue ( Int32 joy_id , int axis )

Returns the initial value of the joystick axis control.
### Arguments

- *Int32* **joy_id** - Joystick ID.
- *int* **axis** - Axis index.

### Return value

Initial value of the axis control.
## string getJoystickButtonName ( Int32 joy_id , int button )

Returns the name of the joystick button.
### Arguments

- *Int32* **joy_id** - Joystick ID.
- *int* **button** - Button index.

### Return value

Button name.
## string getJoystickAxisName ( Int32 joy_id , int axis )

Returns the name of the joystick axis.
### Arguments

- *Int32* **joy_id** - Joystick ID.
- *int* **axis** - Axis index.

### Return value

Axis name.
## string getJoystickPovName ( Int32 joy_id , int pov )

Returns the name of the joystick POV hat.
### Arguments

- *Int32* **joy_id** - Joystick ID.
- *int* **pov** - POV hat index.

### Return value

POV hat name.
## void getConnectedGamepads ( Vector<int32_t>& connected_ids )

Returns identifiers of all connected gamepads.
### Arguments

- *Vector<int32_t>&* **connected_ids** - Vector of IDs.

## int getGamepadPlayerIndex ( Int32 pad_id )

Returns the player index of the gamepad.
### Arguments

- *Int32* **pad_id** - Gamepad ID.

### Return value

Player index.
## int getGamepadDeviceType ( Int32 pad_id )

Returns the type of the gamepad.
### Arguments

- *Int32* **pad_id** - Gamepad ID.

### Return value

Gamepad type.
## int getGamepadModelType ( Int32 pad_id )

Returns the model type of the joystick.
### Arguments

- *Int32* **pad_id** - Gamepad ID.

### Return value

Model type.
## string getGamepadName ( Int32 pad_id )

Return the name of the gamepad.
### Arguments

- *Int32* **pad_id** - Gamepad ID.

### Return value

Gamepad name.
## string getGamepadModelGUID ( Int32 pad_id )

Returns the model GUID of the gamepad.
### Arguments

- *Int32* **pad_id** - Gamepad ID.

### Return value

Model GUID.
## void setGamepadVibration ( Int32 pad_id , float low_frequency , float high_frequency , float duration_ms )

Starts vibration of the gamepad.
### Arguments

- *Int32* **pad_id** - Gamepad ID.
- *float* **low_frequency** - Low-frequency (left) motor speed.
- *float* **high_frequency** - High-frequency (right) motor speed.
- *float* **duration_ms** - Duration of vibration, in milliseconds.

## int getGamepadNumTouches ( Int32 pad_id )

Returns the total number of touch panels for the specified gamepad.
### Arguments

- *Int32* **pad_id** - Gamepad ID.

### Return value

Total number of touch panels for the specified gamepad.
## int getGamepadNumTouchFingers ( Int32 pad_id , int touch )

Returns the total number of fingers supported by the specified gamepad touch panel.
### Arguments

- *Int32* **pad_id** - Gamepad ID.
- *int* **touch** - Index of the gamepad touch panel, the number from 0 to the total number of touch panels.

### Return value

Total number of the fingers supported by the specified gamepad touch panel.
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
## bool isDpiAwarenessSupported ( Int32 mode )

Returns a value indicating if the specified DPI awareness mode is supported.
### Arguments

- *Int32* **mode** - DPI awareness mode, the value indicating how the application processes the DPI scaling.

### Return value

true the specified DPI awareness mode is supported; otherwise, false.
## bool isKeyboardModifierEnabled ( int modifier )

Returns a value indicating if the specified keyboard modifier is enabled.
### Arguments

- *int* **modifier** - Keyboard modifier (one of the *[Input::MODIFIER_*](../../../api/library/controls/class.input_cs.md#MODIFIER)* variables).

### Return value

true if the keyboard modifier is enabled; otherwise, false.
## unsigned int keyToUnicode ( unsigned int key )

Returns the specified key transformed to Unicode.
### Arguments

- *unsigned int* **key** - Key (one of the *[Input::KEY_*](../../../api/library/controls/class.input_cs.md#KEY)* variables).

### Return value

Unicode symbol.
## unsigned int unicodeToKey ( unsigned int unicode )

Returns the key transformed from the specified Unicode symbol.
### Arguments

- *unsigned int* **unicode** - Unicode symbol.

### Return value

Key (one of the *[Input::KEY_*](../../../api/library/controls/class.input_cs.md#KEY)* variables).
## void setIMETextInputEnabled ( bool enabled )

Enables or disables the input method editor, which is used to compose text in languages that need it, such as Chinese, Japanese and Korean. Implement it for the platform you support; leave it empty if the platform has no input method editor.
### Arguments

- *bool* **enabled** - true to start accepting composed text input, false to stop.

## bool isIMETextInputEnabled ( )

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

## int getWindowOrder ( WIN_HANDLE win_handle )

Returns the window Z-order.
### Arguments

- *WIN_HANDLE* **win_handle** - Engine window handle.

### Return value

Window order (a lower value means that the window is closer to the viewer).
## void windowToTop ( WIN_HANDLE win_handle )

Brings the window with the specified handle to top (atop of all other windows).
### Arguments

- *WIN_HANDLE* **win_handle** - Engine window handle.

## WIN_HANDLE getWindowIntersection ( const ivec2& global_pos , const Vector<WIN_HANDLE>& excludes )

Returns the handle of the window the intersection with which is detected.
### Arguments

- *const ivec2&* **global_pos** - The coordinates of the intersection point in global coordinates.
- *const Vector<WIN_HANDLE>&* **excludes** - The windows to be excluded from the intersection detection.

### Return value

The handle of the window the intersection with which is detected.
## bool isJoystickForceFeedbackEffectSupported ( Int32 joy_id , int effect )

Returns a value indicating whether the specified type of force-feedback effect is supported by the joystick with the given ID.
### Arguments

- *Int32* **joy_id** - Joystick ID.
- *int* **effect** - Type of a force-feedback effect.

### Return value

true if the specified type of force-feedback effect is supported by the joystick with the given ID; otherwise, false.
## void playJoystickForceFeedbackEffectConstant ( Int32 joy_id , float force )

Applies the constant force-feedback effect with the specified parameters to the joystick with the given ID. Force is applied at a constant level for the duration of the effect.
### Arguments

- *Int32* **joy_id** - Joystick ID.
- *float* **force** - Amount of force being applied by a force-feedback effect. The value in range [-1, 1]. Negative values mean that the initial direction of the force-feedback effect is towards the left, positive values � to the right.

## void playJoystickForceFeedbackEffectRamp ( Int32 joy_id , float force , unsigned long duration_us )

Applies the ramp force-feedback effect with the specified parameters to the joystick with the given ID. Force is applied gradually by being increased or decreased over the duration of the effect.
### Arguments

- *Int32* **joy_id** - Joystick ID.
- *float* **force** - Amount of force being applied by a force-feedback effect. The value in range [-1, 1]. Negative values mean that the initial direction of the force-feedback effect is towards the left, positive values � to the right.
- *unsigned long* **duration_us** - Force-feedback effect duration, in microseconds.

## void playJoystickForceFeedbackEffectSineWave ( Int32 joy_id , float force , float attack_force , float fade_force , int phase , UInt32 period_ms , UInt32 attack_length_ms , UInt32 fade_length_ms , UInt32 effect_duration_ms )

Applies the sine-wave force-feedback effect with the specified parameters to the joystick with the given ID. Force is applied in a sine-wave pattern.
### Arguments

- *Int32* **joy_id** - Joystick ID.
- *float* **force** - Sustain value � the force value in the middle of the force-feedback effect in range [-1, 1]. Negative values mean that the initial direction of the force-feedback effect is towards the left, positive values � to the right.
- *float* **attack_force** - Value at the start of the attack, in range [0, 1].
- *float* **fade_force** - Value at the end of the fade, in range [0, 1].
- *int* **phase** - Positive phase shift, in degrees in range [0, 360].
- *UInt32* **period_ms** - Period of the wave, in ms.
- *UInt32* **attack_length_ms** - Duration of the attack � time period in ms defining how long it takes to reach the force value (the value in the middle of the effect).
- *UInt32* **fade_length_ms** - Duration of the fade out � time period in ms defining how long it takes to fall away from the force value (the value in the middle of the effect).
- *UInt32* **effect_duration_ms** - Duration of the effect, in ms.

## void playJoystickForceFeedbackEffectSquareWave ( Int32 joy_id , float force , float attack_force , float fade_force , int phase , UInt32 period_ms , UInt32 attack_length_ms , UInt32 fade_length_ms , UInt32 effect_duration_ms )

Applies the square-wave force-feedback effect with the specified parameters to the joystick with the given ID. Force is applied in a square-wave pattern.
### Arguments

- *Int32* **joy_id** - Joystick ID.
- *float* **force** - Sustain value � the force value in the middle of the force-feedback effect in range [-1, 1]. Negative values mean that the initial direction of the force-feedback effect is towards the left, positive values � to the right.
- *float* **attack_force** - Value at the start of the attack, in range [0, 1].
- *float* **fade_force** - Value at the end of the fade, in range [0, 1].
- *int* **phase** - Positive phase shift, in degrees in range [0, 360].
- *UInt32* **period_ms** - Period of the wave, in ms.
- *UInt32* **attack_length_ms** - Duration of the attack � time period in ms defining how long it takes to reach the force value (the value in the middle of the effect).
- *UInt32* **fade_length_ms** - Duration of the fade out � time period in ms defining how long it takes to fall away from the force value (the value in the middle of the effect).
- *UInt32* **effect_duration_ms** - Duration of the effect, in ms.

## void playJoystickForceFeedbackEffectTriangleWave ( Int32 joy_id , float force , float attack_force , float fade_force , int phase , UInt32 period_ms , UInt32 attack_length_ms , UInt32 fade_length_ms , UInt32 effect_duration_ms )

Applies the triangle-wave force-feedback effect with the specified parameters to the joystick with the given ID. Force is applied in a triangle-wave pattern.
### Arguments

- *Int32* **joy_id** - Joystick ID.
- *float* **force** - Sustain value � the force value in the middle of the force-feedback effect in range [-1, 1]. Negative values mean that the initial direction of the force-feedback effect is towards the left, positive values � to the right.
- *float* **attack_force** - Value at the start of the attack. Value in range [0, 1].
- *float* **fade_force** - Value at the end of the fade. Value in range [0, 1].
- *int* **phase** - Positive phase shift, in degrees in range [0, 360].
- *UInt32* **period_ms** - Period of the wave, in ms.
- *UInt32* **attack_length_ms** - Duration of the attack � time period in ms defining how long it takes to reach the force value (the value in the middle of the effect).
- *UInt32* **fade_length_ms** - Duration of the fade out � time period in ms defining how long it takes to fall away from the force value (the value in the middle of the effect).
- *UInt32* **effect_duration_ms** - Duration of the effect, in ms.

## void playJoystickForceFeedbackEffectSawtoothUpWave ( Int32 joy_id , float force , float attack_force , float fade_force , int phase , UInt32 period_ms , UInt32 attack_length_ms , UInt32 fade_length_ms , UInt32 effect_duration_ms )

Applies the upward-sawtooth-wave force-feedback effect with the specified parameters to the joystick with the given ID. Force is applied in a upward-sawtooth-wave pattern.
### Arguments

- *Int32* **joy_id** - Joystick ID.
- *float* **force** - Sustain value � the force value in the middle of the force-feedback effect in range [-1, 1]. Negative values mean that the initial direction of the force-feedback effect is towards the left, positive values � to the right.
- *float* **attack_force** - Value at the start of the attack. Value in range [0, 1].
- *float* **fade_force** - Value at the end of the fade. Value in range [0, 1].
- *int* **phase** - Positive phase shift, in degrees in range [0, 360].
- *UInt32* **period_ms** - Period of the wave, in ms.
- *UInt32* **attack_length_ms** - Duration of the attack � time period in ms defining how long it takes to reach the force value (the value in the middle of the effect).
- *UInt32* **fade_length_ms** - Duration of the fade out � time period in ms defining how long it takes to fall away from the force value (the value in the middle of the effect).
- *UInt32* **effect_duration_ms** - Duration of the effect, in ms.

## void playJoystickForceFeedbackEffectSawtoothDownWave ( Int32 joy_id , float force , float attack_force , float fade_force , int phase , UInt32 period_ms , UInt32 attack_length_ms , UInt32 fade_length_ms , UInt32 effect_duration_ms )

Applies the downward-sawtooth-wave force-feedback effect with the specified parameters to the joystick with the given ID. Force is applied in a downward-sawtooth-wave pattern.
### Arguments

- *Int32* **joy_id** - Joystick ID.
- *float* **force** - Sustain value � the force value in the middle of the force-feedback effect in range [-1, 1]. Negative values mean that the initial direction of the force-feedback effect is towards the left, positive values � to the right.
- *float* **attack_force** - Value at the start of the attack. Value in range [0, 1].
- *float* **fade_force** - Value at the end of the fade. Value in range [0, 1].
- *int* **phase** - Positive phase shift, in degrees in range [0, 360].
- *UInt32* **period_ms** - Period of the wave, in ms.
- *UInt32* **attack_length_ms** - Duration of the attack � time period in ms defining how long it takes to reach the force value (the value in the middle of the effect).
- *UInt32* **fade_length_ms** - Duration of the fade out � time period in ms defining how long it takes to fall away from the force value (the value in the middle of the effect).
- *UInt32* **effect_duration_ms** - Duration of the effect, in ms.

## void playJoystickForceFeedbackEffectSpring ( Int32 joy_id , float left_force , float left_saturation , float right_force , float right_saturation , float offset , float deadband )

Applies the spring force-feedback effect with the specified parameters to the joystick with the given ID. Force is applied in opposition to a set state.
### Arguments

- *Int32* **joy_id** - Joystick ID.
- *float* **left_force** - Strength of the force-feedback effect that occurs when turning to the left. Value in range [0, 1].
- *float* **left_saturation** - Maximum possible force for the force-feedback effect on turning left. Value in range [0, 1]. Not all devices support saturation.
- *float* **right_force** - Strength of the force-feedback effect that occurs when turning to the right. Value in range [0, 1].
- *float* **right_saturation** - Maximum possible force for the force-feedback effect on turning right. Value in range [0, 1]. Not all devices support saturation.
- *float* **offset** - The offset from the zero reading of the appropriate sensor value at which the condition begins to be applied. For a spring effect, the neutral point - that is, the point along the axis at which the spring would be considered at rest - would be defined by the offset for the condition.
- *float* **deadband** - Zone around the offset of an axis at which the condition is not active. In the case of a spring that is at rest in the middle of an axis, the deadband enlarges this area of rest. Not all devices support deadband.

## void playJoystickForceFeedbackEffectFriction ( Int32 joy_id , float left_force , float left_saturation , float right_force , float right_saturation )

Applies the friction force-feedback effect with the specified parameters to the joystick with the given ID. Force is applied to mimic friction.
### Arguments

- *Int32* **joy_id** - Joystick ID.
- *float* **left_force** - Strength of the force-feedback effect that occurs when turning to the left. Value in range [0, 1].
- *float* **left_saturation** - Maximum possible force for the force-feedback effect on turning left. Value in range [0, 1]. Not all devices support saturation.
- *float* **right_force** - Strength of the force-feedback effect that occurs when turning to the right. Value in range [0, 1].
- *float* **right_saturation** - Maximum possible force for the force-feedback effect on turning right. Value in range [0, 1]. Not all devices support saturation.

## void playJoystickForceFeedbackEffectDamper ( Int32 joy_id , float left_force , float left_saturation , float right_force , float right_saturation )

Applies the damper force-feedback effect with the specified parameters to the joystick with the given ID. Force is applied to mimic a damper effect.
### Arguments

- *Int32* **joy_id** - Joystick ID.
- *float* **left_force** - Strength of the force-feedback effect that occurs when turning to the left. Value in range [0, 1].
- *float* **left_saturation** - Maximum possible force for the force-feedback effect on turning left. Value in range [0, 1]. Not all devices support saturation.
- *float* **right_force** - Strength of the force-feedback effect that occurs when turning to the right. Value in range [0, 1].
- *float* **right_saturation** - Maximum possible force for the force-feedback effect on turning right. Value in range [0, 1]. Not all devices support saturation.

## void playJoystickForceFeedbackEffectInertia ( Int32 joy_id , float force )

Applies the inertia force-feedback effect with the specified parameters to the joystick with the given ID. Force is applied to mimic an inertia effect.
### Arguments

- *Int32* **joy_id** - Joystick ID.
- *float* **force** - Amount of force being applied by a force-feedback effect. Value in range [0, 1].

## void stopJoystickForceFeedbackEffect ( Int32 joy_id , int effect )

Stops application of the specified type of force-feedback effect to the joystick with the given ID.
### Arguments

- *Int32* **joy_id** - Joystick ID.
- *int* **effect** - Type of a force-feedback effect.
