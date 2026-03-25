# Creating C++ Plugin


A custom library module (`*.dll` or `*.so` file) containing a set of services and functions can be loaded and used in your UNIGINE application. Implementing such a library via the ***[Plugin](../../api/library/common/class.plugin_cpp.md)*** class interface enables you to leverage the UNIGINE Plugin System to add and manage extra functionality in UNIGINE run-time, choosing which libraries to load on-the-fly without recompiling a UNIGINE executable.


This means, you can **pack** your own functionality into a plugin, **reuse** in other projects, **share** with your team or even **publish** the plugin on the **[UNIGINE Add-On Store](https://store.unigine.com/)** and turn it into a tool, that other developers can use *for free* or as a *paid product*.


To extend UNIGINE functionality, you can develop two types of plugins:


- **[Editor Plugin](../../editor2/extensions/custom_plugin.md)** - plugins that extend the capabilities of the UNIGINE Editor. For example, you can add custom editors for objects, implement viewport overlays and create UI panels for custom tools.
- **Engine Plugin** - plugins that extend the core functionality of the Engine. For instance, you can integrate a third-party SDK or add new rendering features.


Before starting the implementation, make sure to review the naming conventions for plugin files and their correct placement within the project structure.


> **Notice:** This article covers the creation of **Engine Plugins** only. To learn how to create Editor Plugins, please refer to [this article](../../editor2/extensions/custom_plugin.md).


### See Also


- [Ready-to-use plugins](../../code/plugins/index.md) shipped with the ***UNIGINE SDK***
- Specify custom plugin paths using the *[BootConfig](../../api/library/engine/class.bootconfig_cpp.md)* class.
- See the *[Engine](../../api/library/engine/class.engine_cpp.md)* class for methods to add, remove, retrieve information, and perform other plugin-related operations.


## Plugin Naming Conventions


Libraries compiled by you should follow the UNIGINE naming convention:


- Windows Binaries: **<VendorName><PluginName>_plugin_<precision>_x64<debug_version>.***
- Linux Binaries: **lib<VendorName><PluginName>_plugin_<precision>_x64<debug_version>.so**


> **Notice:** Editor plugins require the **_editorplugin** postfix instead of **_plugin**.


**Clarifications:**


**<precision>** - specifies the coordinate precision:


- **Single precision** - this field is omitted
- **Double precision** - the word ***double*** is used


**<debug_version>** - specifies the build configuration:


- **Release build** - this field is omitted
- **Debug build** - ***d*** postfix is added


An example: `VendorPluginName_plugin_double_x64d.dll`.


Thus, to cover all possible use cases (two operating systems, two coordinate precisions, and two build configurations), you would need to build eight binaries. However, providing the full set is not required - you can compile only the variants required for your project.


## Path to Plugin Files


User plugin files should be placed in the appropriate folders. They may depend on third-party libraries and include additional content such as images or models. A plugin, at minimum, consists of a single binary file. However, you may also distribute additional assets such as content, documentation and full source code.


The recommended structure for exporting a plugin is as follows:


- binaries - `bin\plugins\<VendorName>\<PluginName>` (e.g. *bin\plugins\Vendor\Plugin\VendorPlugin_plugin_double_x64.dll*)
- headers and extension files - `include\plugins\<VendorName>\<PluginName>\<VendorName><PluginName>.h` (e.g. *include\plugins\Vendor\Plugin\VendorPlugin.h*)
- third-party libraries - `lib\plugins\<VendorName>\<PluginName>\`
- docs and plugin description - `docs\plugins\<VendorName>\<PluginName>\`
- plugin-related content files - `data\plugins\<VendorName>\<PluginName>\`


Following this structure ensures that plugins are automatically detected and loaded by the Engine, and stay simple to distribute and maintain across other developers.


Plugins distributed with the UNIGINE SDK follow the same structure.


## 1) Set Up the Plugin Project


To create a plugin, use the built-in **Engine Plugin Template**. You can select this option when creating a new project.


You must also fill in the **Plugin Name** and **Plugin Vendor** fields. These values are used to automatically generate the plugin project structure and ensure compliance with [naming conventions](#naming).


![](template_engine_plugin.png)

*Template Engine Pluginin theCreate New Projecttab*


> **Notice:** For an existing project, go to *Other Actions -> Configure*, then choose the desired feature and click *[Configure Project](../../sdk/projects/index_cpp.md#update_config)*.


After this step, a default plugin project will be added to your UNIGINE project's folder. All required files will be added according to [path conventions](#path_to_plugin_files) and your API/IDE project settings:


- **Windows OS: C++ (Qt-based / CMake) or UnigineScript** - *CMake* will be used to build your plugin.
- **Windows OS: C# (.NET) or C++ (Visual Studio)** - a `.vcxproj` project will be created and *Visual Studio 2022* will be used to build your plugin.
- **Linux** - *CMake* will be used to build your plugin regardless of project configuration.


According to the naming conventions, the template build configuration and minimal plugin implementation files will be placed in the following folder of your project:


`source/plugins/<YourVendorName>/<YourPluginName>`


## 2) Implement Plugin's Logic


You can now open the plugin project in your preferred IDE or code editor and explore its contents.


The header file defines a virtual interface inherited from the *[Plugin](../../api/library/common/class.plugin_cpp.md)* class. This approach allows you to expose the API while keeping the source code closed, if necessary, when distributing the plugin.


For example, if you named your plugin **"MyPlugin"**, the implementation would look as follows:


<details>
<summary>Plugin Header | Close</summary>

```cpp
#pragma once

#include <UniginePlugin.h>

class MyPlugin: public Unigine::Plugin
{
public:
	// Constructor and destructor
	MyPlugin();
	virtual ~MyPlugin() override;

	// Plugin identification and configuration
	int getCompilationFlags() const override;
	const char *get_name() override;
	void *get_data() override;
	int get_order() override;

	// Plugin lifecycle
	int init() override;
	int shutdown() override;

	// Per-frame update logic
	void update() override;
	void postUpdate() override;
	void updatePhysics() override;
	void swap() override;

	// Rendering and GUI operations
	void render(const Unigine::EngineWindowViewportPtr &window) override;
	void gui(const Unigine::EngineWindowViewportPtr &window) override;

	// World loading and saving
	int loadWorld(const Unigine::XmlPtr &xml) override;
	int saveWorld(const Unigine::XmlPtr &xml) override;
};

```

</details>


The following plugin methods should be implemented to ensure clean integration with the Engine, for example:


- **Constructor** - called when the plugin instance is created.
- **Destructor** - called when the plugin instance is destroyed.
- **[init()](../../api/library/common/class.plugin_cpp.md#init_int)** method - initializes the plugin (called once the Engine loads it). You can put your code to perform specific actions needed to initialize your plugin (if any).
- **[shutdown()](../../api/library/common/class.plugin_cpp.md#shutdown_int)** method - called when the plugin is unloaded. You can put here your code to be executed on unloading the plugin (some specific cleanup and other actions if necessary).
- **[get_name()](../../api/library/common/class.plugin_cpp.md#get_name_const_char_ptr)** method - returns the unique name of the plugin. This name is used to find and manage (load, unload, etc.) the plugin.
- **[get_order()](../../api/library/common/class.plugin_cpp.md#get_order_int)** method - defines the execution order of the plugin relative to other plugins. If omitted, the plugin will have the default execution order 0.
- **[get_data()](../../api/library/common/class.plugin_cpp.md#get_data_void_ptr)** method - customarily used to get a pointer to the main (public) interface of the plugin. Can be omitted if not required.


Plugins with lower order values are initialized and executed earlier (a plugin with order 1 is executed before a plugin with order 2). This ensures that dependencies between plugins are properly resolved (e.g. core service plugin must be loaded before plugins that rely on it.)


If your plugin is expected to operate in sync with the Engine lifecycle (so it can perform actions on per-frame basis), you can implement an *update(), render(), swap()* and other methods available in the *[Plugin](../../api/library/common/class.plugin_cpp.md)* class. These methods will be automatically called on the corresponding stage of the Engine [Execution Sequence](../../code/fundamentals/execution_sequence/index.md).


The `.cpp` file contains the actual implementation logic of your plugin.


<details>
<summary>Plugin Implementation | Close</summary>

```cpp
#include "MyPlugin.h"
using namespace Unigine;

extern "C" UNIGINE_EXPORT void *CreatePlugin()
{
	return new MyPlugin;
}

extern "C" UNIGINE_EXPORT void ReleasePlugin(void *plugin)
{
	delete reinterpret_cast<MyPlugin *>(plugin);
}

MyPlugin::MyPlugin()
{
}

MyPlugin::~MyPlugin()
{
}

int MyPlugin::getCompilationFlags() const
{
	// Return the UNIGINE compilation flags for which the plugin is built (please, see UNIGINE_COMPILATION_FLAG_).
	return UNIGINE_COMPILATION_FLAGS;
}

const char *MyPlugin::get_name()
{
	// Return the plugin name.

	// This is the name that will be used to refer to your plugin.
	// For example, see Engine::findPlugin(const char *name).

	return "MyPlugin";
}

void *MyPlugin::get_data()
{
	// Return the plugin data.

	// Usually this is expected to be a pointer to the
	// public interface of this plugin, if there is any.
	// See Engine::getPlugin(const char *name).

	return nullptr;
}

int MyPlugin::get_order()
{
	// Return the plugin execution order.
	return 0;
}

int MyPlugin::init()
{
	// The engine calls this function on plugin initialization.
	// Should return 1 on success, or 0 if an error occurred.

	// Put your plugin initialization logic here.

	return 1;
}

int MyPlugin::shutdown()
{
	// The engine calls this function on plugin shutdown.
	// Should return 1 on success, or 0 if an error occurred.

	// Put your plugin deinitialization logic here.

	return 1;
}

void MyPlugin::update()
{
	// The engine calls this function before updating each render frame.

	// Put your update logic here.
}

void MyPlugin::postUpdate()
{
	// The engine calls this function after updating each render frame.

	// Put your post-update logic here.
}

void MyPlugin::render(const Unigine::EngineWindowViewportPtr &window)
{
	// The engine calls this function before rendering each render frame.

	UNIGINE_UNUSED(window);
}

void MyPlugin::gui(const Unigine::EngineWindowViewportPtr &window)
{
	// The engine calls this function before each GUI render frame.

	UNIGINE_UNUSED(window);
}

void MyPlugin::updatePhysics()
{
	// The engine calls this function before updating each physics frame.

	// Put your physics update logic here.
}

void MyPlugin::swap()
{
	// The engine calls this function before swapping each render frame.
}

int MyPlugin::loadWorld(const Unigine::XmlPtr &xml)
{
	// The engine calls this function on world loading.
	// Should return 1 on success, or 0 if an error occurred.

	// You can load your plugin data here from the given xml.

	UNIGINE_UNUSED(xml);

	return 1;
}

int MyPlugin::saveWorld(const Unigine::XmlPtr &xml)
{
	// The engine calls this function on world saving.
	// Should return 1 on success, or 0 if an error occurred.

	// You can save your plugin data here to the given xml.

	UNIGINE_UNUSED(xml);

	return 1;
}

```

</details>


> **Notice:** *CreatePlugin()* and *ReleasePlugin()* methods are declared as *extern "C"* to be compiled as regular C functions. This is required to prevent mangling of the function names and thus ensure that the naming decoration scheme matches between the UNIGINE executable and the created dynamic-link library. Otherwise, binary code generated by two different C++ compilers may be incompatible, because there is no recognized C++ application binary interface.


### Basic Plugin Example


If you are going to interfere the engine initialization, main loop or shutdown, implement classes inherited from the *[WorldLogic or SystemLogic](../../code/fundamentals/execution_sequence/app_logic_system.md)* classes. You can implement your own logic (namely, callback functions) in these classes and then add it to the engine to be executed in its *init(), update(), shutdown()*, etc. via the plugin interface.


> **Notice:** It is required to include `UnigineLogic.h` for accessing the *World/SystemLogic* classes methods.


In addition to that, you can define **plugin methods** and **free (standalone) functions** that are called from your application code. For simple cases, these methods and functions can be implemented directly in the header file (for example, as inline functions), so they are available both to the plugin and to the user code without extra setup.


As an example let's implement the following simple plugin with its System and World logic components, as well as plugin methods and free functions to be called from your UNIGINE application (we'll see how to use them a bit later):


**Simple Plugin Example:**


<details>
<summary>MyPlugin.h | Close</summary>

```cpp
#pragma once

#include <UniginePlugin.h>
#include <UnigineLogic.h>

using namespace Unigine;

// System logic:
class MySystemLogic : public SystemLogic {
public:
	// Called on system initialization.
	virtual int init() override;

	// Called on system shutdown.
	virtual int shutdown() override;
};

// World logic:
class MyWorldLogic : public WorldLogic {
public:
	// Called after the world is initialized.
	virtual int init() override;

	// Called before the world is destroyed or unloaded.
	virtual int shutdown() override;
};

// Plugin implementation:
// This class is the actual plugin loaded by the engine.
class MyPlugin : public Plugin {
public:
	MyPlugin();
	virtual ~MyPlugin();

	// Example of a member method (plugin method).
	void printPluginMessage()
	{
		Log::message("printPluginMessage(): called for '%s'\n", get_name());
	};

	// Plugin interface methods:
	virtual int getCompilationFlags() const override;
	virtual const char* get_name() override;
	virtual void* get_data() override;
	virtual int get_order() override;

	virtual int init() override;
	virtual int shutdown() override;

private:
	// Instances of system and world logic managed by the plugin.
	MySystemLogic system_logic;
	MyWorldLogic  world_logic;
};

// Free (standalone) function example:
// This function is not a member of any class.
// It can be used as a simple helper and does not have access to 'this'.
void printGlobalMessage()
{
	Log::message("printGlobalMessage(): free function called\n");
}

```

</details>


<details>
<summary>MyPlugin.cpp | Close</summary>

```cpp
#include "MyPlugin.h"

#include <UnigineEngine.h>
#include <UnigineLog.h>

using namespace Unigine;

// -------------------------
// MySystemLogic implementation
// -------------------------

int MySystemLogic::init() {
	// Called when system logic is initialized.
	Log::message("MySystemLogic::init(): called\n");
	return 1;
}

int MySystemLogic::shutdown() {
	// Called when system logic is shutting down.
	Log::message("MySystemLogic::shutdown(): called\n");
	return 1;
}

// -------------------------
// MyWorldLogic implementation
// -------------------------

int MyWorldLogic::init() {
	// Called when the world logic is initialized.
	Log::message("MyWorldLogic::init(): called\n");
	return 1;
}

int MyWorldLogic::shutdown() {
	// Called when the world logic is shutting down.
	Log::message("MyWorldLogic::shutdown(): called\n");
	return 1;
}

// -------------------------
// Plugin exports
// -------------------------

extern "C" UNIGINE_EXPORT void* CreatePlugin() {
	// Called by the engine to create the plugin instance.
	return new MyPlugin;
}

extern "C" UNIGINE_EXPORT void ReleasePlugin(void* plugin) {
	// Called by the engine to destroy the plugin instance.
	delete reinterpret_cast<MyPlugin*>(plugin);
}

// -------------------------
// MyPlugin implementation
// -------------------------

MyPlugin::MyPlugin() {
	// Constructor: plugin object is created here, but not yet initialized.
}

MyPlugin::~MyPlugin() {
	// Destructor: called when the plugin instance is destroyed.
}

int MyPlugin::getCompilationFlags() const {
	// Return the UNIGINE compilation flags for which the plugin is built.
	return UNIGINE_COMPILATION_FLAGS;
}

const char* MyPlugin::get_name() {
	// This name is used by the engine to refer to the plugin.
	return "MyPlugin";
}

void* MyPlugin::get_data() {
	// Return plugin data.
	// Usually this is a pointer to the public interface of the plugin.
	// In this basic example we simply return 'this'.
	return this;
}

int MyPlugin::get_order() {
	// Plugin execution order.
	// Lower values are initialized earlier.
	return 0;
}

int MyPlugin::init() {
	// Called when the plugin is initialized.
	// Here we attach our system and world logic to the engine.

	Engine* engine = Engine::get();

	engine->addSystemLogic(&system_logic);
	engine->addWorldLogic(&world_logic);

	return 1;
}

int MyPlugin::shutdown() {
	// Called when the plugin is shutting down.
	// Here we detach our system and world logic from the engine.

	Engine* engine = Engine::get();

	engine->removeSystemLogic(&system_logic);
	engine->removeWorldLogic(&world_logic);

	return 1;
}

```

</details>


If you want to hide the implementation inside the plugin and expose only a clean public API, the design becomes more advanced. In this case, you typically use a separate interface (as shown in the **[NodeViewerPlugin](#engine_plugin_sample)** sample below), so the Engine and user code only see the interface, while the actual implementation remains inside the plugin.


## 3) Build the Plugin


After the plugin code has been implemented, you can proceed to build it in order to make it available for use in UNIGINE applications.


> **Notice:** - *Release* version of the Engine requires *Release* binaries of plugins and does not load *Debug* ones! For each version of the application that will use your plugin, make sure to build the corresponding plugin version.
> - **Plugins are not guaranteed to be binary-compatible across different SDK versions**. For example, a plugin built with SDK 2.20 may not work correctly with SDK 2.21, and vice versa. To avoid compatibility issues, it is recommended to always rebuild your plugin using the exact SDK version targeted by your application.


### Using MS Visual Studio


In case you're using *MS Visual Studio*, there is a `.vcxproj` file in your plugin folder. Specify the solution configuration: *Release, Release-Double, Debug* or *Debug-Double* configuration and choose *Build -> Build Solution* in the menu or press **Ctrl + Shift + B**.

  ![](../rebuild/configuration_p.png)
*1) Select the configuration that matches your project before building the plugin.*

  ![](../rebuild/build_p.png)
*2) Build the plugin project usingBuild -> Build SolutionorCtrl + Shift + B.*


Created plugin library will be automatically placed inside your `bin/plugins` folder.


### Using CMake


If you're using *CMake*, then `CMakeLists.txt` is automatically added to the corressponding folder of your plugin inside your UNIGINE project's `source` folder. To build the plugin, run the following commands:


```text
cmake -B build -S .
cmake --build build

```


> **Notice:** If you add additional `*.cpp` or `*.h` files to the project, make sure to update the `CMakeLists.txt` accordingly, otherwise these files will not be compiled and linked into the plugin.


## 4) Load the Plugin Library


At this stage, the plugin is already compiled and can be used. To make it active within the project, it needs to be loaded by the Engine.


For your convenience, the **Template Engine Plugin will be automatically included in the project** in which it was created, using *-extern_plugin*, so no additional configuration is required!


However, when you work with existing (prebuilt) plugins, you need to explicitly include them in the project. There are several ways to specify which plugins should be included:


1. **Via Command-Line On Startup** The **preffered way** is to pass the plugin as a command-line argument using `-extern_plugin`: ```text -extern_plugin VendorNamePluginName ``` > **Notice:** The plugin name should be specified **without prefixes or postfixes**. For example, to load `VendorNamePluginName_plugin_x64d.dll`, use `VendorNamePluginName` in the command. If the path to the library is relative, it is resolved relative to the binary executable; absolute paths are also supported.
2. **Via Configuration File** You can also specify paths to plugins and plugin names that will be loaded at startup directly in the configuration file (`data/configs/default.boot`) > **Warning:** Settings defined in the configuration file **will be overridden** if the corresponding command-line arguments are used: > > > - *plugin_paths* will be overridden by *-plugin_path* > - *extern_plugins* will be overridden by *-extern_plugin*

  - ***plugin_paths*** - a list of [paths to directories](../../code/command_line.md#plugin_path) that contain plugins libraries. ```xml <plugin_paths> <path>plugins/</path> <path>../extra/plugins/</path> </plugin_paths> ```
  - ***extern_plugins*** - a list of [plugin libraries](../../code/command_line.md#extern_plugin) to be loaded. ```xml <extern_plugins> <plugin>UnigineSteam</plugin> <plugin>UnigineUltraleap</plugin> <plugin>UnigineDataBridge</plugin> </extern_plugins> ```


### Load Plugins On Demand


Plugins can also be loaded directly at runtime, which allows the application to activate only the required functionality when it is needed.


You can even modify a plugin without shutting down the Engine - simply unload it, rebuild it, and load it back again.


- **Via the Console** Plugins can be loaded, unloaded, and reloaded using console commands: ```text Unigine~# plugin_load UnigineNodeViewerPlugin Loading "D:/UNIGINE/UNIGINE_Projects/PluginProject/bin/plugins/Unigine/NodeViewerPlugin/UnigineNodeViewerPlugin_plugin_double_x64d.dll"... EnginePlugins: "UnigineNodeViewerPlugin" plugin is initialized ```

  - [*plugin_load*](../../code/console/index.md#plugin_load)
  - [*plugin_unload*](../../code/console/index.md#plugin_unload)
  - [*plugin_reload*](../../code/console/index.md#plugin_reload)
- **From World Logic or Script**

  - Add and use the plugin in the **World Script** via *[engine.addPlugin()](../../api/library/engine/class.engine_cpp.md#addPlugin_const_char_ptr_bool)*.
  - The same can be done in the project's **World Logic** via *[Engine::addPlugin()](../../api/library/engine/class.engine_cpp.md#addPlugin_const_char_ptr_bool)*.
- **From System Logic or Script**

  - Add the plugin in the **System Script** or **System Logic**, and use it later in the **World Script** or **World Logic**. > **Notice:** You cannot initialize the plugin and call its functions from the same **System Script** simultaneously. Alternatively, load the plugin [via the command-line argument](#command_line_plugin), and then use it in the System Script or System Logic.


## 5) Call Plugin Library Functions


To access classes and functions of the library from the C++ side of the application, you should do the following:


1. Include a plugin's header file in your C++ code: ```cpp // The plugin's header is placed according to the plugin naming conventions #include "plugins/Local/MyPlugin/MyPlugin.h" ``` > **Notice:** If you implemented the plugin in the `.cpp` file only, include it instead of creating a separate header file.
2. Get the plugin instance in the project's World Logic. Access to plugin depends on its implementation. In our [basic example](#basic_plugin_example) (**MyPlugin**), all logic is implemented directly in the plugin class inherited from *[Unigine::Plugin](../../api/library/common/class.plugin_cpp.md)* and API exposed via header file. <details> <summary>Show | Close</summary> ```cpp int AppWorldLogic::update() { if (Unigine::Input::isKeyDown(Unigine::Input::KEY_F8)) { // Plugins support hot reload - they can be loaded or reloaded at runtime. // Therefore, it is recommended to perform extra checks before calling any // plugin methods to avoid errors when the plugin is not available // Here, the Engine will search for loaded plugin by calling get_name() methods int id = Unigine::Engine::get()->findPlugin("MyPlugin"); if (id != -1) { // Free function defined inline in the plugin header printGlobalMessage(); // Direct access to the plugin instance Unigine::Plugin* plugin = Unigine::Engine::get()->getPluginInterface(id); if (plugin) { // Cast to the plugin class and call its member method MyPlugin* my_plugin = static_cast<MyPlugin*>(plugin); my_plugin->printPluginMessage(); } } } return 1; } ``` </details>
3. [Compile](../../code/cpp/application.md#logic) and run the C++ application.


![](basic_plugin_output.png)

*The plugin was loaded successfully, both logics were initialized, and both the free function and the plugin method were called correctly.*


## Engine Plugin Sample


When you create a plugin using the **Engine Plugin Template**, the project configuration also adds a sample plugin called ***NodeViewerPlugin***, as a reference implementation. You can use it as a starting point for developing your own plugin, or remove it if it is not required.


***NodeViewerPlugin*** lets you inspect the in-world node hierarchy, select nodes with the right mouse button, and move/rotate/scale them using manipulators (gizmos). The plugin window can be toggled on or off with the *F10* key.


![](engine_plugin_sample.png)

*Node Viewer Window*


Let's quickly review the sources:


The plugin implementation is located in the `NodeViewerPluginImpl` class. It inherits from both *[Unigine::Plugin](../../api/library/common/class.plugin_cpp.md)* and `NodeViewerPlugin`.


- The `NodeViewerPlugin` interface is the part that user code can access. It provides simple methods to work with the plugin, for example, checking if it is initialized or showing and hiding the window.
- The ***[Unigine::Plugin](../../api/library/common/class.plugin_cpp.md)*** interface is used by the Engine itself. Through this interface, the Engine registers the plugin, runs its initialization, and calls its *update()* method every frame.


In this design, all public API is exposed through the `NodeViewerPlugin` interface, while its actual implementation is hidden inside `NodeViewerPluginImpl`.


### Implementing Singleton Pattern


In most cases, plugins are designed as **singletons**. This means there is **only one instance** of the plugin in the Engine, and it can be accessed from anywhere in the code. Instead of creating new objects, the user simply gets the existing instance and uses its public methods.


A common approach is to provide a static *get()* method that returns a pointer to the current plugin instance:


<details>
<summary>Singleton Plugin | Close</summary>

```cpp
UNIGINE_INLINE static NodeViewerPlugin *get()
{
	static NodeViewerPlugin *instance = nullptr;
	static Unigine::EventConnection connection;
	static Unigine::Mutex m;

	if (instance == nullptr)
	{
		Unigine::ScopedLock l(m);

		if (instance == nullptr)
		{
			if (!connection.isValid())
			{
				Unigine::Engine::get()->getEventPluginRemoved().connect(
					connection,
					[](const char *name) {
						if (Unigine::String::equal(name, "NodeViewerPlugin"))
						{
							connection.disconnect();
							instance = nullptr;
						}
					}
				);
			}

			instance = Unigine::Engine::get()->getPlugin<NodeViewerPlugin>("NodeViewerPlugin");
		}
	}
	return instance;
}

```

</details>


By default, the plugin provides window toggling using the **F10** key. To access the plugin instance and call its methods directly (in this case to show or hide the window manually), you typically do the following:


<details>
<summary>Accessing Plugin Instance | Close</summary>

```cpp
#include "AppWorldLogic.h"
#include "plugins/Unigine/NodeViewerPlugin/NodeViewerPlugin.h"

AppWorldLogic::AppWorldLogic()
{}

AppWorldLogic::~AppWorldLogic()
{}

int AppWorldLogic::init()
{
	// Load the plugin by its name at WorldLogic initialization.
	// You can also use:
	// "-extern_plugin" start-up argument or
	// "plugin_load" console command at runmtime

	// When loading plugin, you have to specify its full name:
	// Vendor + PluginName
	Unigine::Engine::get()->addPlugin("UnigineNodeViewerPlugin");
	return 1;
}

int AppWorldLogic::update()
{
	// Hide the plugin window on F8.
	if (Unigine::Input::isKeyDown(Unigine::Input::KEY_F8))
	{
		// Plugins support hot reload - they can be loaded or reloaded at runtime.

		// Therefore, it is recommended to perform extra checks before calling any
		// plugin methods to avoid errors when the plugin is not available

		// Here, the Engine will search for loaded plugin by calling get_name() methods
		// See NodeViewerPlugin sources to find implementation
		bool is_plugin_loaded = Unigine::Engine::get()->findPlugin("NodeViewerPlugin") != -1;

		if (is_plugin_loaded && NodeViewerPlugin::get()->isInitialized())
		{
			NodeViewerPlugin::get()->setVisible(false);
		}
	}

	// Show the plugin window on F9.
	if (Unigine::Input::isKeyDown(Unigine::Input::KEY_F9))
	{
		// The same logics applies here
		bool is_plugin_loaded = Unigine::Engine::get()->findPlugin("NodeViewerPlugin") != -1;

		if (is_plugin_loaded && NodeViewerPlugin::get()->isInitialized())
		{
			NodeViewerPlugin::get()->setVisible(true);
		}
	}

	return 1;
}

```

</details>


## Accessing a C++ Plugin from C# Project


Since a plugin is built as a native library, it can be easily added and loaded to a C# project [the same way as in C++ project](#step_4). However, if the plugin provides a public API that must be called from C#, you need an additional layer to bridge native C++ code and managed C# code.


For this purpose, you can use the **C# API Generator** Add-On, that automatically generates both the native wrappers (C++) and the managed API layer (C#) for your plugins:


- **[C# API Generator](https://store.unigine.com/en/add-on/1f0734b4-b7f2-6c80-b381-950ea7ab9eab/description)** Add-On available in the *UNIGINE Add-On Store*
