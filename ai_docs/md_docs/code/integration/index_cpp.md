# Integrating with 3rd-Party Software (CPP)


UNIGINE is a powerful platform for developing modern 3D applications, providing a comprehensive toolkit suitable for a wide range of industries and use cases. However, every project is unique, and the final product isn't always a standalone UNIGINE application using only standard, out-of-the-box features. In some cases, practical implementation requires **extending the Engine's core capabilities** - whether through integration with existing professional ecosystems, incorporation of familiar development tools, or unifying multiple components within a single architecture.


Corporate projects may require integrating software solutions powered by UNIGINE into a larger system or developing interoperable UNIGINE-based modules that operate on a client-server model. Implementing such solutions involves setting up data exchange between internal components and external software, as well as integrating with the company's existing infrastructure.


There are three primary ways to integrate with the UNIGINE Engine:


- Adding third-party libraries
- Embedding UNIGINE into another Application
- Integration via Network Communication


Adding third-party libraries to a UNIGINE project allows you to extend functionality beyond the built-in features. Depending on the task, external libraries can provide tools for:


- Physics Simulation: *Havok, Bullet, PhysX*
- Networking and multiplayer: *Photon, RakNet*
- AI and Computer Vision: *Tensorflow, OpenCV, OpenAI Gym*
- Audio Processing: *FMOD, OpenAL*
- Custom UI: *Qt, Dear ImGui*
- Databases: *MySQL, Oracle, Postgres*


If you already have an existing software framework and plan to use UNIGINE primarily for real-time 3D visualization, then embedding UNIGINE into your existing application might be the best option.


For example, if you need to send messages between devices or sync media streams, it�s better to connect through network protocols instead of embedding the Engine directly. Several approaches for network-based integration are described further in this article. Use these methods as a starting point when planning the most suitable integration strategy for your project.


## Adding Third-Party Libraries


UNIGINE Projects are compiled with standard *C++ (MSVC, Clang, GNU)* and *C# (.NET Compiler Platform)* tools, which makes it possible to work with familiar language features and standard libraries. This also ensures that most third-party libraries written in C++ or C# can be integrated into a UNIGINE-based application without significant effort.


> **Notice:** When integrating a third-party library into a UNIGINE project, follow the standard C++ or C# build and linking practices. The exact steps depend on the library: some require copying files, others use dynamic linking, and some follow their own setup instructions. Always check the library's documentation to determine the correct integration method.


After external libraries are added to the project, their functions and methods can be called directly from your UNIGINE code. Depending on your goals and the purpose of the embedded library, this might be as simple as invoking a function when needed (for example, to process, compress, or transform an image). If the library must interact more deeply with the Engine's lifecycle or rendering processes, it is important to plan the integration scheme carefully.


Additional functionality from third-party libraries can be incorporated into a UNIGINE project through:


- **Engine Lifecycle integration**
- **Event-driven integration**


In practice, a combination of these approaches usually works best. However, the choice depends on the specific requirements of your project's functionality.

 Best PracticeFor more details, refer to the articles **[Execution Sequence](../../code/fundamentals/execution_sequence/app_logic_system.md)** and **[Where to Put Your Code](../../code/fundamentals/execution_sequence/code_update.md)**. They describe the specific points at which custom code is executed and provide a list of available Engine events that you can subscribe to.
### Third-Party Library Integration Example


Let's take a look at a typical approach to integrating third-party tools into UNIGINE using the **Dear ImGui** library as an example. **Dear ImGui** provides a convenient way to create graphical user interfaces, and the following example shows how to connect and embed it into a project.


![](dear_imgui.png)


#### Lifecycle-Based Library Integration


