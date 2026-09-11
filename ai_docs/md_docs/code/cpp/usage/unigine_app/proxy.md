# Integrating with Frameworks


To integrate UNIGINE Engine with another system (for example Qt, SDL, WPF, WinForms, etc.), you can use the *[Unigine::CustomSystemProxy](../../../../api/library/engine/class.customsystemproxy_cpp.md)* class. Its concept incorporates the definition of available functions (window creation and management, input management, additional functionality such as dialogs, clipboard, etc.) along with all necessary overrides.


The functionality of some engine subsystems is defined depending on the set of functions made available by the user. This class forms the basis for the operation of *[WindowManager](../../../../api/library/gui/class.windowmanager_cpp.md), [Input](../../../../api/library/controls/class.input_cpp.md), [GUI](../../../../api/library/gui/class.gui_cpp.md), [Displays](../../../../api/library/gui/class.displays_cpp.md)*, etc.


The *CustomSystemProxy*-based workflow allows the following:


- Creating a window without using the platform-dependent code
- Creating a separate rendering window without any plugins
- Implementing the window creation functionality, which is common for all applications
- Obtaining information on the physical configuration of displays
- Providing full functionality of the main window for other windows (*GUI, Input*, etc.)


> **Notice:** A separate proxy implementation is required for each integration environment (*SystemProxySDL, SystemProxyQt*, etc.).


## Integration Workflow


To correctly use the *CustomSystemProxy* class, you should do the following:


1. Include the `UnigineCustomSystemProxy.h` header file into the source code.
2. Create a custom class and inherit it from the *[Unigine::CustomSystemProxy](../../../../api/library/engine/class.customsystemproxy_cpp.md)* class.
3. Override all virtual functions specified in the `include/UnigineCustomSystemProxy.h` file.
4. Define the supported features via the proxy constructor (the *[SYSTEM_PROXY_*](../../../../api/library/engine/class.customsystemproxy_cpp.md#SYSTEM_PROXY_WINDOWS)* variables).
5. Implement the functions according to the list of the supported features, including event handling and rendering into an external window, if required.


> **Notice:** The full-featured example of integrating UNIGINE Engine into the QT framework can be found in the `source/apps/main_qt` folder (`SystemProxyQt.h`, `SystemProxyQt.cpp`).


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


### Creating System Proxy


When creating a system proxy, you can specify the features it will support: pass the required *[SYSTEM_PROXY_*](../../../../api/library/engine/class.customsystemproxy_cpp.md#SYSTEM_PROXY_WINDOWS)* variables to the constructor. For example:


<details>
<summary>SystemProxyQt.cpp | Close</summary>

```cpp
// create a proxy that can work with the mouse and keyboard and create windows
SystemProxyQt::SystemProxyQt()
: CustomSystemProxy(SYSTEM_PROXY_WINDOWS | SYSTEM_PROXY_MOUSE | SYSTEM_PROXY_KEYBOARD)
{
}

```

</details>


You can check if the feature is supported by using the [corresponding function](../../../../api/library/engine/class.customsystemproxy_cpp.md#isWindowsSupported_bool). Also you can get the supported features via *[getFeatures()](../../../../api/library/engine/class.customsystemproxy_cpp.md#getFeatures_int)*.


<details>
<summary>SystemProxyQt.cpp | Close</summary>

```cpp
WIN_HANDLE SystemProxyQt::createWindow(int width, int height)
{
	// check if window creation is supported
	if (0 == isWindowsSupported())
	{
		return WIN_HANDLE();
	}

	WIN_HANDLE result;

	// createWindow() implementation
	...
}

```

</details>


### Event Handling


Information on data input or window interaction is passed to the engine by using *events*. There are:


- **[Input events](../../../../api/library/controls/class.inputevent_cpp.md)** for the mouse, keyboard, text, sensor input, joysticks, gamepads and system events (*[InputEventMouseButton](../../../../api/library/controls/class.inputeventmousebutton_cpp.md), [InputEventKeyboard](../../../../api/library/controls/class.inputeventkeyboard_cpp.md)*, etc.).
- **[Window events](../../../../api/library/gui/class.windowevent_cpp.md)** for windows (*[WindowEventGeneric](../../../../api/library/gui/class.windoweventgeneric_cpp.md), [WindowEventDrop](../../../../api/library/gui/class.windoweventdrop_cpp.md)*).


When the events are created, they can be passed to the engine by using the *[invokeWindowEvent()](../../../../api/library/engine/class.customsystemproxy_cpp.md#invokeWindowEvent_WindowEventPtr_void)* and *[invokeInputEvent()](../../../../api/library/engine/class.customsystemproxy_cpp.md#invokeInputEvent_InputEventPtr_void)* methods of the CustomSystemProxy class.


<details>
<summary>SystemProxyQt.cpp | Close</summary>

```cpp
bool SystemProxyQt::invoke_input_event(const QEvent *q_event)
{
	...
	switch (q_event->type())
	{
	case QEvent::Wheel:
	{
		auto e = static_cast<const QWheelEvent *>(q_event);

		const QPoint delta = e->angleDelta() / 120;
		const Math::ivec2 scroll(delta.x(), delta.y());
		const auto timestamp = get_timestamp();
		const Math::ivec2 mouse_pos(e->globalX(), e->globalY());

		// create the mouse wheel input event
		auto wheel_event = InputEventMouseWheel::create(timestamp, mouse_pos, scroll);
		// convey the input event to WindowManager
		invokeInputEvent(wheel_event);
	}
	break;
	...
	// process the other events
}

```

</details>


### Rendering to External Window


UNIGINE allows **registering** any external window for rendering by using the following methods:


- *[initExternalWindowBuffers()](../../../../api/library/engine/class.customsystemproxy_cpp.md#initExternalWindowBuffers_WIN_HANDLE_const_ivec2_ref_bool)* initializes the required resources in the engine for rendering to the external window.
- *[resizeExternalWindowBuffers()](../../../../api/library/engine/class.customsystemproxy_cpp.md#resizeExternalWindowBuffers_WIN_HANDLE_const_ivec2_ref_bool)* passes to the engine new window dimensions after its resizing, so that the engine can update rendering resources.
- *[shutdownExternalWindowBuffers()](../../../../api/library/engine/class.customsystemproxy_cpp.md#shutdownExternalWindowBuffers_WIN_HANDLE_bool)* deletes all resources used for rendering to the external window upon closing the window (or when rendering to the window is no longer required).


**Rendering** to the external window is performed by using the following virtual methods:


- *[needRenderExternalWindow()](../../../../api/library/engine/class.customsystemproxy_cpp.md#needRenderExternalWindow_WIN_HANDLE_bool)* checks rendering of the external window. If the window is minimized, occluded by other windows and so on, you can pass this information to the engine (for example, to stop rendering).
- *[onExternalWindowRender()](../../../../api/library/engine/class.customsystemproxy_cpp.md#onExternalWindowRender_WIN_HANDLE_void)* � a callback function, which is called on rendering of the external window. It receives the window handle, and you can render to the window at this point.


> **Notice:** As these methods are virtual, you will need to override them.


<details>
<summary>SystemProxyQt.h | Close</summary>

```cpp
...

// external window into which rendering is performed
class ExternalWindow
{
public:
	virtual ~ExternalWindow() = default;

	virtual void doRender() {}
	virtual void doUpdate() {}
	virtual void doSwap() {}
	virtual bool isRendering() const { return true; }
};

// CustomSystemProxy-based class
class SystemProxyQt final : public Unigine::CustomSystemProxy
{
public:
	...
	// override virtual functions
	int needRenderExternalWindow(Unigine::WIN_HANDLE win_handle) override;
	void onExternalWindowRender(Unigine::WIN_HANDLE win_handle) override;
	...

private:
	// declare necessary variables
	Unigine::HashMap<uint64_t, ExternalWindow *> external_id_to_window_;
	...
}

```

</details>


<details>
<summary>SystemProxyQt.cpp | Close</summary>

```cpp
...

// check if the external window is rendered
int SystemProxyQt::needRenderExternalWindow(WIN_HANDLE win_handle)
{
	const auto it = external_id_to_window_.find(win_handle.win_id);
	if (it != external_id_to_window_.end())
	{
		return it->data->isRendering();
	}

	return 0;
}

// implement logic that will be executed on external window rendering
void SystemProxyQt::onExternalWindowRender(WIN_HANDLE win_handle)
{
	const auto it = external_id_to_window_.find(win_handle.win_id);
	if (it != external_id_to_window_.end())
	{
		it->data->doRender();
	}
}

...

```

</details>
