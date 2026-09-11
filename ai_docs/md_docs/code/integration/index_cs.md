# Integrating with 3rd-Party Software (CS)


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


> **Notice:** A complete sample project is available on GitHub as *[Dear ImGui C# Integration](https://github.com/unigine-engine/unigine-imgui-csharp-integration-sample)*. You can use these examples as a reference and [follow the instructions provided in this guide](../../sdk/api_samples/third_party/dear_imgui_cs.md) to set up the library in your own UNIGINE project.


The **Dear ImGui** library requires implementation of all three main stages: initialization, execution, and unloading. During the execution stage, this library manages the output window and renders the graphical interface.


The developer's task is to establish an interaction between the embedded functionality and the original environment. In the *Dear ImGui C# Integration* sample, the file `AppSystemLogic.cs` contains the code for these stages of the library's operation.


<details>
<summary>Open | Close</summary>

```csharp
using System;

using Unigine;

// Importing the Dear ImGui C# wrapper
using ImGuiNET;

internal class UnigineApp
{
	class AppSystemLogic : SystemLogic
	{
		private Texture custom_texture;

		// Initializing the Dear ImGui library in the UNIGINE application initialization block
		public override bool Init()
		{
			Engine.BackgroundUpdate = Engine.BACKGROUND_UPDATE.BACKGROUND_UPDATE_RENDER_NON_MINIMIZED;
			Unigine.Console.Run("world_load data/imgui");

			// Create texture
			custom_texture = new Texture();
			custom_texture.Load("core/textures/common/checker_d.texture");

			// Initialize ImGui backend, set up the Engine
			ImGuiImpl.Init();
			return true;
		}

		// Executing Dear ImGui library functions in the main loop of a UNIGINE application
		public override bool Update()
		{
			EngineWindow main_window = WindowManager.MainWindow;
			if (main_window == null)
			{
				Engine.Quit();
				return true;
			}

			ImGuiImpl.NewFrame();

			// Feel free to use ImGui API here...
			ImGui.ShowDemoWindow();

			// Show custom texture with ImGui
			ImGui.Begin("Texture Test");
			ImGui.Image(custom_texture.GetPtr(), new System.Numerics.Vector2(custom_texture.GetWidth(), custom_texture.GetHeight()));
			ImGui.End();

			// Render implementation
			ImGuiImpl.Render();
			return true;
		}

		// Unloading the Dear ImGui library in the UNIGINE application shutdown block
		public override bool Shutdown()
		{
			custom_texture.DeleteLater();

			// shutdown ImGui backend
			ImGuiImpl.Shutdown();

			return true;
		}
	}
}

```

</details>


#### Event-Based Library Integration


In addition to defining logic through the Engine lifecycle, you can also subscribe to [Engine events](../../code/fundamentals/events/index_cs.md) and implement functionality within those callbacks. The UNIGINE API provides a wide range of events, most of which are exposed in classes such as *Engine, Render, World, Input*, and others.


The **[Execution Sequence](../../code/fundamentals/execution_sequence/app_logic_system.md)** article contains an overview of the key events triggered by the Engine during runtime. For example, Input events are triggered [here](../../code/fundamentals/execution_sequence/main_loop.md#inputs), and Render events [here](../../code/fundamentals/execution_sequence/main_loop.md#render).


The **Dear ImGui** library is designed for creating user interfaces, so it needs to interact with the input system. In addition to implementing functions for the application's lifecycle, the file `ImGuiImpl.cs` contains subscriptions to various events that allow the interface to respond to user actions.


<details>
<summary>Open | Close</summary>

```csharp
public static void Init()
{
	prev_mouse_handle = Input.MouseHandle;

	ImGui.CreateContext();

	// subscription to input events
Input.EventKeyDown.Connect(connections, on_key_pressed);
	Input.EventKeyUp.Connect(connections, on_key_released);

	Input.EventMouseDown.Connect(connections, on_button_pressed);
	Input.EventMouseUp.Connect(connections, on_button_released);

	Input.EventTextPress.Connect(connections, on_unicode_key_pressed);

// subscription to the beginning of the rendering stage of the Engine to disable the embedded UI
	Engine.EventBeginRender.Connect(connections, before_render_callback);

// subscribe to the end of screen rendering to overlay ImGUI UI on top of the finished image
	Unigine.Render.EventEndScreen.Connect(connections, draw_callback);

	...
}

```

</details>


#### Performance Considerations During Integration


When integrating third-party libraries, consider how their logic affects the Engine's lifecycle and rendering (especially if it runs every frame). Use [Profiling Tools](../../tools/profiling/index.md) to measure execution time and detect performance bottlenecks.


If certain library calls take too long, move them to a separate thread to avoid blocking frame rendering (e.g., during large file downloads or heavy data processing).


For example, you can measure the execution time of your custom logic using *[Profiler.Begin()](../../api/library/engine/class.profiler_cs.md#begin_cstr_void)* and *[Profiler.End()](../../api/library/engine/class.profiler_cs.md#end_float)*:


```csharp
Profiler.Begin("Dear ImGui");

ImGuiImpl.NewFrame();
ImGui.ShowDemoWindow();
ImGui.Begin("Texture Test");
ImGui.Image(custom_texture.GetPtr(), new System.Numerics.Vector2(custom_texture.GetWidth(), custom_texture.GetHeight()));
ImGui.End();
ImGuiImpl.Render();

Profiler.End();

```


![](dear_imgui_metric.png)


**See Also:**


- Example of integrating **[Photon SDK](../../sdk/api_samples/third_party/photon/index_cs.md)** into UNIGINE for building multiplayer functionality.
- Example of integrating **FMOD Studio** and **FMOD Core** via the **[FMOD Plugin](../../code/plugins/fmod/index.md)**:

  -
  -


## Embedding UNIGINE in Third-Party Application


When integrating the UNIGINE Engine into external software or frameworks, there are two general approaches. Both rely on the *SystemProxy*, which defines platform-specific tasks such as window creation, input handling, and interaction with the OS windowing system.


- **Built-in *SystemProxy*** - the default implementation used when **UNIGINE creates and manages its own rendering windows and input events**.
- **Custom *[SystemProxy](../../api/library/engine/class.customsystemproxy_cs.md)***  - used when the **target application has its own windowing and input systems** (such as **Qt, WPF, WinForms**, etc.). In this case, the proxy acts as an adapter between UNIGINE and the existing environment.


The choice depends on whether the external application uses its own rendering windows and input/event handling. If it does, a ***[CustomSystemProxy](../../api/library/engine/class.customsystemproxy_cs.md)*** is required.


![](system_proxy.png)


### Using Default System Proxy


The UNIGINE Engine comes in a form of a dynamic library, which allows it to be integrated into external applications using standard C++ practices. This makes it possible to include the Engine in other projects and initialize it directly from your application code.


When we initialize the Engine and hand over control to it using the *[Main()](../../api/library/engine/class.engine_cs.md#main_SystemLogic_ptr_WorldLogic_ptr_EditorLogic_ptr_void)* method (see the example below), it takes full ownership of execution and blocks until the Engine shuts down.


<details>
<summary>Open | Close</summary>

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;

using Unigine;

namespace UnigineApp
{
	internal class UnigineApp
	{
		[STAThread]
		private static void Main(string[] args)
		{
		// engine initialization
			Engine.Init(args);

			AppSystemLogic systemLogic = new AppSystemLogic();
			AppWorldLogic worldLogic = new AppWorldLogic();
			AppEditorLogic editorLogic = new AppEditorLogic();

			// entering the main loop blocking the external environment
			Engine.Main(systemLogic, worldLogic, editorLogic);

			Engine.Shutdown();
		}
	}
}

```

</details>


If you cannot fully block the external application's functions, consider using the *[Iterate()](../../api/library/engine/class.engine_cs.md#iterate_void)* method instead of *[Main()](../../api/library/engine/class.engine_cs.md#main_SystemLogic_ptr_WorldLogic_ptr_EditorLogic_ptr_void)*. It executes one Engine cycle and returns control to the original environment, allowing the application to interact with other tasks.


<details>
<summary>Open | Close</summary>

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;

using Unigine;

namespace UnigineApp
{
	internal class UnigineApp
	{
		[STAThread]
		private static void Main(string[] args)
		{
			// Engine initialization
			Engine.Init(args);

			AppSystemLogic systemLogic = new AppSystemLogic();
			AppWorldLogic worldLogic = new AppWorldLogic();
			AppEditorLogic editorLogic = new AppEditorLogic();

			Engine.AddSystemLogic(systemLogic);
			Engine.AddWorldLogic(worldLogic);
			Engine.AddEditorLogic(editorLogic);

			// Example of loop organization for alternate execution of engine frames
			while (!Engine.IsQuit)
			{
				// do something
				${#HL}$Engine.Iterate();${HL#}$
				// do something
			}

			Engine.Shutdown();
		}
	}
}

```

</details>


### Using CustomSystemProxy


If you need to extend or adapt interaction for special requirements, external systems, non-standard protocols, data processing, or complex logic scenarios that go beyond the standard UNIGINE APIs, you must develop and implement a system proxy yourself.


The **[CustomSystemProxy](../../api/library/engine/class.customsystemproxy_cs.md)** interface allows you to delegate platform-specific system tasks from the Engine to an external system or framework. By implementing this interface, your application takes responsibility for providing the system-level services, such as creating the main window or processing user input, and then hands control back to the Engine for rendering and simulation.


You can find more detailed information about creating custom proxies for integration in the "[**Integration with Frameworks**](../../code/csharp/usage/unigine_app/proxy.md)" article.


As an example, you can refer to the C# sample where UNIGINE integrates with the WPF Framework. The sample is available in the *SDK Browser* with Sim SDK : **[WPF Integration](../../code/csharp/usage/unigine_app/wpf_integration/index.md)**.


In the following snippet, the CustomSystemProxy is passed as an argument during engine initialization:


<details>
<summary>Open | Close</summary>

```csharp
// initialize engine
if (isInitPaint && Engine.IsInitialized == false)
{
	isInitPaint = false;

	List<string> args = Environment.GetCommandLineArgs().ToList();
	args.Add("-dpi_awareness");
	args.Add("-1");

	Engine.InitParameters init_params = new Engine.InitParameters();
	init_params.system_proxy = SystemProxyWPF.Instance;

	Engine.Init(init_params, args.ToArray());

	WPFApplication.ExternalWindow.InitExternalWindows();

	// setting forced focus in main window
	Focus();
	SystemProxyWPF.Instance.invokeWindowEvent(MainWindow.First.getGenericEvent(WindowEventGeneric.ACTION.FOCUS_GAINED));
}

```

</details>


During updates, the *[Iterate()](../../api/library/engine/class.engine_cs.md#iterate_void)* method is called, while all the actions from WPF application are defined in events:


```csharp
// Main loop
if (mainLoopWindow == Handle)
{
	if (Engine.IsInitialized && !Engine.IsQuit)
		${#HL}$Engine.Iterate();${HL#}$

	Invalidate();
}

```


**See Also:**


- General "[**Integration with Frameworks**](../../code/csharp/usage/unigine_app/proxy.md)" article, describing the usage of the *[CustomSystemProxy](../../api/library/engine/class.customsystemproxy_cs.md)* class API
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


For basic non-confidential data exchange, you can use **TCP** (if reliability is important) or **UDP** (if transmission speed is critical). UNIGINE provides the *[Socket](../../api/library/networking/class.socket_cs.md)* class for working directly with these protocols.


If data confidentiality is required, use the *[SSLSocket](../../api/library/networking/class.sslsocket_cs.md)* class, which enables secure network communication based on the *TLS* cryptographic protocol and public key encryption.


The following samples are available in the *SDK Browser*:


-
-
-


![](client_server.png)


For example, using this as a foundation, you can implement higher-level protocols such as **MQTT**, which operates on top of TCP and provides a publish/subscribe messaging model for telemetry systems, external controllers or **IoT** devices.


### HTTP Communication


The SDK includes set of samples that demonstrate how to use the *System.Net.Http* to perform HTTP requests. This allows the application to interact with web services and REST endpoints without implementing raw socket communication (for example, retrieving weather conditions or equipment status in real time or to control the application over HTTP). The available samples are:


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


**[DataBridge plugin](../../code/plugins/databridge/index_cs.md)** - designed to exchange dynamic data between a UNIGINE application and external tools such as sensors, control systems, Python scripts, or IoT devices. It provides a universal API and uses RUDP for fast and secure communication over the network.


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


The [**Photon Integration Sample**](../../sdk/api_samples/third_party/photon/index_cs.md), available in the *SDK Browser*, includes several useful examples:


- *Simplified user login authorization*
- *Lobby interface for creating shared rooms and viewing available rooms*
- *Chat window for exchanging messages between users*


Additionally, you can use the *[Steam Plugin](../../code/plugins/steam/index.md)* to simplify integration with this service.
