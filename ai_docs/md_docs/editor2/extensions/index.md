# Extending Editor Functionality


> **Warning:** This feature is an experimental one and is not recommended for production use.


UNIGINE enables you to extend the core UnigineEditor functionality, e.g., add new menus, windows, tool bar commands, sub-modes, define how properties are displayed, and even create your custom Editor. This is made possible by UnigineEditor's [Plugin System](#plugin_system) via adding [custom user plugins](../../editor2/extensions/custom_plugin.md).


UnigineEditor is an application written entirely in C++ relying a lot on the Qt6 framework infrastructure. So, in order to extend its functionality not only C++ programming skills are required, but you should also be familiar with the Qt6 framework, CMake build system.


> **Notice:** *Qt Framework* version **6.5.3** is required to develop plugins for UnigineEditor. It is not included in UNIGINE SDK, so you'll have to download and install it.


### See Also


- [Creating Your First Editor Plugin](../../editor2/extensions/custom_plugin.md) article to learn how to create a custom Editor plugin.
- *[Editor API Reference](/api/editor/index.md)* for more information on all available classes.


## Editor Plugin System


**Plugins** are collections of code and data that developers can easily enable or disable within UnigineEditor on a per-project basis. Each plugin is compiled into a dynamic library that is shipped separately, it is detected and loaded at run time by UnigineEditor.


Basically the structure of the Plugin System is as follows:


![Plugin System](plugin_system.png)

*Plugin System*


Here is a brief description of the main components:


- ***QPluginLoader*** is responsible for plugin loading and providing meta data.
- *[**Editor::PluginInfo**](/api/editor/class_unigine_editor_1_1_plugin_info.md)* � plugin [meta data](#plugin_meta) parsing and storage, interaction with plugin interface, it also contains the current plugin state and information on a possible plugin initialization error.
- *[**Editor::PluginManager**](/api/editor/class_unigine_editor_1_1_plugin_manager.md)* � a manager class responsible for locating plugins, building plugin loading queue, as well as loading and removing plugins.
- *[**Editor::Plugin**](/api/editor/class_unigine_editor_1_1_plugin.md)* � the basic class all Editor plugins inherit from, it has the following declaration: <details> <summary>Editor::Plugin Class Declaration | Close</summary> ***Editor::Plugin* Class Declaration** ```cpp namespace Editor { class EDITOR_API Plugin { public: Plugin(); virtual ~Plugin(); // Plugin's life cycle. virtual bool init()     = 0; virtual void shutdown() = 0; }; } // namespace Editor // Associates the given Identifier (a string literal) to the interface class called Editor::Plugin. Q_DECLARE_INTERFACE(Editor::Plugin, "com.unigine.EditorPlugin") ``` </details> It has two abstract methods defining the plugin's [life cycle](#plugin_lifecycle), you should override them for your custom plugin: > **Notice:** The `Q_DECLARE_INTERFACE` macro adds the interface to Qt's metasystem.

  - ***init()*** � plugin initialization (returns initialization result)
  - ***shutdown()*** � plugin shutdown


## Locating Plugins


Plugins having their libraries located in the directory given below, are automatically loaded and added to the list of available UnigineEditor plugins, no specific code is required:


- `%project%/bin/plugins/` � for *Debug* and *Release* builds and any SDK build.


> **Notice:** All UNIGINE plugins, both for the Engine and UnigineEditor, should meet [requirements to their location (paths)](../../code/cpp/plugin.md#path_to_plugin_files) and comply with [naming convention](../../code/cpp/plugin.md#naming).


To see the list of all currently loaded plugins in UnigineEditor, choose *Windows -> Editor Plugin Manager*.


![Plugins List](pluginslistview.png)


You can view any plugin's description by selecting it in the list and clicking **Details**.


![Plugin Details](plugindetailview.png)


## Plugin Meta Data


Each plugin must have additional information required by the plugin manager to find your plugin and resolve its [dependencies](#plugin_dependencies) before actually loading your plugin's library file.  This information is stored in a meta file in JSON format (`myplugin.json` file automatically generated when adding an Editor plugin template to your project) and can be obtained at run time from an instance of the *[**Editor::PluginInfo**](/api/editor/class_unigine_editor_1_1_plugin_info.md)* class. This meta file may look as follows:


```java
{
    "Name" : "MyPlugin",
    "Vendor" : "Unigine",
    "Description" : "The plugin's description text." ,
    "Version" : "@PLUGIN_VERSION@",
    "CompatVersion" : "@PLUGIN_COMPAT_VERSION@"
    "Dependencies" : [
      {
        "Name": "RequiredPlugin",
        "Type": "required",
        "Version" : "2.9.0.0"
      },
      {
        "Name": "OptionalPlugin",
        "Type": "optional",
        "Version" : "2.8.0"
      }

    ]
}

```


Here is a brief overview of the basic elements:


- **Name** � plugin name displayed in UnigineEditor's Plugins List, and used as reference when describing other plugins dependencies.
- **Vendor, Description** � additional information (optional).
- **Version** � current plugin version.
- **CompatVersion** � last binary compatible plugin version, defines which version of this plugin the current version is binary backward compatible with and is used to resolve dependencies on this plugin.
- **[Dependencies](#plugin_dependencies)** � list of objects describing dependencies on other plugins.
- **Name** � name of the plugin, on which this plugin relies.
- **Type** � dependency type, can be either *required* or *optional*.
- **Version** � version with which the plugin must be compatible to fill the dependency, in the form x.y.z. Can be empty if the version does not matter.


Actually, the author creates a `.json.in` file, which is then used by CMake to generate the actual plugin `.json` meta data file, replacing variables like `EDITOR_VERSION` with their actual values.


### Plugin Dependencies


A plugin can rely on other plugins. Such dependencies are specified in the plugin meta data, to ensure that these other plugins are loaded before this one.


Dependencies are declared with the key *Dependency* that contains an array of JSON objects with required keys *Name* and *Version*, and the optional key *Type*.


The following formulas illustrate how the dependency information is matched. In the formulas the name of the required plugin (as defined in *Name* of the dependency object) is denoted as *DependencyName* and the required version of the plugin is denoted as DependencyVersion. A plugin with given *Name, Version*, and *CompatVersion* as defined in the plugin meta data matches the dependency if the following conditions are met:


- Its **Name** matches **DependencyName**.
- **CompatVersion <= DependencyVersion <= Version**


For example, a dependency


```java
{
    "Name" : "SomeOtherPlugin",
    "Version" : "2.4.1"
}

```


would be matched by a plugin with


```java
{
    "Name" : "SomeOtherPlugin",
    "Version" : "3.1.0",
    "CompatVersion" : "2.2.0",
    ...
}

```


since the name matches, and the version **2.4.1** given in the dependency tag lies between **2.2.0** and **3.1.0**.


## Plugin Life Cycle


To be able to write Editor plugins, you must understand the steps that the plugin manager takes when you start or shut down UnigineEditor.


When you **start UnigineEditor**, the plugin manager does the following:


- Looks in its search paths for all dynamic libraries, and reads their meta data. All libraries without meta data and the ones without the *com.unigine.EditorPlugin* IID are ignored. The initial state of all plugins is *INVALID* as this is the first point where loading a plugin can fail in the worst case of malformed meta data.
- Creates an instance of the *[**Editor::PluginInfo**](/api/editor/class_unigine_editor_1_1_plugin_info.md)* class for each plugin. Being a container for the plugin meta data, this class also tracks the current plugin state. You can get the *Editor::PluginInfo* instances via the *[Editor::PluginManager::plugins()](/api/editor/class_unigine_editor_1_1_plugin_manager.md#ae651195c4a93794b290e1ec514a0aefb)* function.
- Sets the plugins to the *READ* state.
- Verifies that the [dependencies](#plugin_dependencies) of each plugin exist and are compatible.
- Sets the plugins to the *RESOLVED* state.
- Sorts all plugins into a list called the "loading queue", where the dependencies of a plugin are positioned after the plugin (but not necessarily directly after it). It ensures that plugins are loaded and initialized in proper order.
- Loads the plugins' libraries, and creates their *[**Editor::Plugin**](/api/editor/class_unigine_editor_1_1_plugin.md)* instances in the order of the loading queue. At this point the plugin constructors are called. Plugins that other plugins depend on are created first.
- Sets the plugins to the *LOADED* state.
- Calls the *init()* functions of all plugins in accordance with the loading queue. In the *init()* function, a plugin should make sure that all exported interfaces are set up and available to other plugins. As each plugin assumes that plugins it depends on have set up their exported interfaces. > **Notice:** The plugin *init()* function is a good place for: > - Creating new objects > - Loading settings > - Adding new menus, and new actions to them > - Connecting to other plugin's signals
- Sets the plugins to the *RUNNING* state.


On **UnigineEditor shutdown** the plugin manager starts its shutdown sequence:


- Calls the *shutdown()* functions of all plugins in the order of the loading queue. Plugins should perform measures for speeding up the actual shutdown here, like disconnecting signals that would otherwise needlessly be called.
- Destroys all plugins by deleting their *Editor::Plugin* instances in reverse order of the loading queue. At this point the plugin destructors are called. Plugins should clean up after themselves by freeing memory and other resources.


## Hot Reload


Editor plugins support hot reloading, which can be useful in cases, when you need to perform actions like:


- Unload a plugin.
- Do something.
- Reload the plugin.


You can **unload** and **Load** your plugin again when necessary via the corresponding button in the **HotReload** column (accessible via the **Editor Plugin Manager** window: *Windows -> Editor Plugin Manager*).


You can also do the same via code:


```cpp
Unigine::Vector<Editor::PluginInfo *> plugin_infos = Editor::PluginManager::plugins();

// choose your `PluginInfo*`:
Editor::PluginInfo *required_plugin_info = ..;

// Unload a plugin:
bool unloaded = Editor::PluginManager::unloadPlugin(required_plugin_info);

// Do something
// ...

// Reload the plugin
bool loaded = Editor::PluginManager::loadPlugin(required_plugin_info);

```