> **Notice:** A complete sample project is available on GitHub as *[Dear ImGui C++ Integration](https://github.com/unigine-engine/unigine-imgui-cpp-integration-sample)*. You can use these examples as a reference and [follow the instructions provided in this guide](../../sdk/api_samples/third_party/dear_imgui_cpp.md) to set up the library in your own UNIGINE project.


The **Dear ImGui** library requires implementation of all three main stages: *initialization*, *execution*, and *unloading*. During the execution stage, this library manages the output window and renders the graphical interface.


The developer's task is to establish an interaction between the embedded functionality and the original environment. To enable the use of **Dear ImGui** functions in the UNIGINE project, we have prepared the *ImGuiImpl* proxy class, described in the `ImGuiImpl.h` file.


<details>
<summary>Open | Close</summary>

```cpp
#include <UnigineInput.h>
// Connect Dear ImGUI library
#include "imgui.h"

class ImGuiImpl
{
// Declare functions to be used in the project
public:
	static void init();
	static void newFrame();
	static void render();
	static void shutdown();

private:
	static ImGuiStyle source_style;
	static float last_scale;

	static Unigine::Input::MOUSE_HANDLE prev_mouse_handle;
};

```

</details>


The implementation of these functions is placed in the `ImGuiImpl.cpp` file.


The `AppSystemLogic.cpp` file contains the code required to implement the main library steps:


<details>
<summary>Open | Close</summary>

```cpp
#include "AppSystemLogic.h"
#include <UnigineWorld.h>
#include <UnigineControls.h>
#include <UnigineInput.h>

// Including ImGui proxy class header
#include "ImGuiImpl.h"

using namespace Unigine;

// Initializing the Dear ImGui library in the AppSystemLogic
int AppSystemLogic::init()
{
	Unigine::Engine::get()->setBackgroundUpdate(Engine::BACKGROUND_UPDATE_RENDER_NON_MINIMIZED);

	Unigine::World::loadWorld("imgui");

	// Initialize ImGui backend
	ImGuiImpl::init();

	// Create texture
	custom_texture = Texture::create();
	custom_texture->load("core/textures/common/checker_d.texture");

	return 1;
}

// Executing Dear ImGui library functions in the main loop of a UNIGINE application
int AppSystemLogic::update()
{
	EngineWindowPtr main_window = WindowManager::getMainWindow();
	if (!main_window)
	{
		Engine::get()->quit();
		return 1;
	}

	ImGuiImpl::newFrame();

	// Feel free to use ImGui API here...
	ImGui::ShowDemoWindow();

	// Show custom texture with ImGui
	int image_width = custom_texture->getWidth();
	int image_height = custom_texture->getHeight();

	ImGui::Begin("Texture Test");
	ImGui::Image((ImTextureID)(intptr_t)custom_texture.get(), ImVec2(float(image_width), float(image_height)));
	ImGui::End();

	// Call render
	ImGuiImpl::render();
	return 1;
}

// Unloading the Dear ImGui library in the shutdown
int AppSystemLogic::shutdown()
{
	custom_texture.deleteLater();

	// Shutdown ImGui backend
	ImGuiImpl::shutdown();
	return 1;
}

```

</details>


In this example, the external library is called from System Logic, so all methods are executed according to the Engine's Execution Sequence.


- *init()* � initialization stage (see: [Engine Initialization](../../code/fundamentals/execution_sequence/init.md))
- *update()* � per-frame update stage (see: [Engine Main Loop](../../code/fundamentals/execution_sequence/main_loop.md))
- *shutdown()* � shutdown stage (see: [Engine Shutdown](../../code/fundamentals/execution_sequence/shutdown.md))


#### Event-Based Library Integration


In addition to defining logic through the Engine lifecycle, you can also subscribe to [Engine events](../../code/fundamentals/events/index_cpp.md) and implement functionality within those callbacks. The UNIGINE API provides a wide range of events, most of which are exposed in classes such as *Engine, Render, World, Input*, and others.


The **[Execution Sequence](../../code/fundamentals/execution_sequence/app_logic_system.md)** article contains an overview of the key events triggered by the Engine during runtime. For example, Input events are triggered [here](../../code/fundamentals/execution_sequence/main_loop.md#inputs), and Render events [here](../../code/fundamentals/execution_sequence/main_loop.md#render).


The **Dear ImGui** library is designed for creating user interfaces, so it needs to interact with the input system. In addition to implementing functions for the application's lifecycle, the file `ImGuiImpl.cpp` contains subscriptions to various events that allow the interface to respond to user actions.


<details>
<summary>Open | Close</summary>

```cpp
void ImGuiImpl::init()
{
	Input::setMouseHandle(Input::MOUSE_HANDLE_GRAB);
	prev_mouse_handle = Input::getMouseHandle();

	IMGUI_CHECKVERSION();
	ImGui::CreateContext();

// input event subscription
	Input::getEventKeyDown().connect(connections, on_key_pressed);
	Input::getEventKeyUp().connect(connections, on_key_released);

	Input::getEventMouseDown().connect(connections, on_button_pressed);
	Input::getEventMouseUp().connect(connections, on_button_released);

	Input::getEventTextPress().connect(connections, on_unicode_key_pressed);

// subscription at the beginning of the rendering stage of the Engine to disable the inbuilt UI
	Engine::get()->getEventBeginRender().connect(connections, before_render_callback);

// subscribing to the end of the screen renderer to overlay the ImGUI UI on top of the finished image
	Render::getEventEndScreen().connect(connections, draw_callback);

	...
}

```

</details>


**See Also:**


- Example of integrating **[Photon SDK](../../sdk/api_samples/third_party/photon/index_cpp.md)** into UNIGINE for building multiplayer functionality.
- Example of integrating **FMOD Studio** and **FMOD Core** via the **[FMOD Plugin](../../code/plugins/fmod/index.md)**:

  -
  -


#### Performance Considerations During Integration


When integrating third-party libraries, consider how their logic affects the Engine's lifecycle and rendering (especially if it runs every frame). Use [Profiling Tools](../../tools/profiling/index.md) to measure execution time and detect performance bottlenecks.


If certain library calls take too long, move them to a separate thread to avoid blocking frame rendering (e.g., during large file downloads or heavy data processing).


For example, you can measure the execution time of your custom logic using *[Profiler::begin()](../../api/library/engine/class.profiler_cpp.md#begin_cstr_void)* and *[Profiler::end()](../../api/library/engine/class.profiler_cpp.md#end_float)*:


```cpp
Profiler::start("Dear ImGui")

ImGuiImpl::newFrame();
ImGui::ShowDemoWindow();
int image_width = custom_texture->getWidth();
int image_height = custom_texture->getHeight();
ImGui::Begin("Texture Test");
ImGui::Image((ImTextureID)(intptr_t)custom_texture.get(), ImVec2(float(image_width), float(image_height)));
ImGui::End();
ImGuiImpl::render();

Profiler::end();

```


![](dear_imgui_metric.png)


**See Also:**


- Example of integrating **[Photon SDK](../../sdk/api_samples/third_party/photon/index_cpp.md)** into UNIGINE for building multiplayer functionality.
- Example of integrating **FMOD Studio** and **FMOD Core** via the **[FMOD Plugin](../../code/plugins/fmod/index.md)**:

  -
  -


## Embedding UNIGINE in Third-Party Application


When integrating the UNIGINE Engine into external software or frameworks, there are two general approaches. Both rely on the *SystemProxy*, which defines platform-specific tasks such as window creation, input handling, and interaction with the OS windowing system.


- **Built-in *SystemProxy*** - the default implementation used when **UNIGINE creates and manages its own rendering windows and input events**.
- **Custom *[SystemProxy](../../api/library/engine/class.customsystemproxy_cpp.md)***  - used when the **target application has its own windowing and input systems** (such as **Qt, WPF, WinForms**, etc.). In this case, the proxy acts as an adapter between UNIGINE and the existing environment.


The choice depends on whether the external application uses its own rendering windows and input/event handling. If it does, a ***[CustomSystemProxy](../../api/library/engine/class.customsystemproxy_cpp.md)*** is required.


![](system_proxy.png)


### Using Default System Proxy


The UNIGINE Engine comes in a form of a dynamic library, which allows it to be integrated into external applications using standard C++ practices. This makes it possible to include the Engine in other projects and initialize it directly from your application code.


When we initialize the Engine and hand over control to it using the *[main()](../../api/library/engine/class.engine_cpp.md#main_SystemLogic_ptr_WorldLogic_ptr_EditorLogic_ptr_void)* method (see the example below), it takes full ownership of execution and blocks until the Engine shuts down.


<details>
<summary>Open | Close</summary>

```cpp
#include <UnigineEngine.h>
#include "AppSystemLogic.h"
#include "AppEditorLogic.h"
#include "AppWorldLogic.h"
#ifdef _WIN32
int wmain(int argc, wchar_t *argv[])
#else
int main(int argc, char *argv[])
#endif
{
	// engine initialization
	Unigine::EnginePtr engine(argc, argv);

	AppSystemLogic system_logic;
	AppWorldLogic world_logic;
	AppEditorLogic editor_logic;

	// entering the main loop blocking the external environment
	engine->main(&system_logic, &world_logic, &editor_logic);

	return 0;
}

```

</details>


If you cannot fully block the external application's functions, consider using the *[iterate()](../../api/library/engine/class.engine_cpp.md#iterate_void)* method instead of *[main()](../../api/library/engine/class.engine_cpp.md#main_SystemLogic_ptr_WorldLogic_ptr_EditorLogic_ptr_void)*. It executes one Engine cycle and returns control to the original environment, allowing the application to interact with other tasks.


<details>
<summary>Open | Close</summary>

```cpp
#include <UnigineEngine.h>
#include "AppSystemLogic.h"
#include "AppEditorLogic.h"
#include "AppWorldLogic.h"
#ifdef _WIN32
int wmain(int argc, wchar_t *argv[])
#else
int main(int argc, char *argv[])
#endif
{
	// engine initialization
	Unigine::EnginePtr engine(argc, argv);

	AppSystemLogic system_logic;
	AppWorldLogic world_logic;
	AppEditorLogic editor_logic;

	enigine->addSystemLogic(&system_logic);
	enigine->addWorldLogic(&world__logic);
	enigine->addEditorLogic(&editor_logic);

	// example of loop organization for alternate execution of engine frames

	while (!engine->isQuit())
	{
		// do something
		${#HL}$engine->iterate();${HL#}$
		// do something
	}
	return 0;
}

```

</details>


### Using Custom System Proxy


If you need to extend or adapt interaction for special requirements, external systems, non-standard protocols, data processing, or complex logic scenarios that go beyond the standard UNIGINE APIs, you must develop and implement a system proxy yourself.


The **[CustomSystemProxy](../../api/library/engine/class.customsystemproxy_cpp.md)** interface allows you to delegate platform-specific system tasks from the Engine to an external system or framework. By implementing this interface, your application takes responsibility for providing the system-level services, such as creating the main window or processing user input, and then hands control back to the Engine for rendering and simulation.


You can find more detailed information about creating custom proxies for integration in the "[**Integration with Frameworks**](../../code/cpp/usage/unigine_app/proxy.md)" article.


As an example, you can refer to the C++ sample where UNIGINE integrates with the Qt Framework. The sample is available in the *SDK Browser* with Sim SDK :


In the following snippet, the *CustomSystemProxy* is passed as an argument during the Engine initialization:


<details>
<summary>Open | Close</summary>

```cpp
#include "AppQt.h"
#include "MainWindow.h"
#include "SystemProxyQt.h"

#include <UnigineConsole.h>
#include <UnigineEngine.h>
#include <UnigineWorld.h>
#include <UnigineWindowManager.h>

#ifdef _WIN32
int wmain(int argc, wchar_t *wargv[])
{
	char **argv = nullptr;
#else
int main(int argc, char *argv[])
{
#endif
	...

	AppQt app(argc, argv);
	SystemProxyQt system_proxy;

	// Engine initialization
	Unigine::Engine::InitParameters init_params;
	init_params.system_proxy = &system_proxy;

	Unigine::EnginePtr engine(init_params, argc, argv);
	Unigine::World::loadWorld("viewport_world");

	// Starting the main window
	MainWindow main_window(&system_proxy);
	main_window.setWindowTitle(MainWindow::tr("UNIGINE Engine: C++ Qt integration"));

	app.startEngineLoop();

	main_window.show();

	return AppQt::exec();
}
}

```

</details>


During updates, the *[iterate()](../../api/library/engine/class.engine_cpp.md#iterate_void)* method is called. This transfers control to the Engine for a single frame and then returns it back to the Qt application:


<details>
<summary>Open | Close</summary>

```cpp
void AppQt::timerEvent(QTimerEvent *event)
{
	if (event->timerId() == timer_update_id_)
	{
		if (false == engine_->isQuit())
		{
			// execution of one engine cycle
			${#HL}$engine_->iterate();${HL#}$
		}
		else
		{
			killTimer(timer_update_id_);
			timer_update_id_ = -1;
			exit();
		}
	}
	else
	{
		QApplication::timerEvent(event);
	}
}

```

</details>


**See Also:**


- General "[**Integration with Frameworks**](../../code/cpp/usage/unigine_app/proxy.md)" article, describing the usage of [CustomSystemProxy](../../api/library/engine/class.customsystemproxy_cpp.md) class API
- [**WPF Integration sample**](../../code/csharp/usage/unigine_app/wpf_integration/index.md) availabe for the C# API.
- [**Qt Integraion sample**](../../code/cpp/usage/unigine_app/AppQt.md) available for the C++ API.
- [**Viewer Demo**](../../sdk/demos/viewer.md) - demo-project built on top of the Qt Integration sample that demonstrates how to create a complete application using both UNIGINE and the Qt framework.


## Network Communication


When UNIGINE is used alongside other applications or services, direct code integration is not always the best approach. In such cases, applications can interact at runtime through **network communication**. This makes it possible to exchange data between independent processes (even when they run on different machines) and enables integration with external tools, real-time simulators, automation systems, or cloud services.


> **Notice:** If you already have a networking solution in place, it's best to use it as the foundation for integrating with UNIGINE. This ensures consistent data formats and clean interoperability.
>
>
> See the [first section for guidance](#libraries) on integrating third-party libraries.


### Low-Level Networking


UNIGINE provides socket-level access for direct data exchange between the Engine and external applications.


Communication is performed at the transport level and all interactions are handled manually, including message formatting, sending, receiving, and parsing. This gives full flexibility but also makes the solution heavily implementation-dependent.


For basic non-confidential data exchange, you can use **TCP** (if reliability is important) or **UDP** (if transmission speed is critical). UNIGINE provides the *[Socket](../../api/library/networking/class.socket_cpp.md)* class for working directly with these protocols.


If data confidentiality is required, use the *[SSLSocket](../../api/library/networking/class.sslsocket_cpp.md)* class, which enables secure network communication based on the *TLS* cryptographic protocol and public key encryption.


The following samples are available in the *SDK Browser*:


-
-
-


![](client_server.png)


For example, using this as a foundation, you can implement higher-level protocols such as **MQTT**, which operates on top of TCP and provides a publish/subscribe messaging model for telemetry systems, external controllers or **IoT** devices.


### HTTP Communication


To exchange data with external systems (for example, retrieving weather conditions or equipment status in real time) or to control the application over HTTP, you can use the *[cpp-httplib](https://github.com/yhirose/cpp-httplib)* library.


The SDK includes set of samples that demonstrate how to use this library to perform HTTP requests. This allows the application to interact with web services and *REST* endpoints without implementing raw socket communication. The available samples are:


-
-
- Screenshot to HTTP Response
- HTTP REST Request
- HTTP Server


### Integration with Professional Simulation Protocols


**[Image Generator (IG)](../../ig/index.md)** - a ready-to-use template recommended for integrating professional simulators that rely on protocols such as *CIGI, DIS*, or *HLA*. It provides industry-standard image generation capabilities with minimal setup.


![](../../ig/protocols.png)


### Plugins Networking


UNIGINE includes several plugins that use network communication to interact with external systems and distributed environments.


#### Network Video Streaming


**[WebStream plugin](../../code/plugins/webstream/index.md)** - enables video streaming over the network to multiple devices and supports two-way interaction, allowing rendered frames to be produced on a powerful workstation while user input is received from remote devices.

     Sorry, your browser does not support embedded videos.
#### Multi-Channel Rendering Synchronization


**[Syncker plugin](../../code/plugins/syncker/index.md)** - used for multi-channel visualization across network clusters. It synchronizes rendering and simulation in real time between a master node and multiple slave nodes, providing robust and reliable frame-to-frame synchronization.


![](../../code/plugins/syncker/syncker.png)


#### Runtime Data Exchange with External Apps


**[DataBridge plugin](../../code/plugins/databridge/index_cpp.md)** - designed to exchange dynamic data between a UNIGINE application and external tools such as sensors, control systems, Python scripts, or IoT devices. It provides a universal API and uses RUDP for fast and secure communication over the network.


To help you get started quickly, the plugin is supplied with a sample. It demonstrates a simplified vehicle model and a basic data flow:


- The Engine initializes a server and sends vehicle data (sensor values).
- A Python script reads this data, recalculates speed and steering values, and prepares control signals.
- The values are sent back to the server, and the Engine applies them to the vehicle model.


![](databridge_car.gif)

*Data Exchange via DataBridge Plugin*


Python is used only as an example - any external application can act as a data provider or receiver.


#### Database Integration


**[SQL Plugin](../../code/plugins/sql/index.md)** - provides access to SQL databases and can be used both with local and remote database servers. It supports standard request-response operations and several built-in UNIGINE data types, as well as asynchronous queries executed in a separate thread.


### Solutions for Gaming Applications


For implementing multiplayer features, review the sample for integrating the **[Photon](https://www.photonengine.com/)** framework into UNIGINE. This tool enables networked interaction between players.


The [**Photon Integration Sample**](../../sdk/api_samples/third_party/photon/index_cpp.md), available in the *SDK Browser*, includes several useful examples:


- *Simplified user login authorization*
- *Lobby interface for creating shared rooms and viewing available rooms*
- *Chat window for exchanging messages between users*


Additionally, you can use the *[Steam Plugin](../../code/plugins/steam/index.md)* to simplify integration with this service.
