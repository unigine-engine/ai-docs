# C# Component System


**Component System** enables you to implement your application's logic via a set of building blocks � **components**, and assign these blocks to nodes, giving them additional functionality. By combining these small and simple blocks you can create a very sophisticated logic system.


A logic component integrates a [node](../../../start/index.md#node) and a C# class, containing logic implementation (actions to be performed), defining a set of additional parameters to be used.


![](components.png)

*Components assigned to a node*


Components give you more flexibility in implementing your logic, enabling you to:


- Control which parts of code (implemented as component methods) are to be executed, and which of them are not.
- Control execution order of these parts of code.
- Repeatedly use parts of code, written once, for as many objects as you need, with no modifications required. If you want to change your code, you modify a single source (similar to [*NodeReferences*](../../../objects/nodes/reference/index.md), if we talk about content).
- Combine certain parts of code to be executed for certain nodes. Build a very sophisticated system from numerous small and simple blocks (like you would use a [*NodeReference*](../../../objects/nodes/reference/index.md) to build a large complex structure using many simple nodes).


Before starting coding, you should install [required software](../../../principles/component_system/component_system_cs/index.md#requirements).


### See Also


- [Debugging C# Components](../../../code/csharp/debug_components.md) for more details on debugging the code of your C# components.
- [C# Component Samples](../../../sdk/api_samples/cs/index.md) demo package that demonstrates various ways of using C# components.
- [C# Third Person Platformer](../../../sdk/demos/cs_component_sample.md) demo illustrating performance and flexibility of the logic system using familiar concepts of a simple third-person shooter game.
- [C# Component System API](../../../api/library/common/logic/component_system/cs/index.md) for more details on managing components via C# API.
- [C# Component System Usage Example](../../../code/csharp/usage/using_cs_component_system/index.md) for more details on implementing logic using the C# Component System.


## Requirements


Proper workflow for programming and building .NET-based projects implies a set of requirements:


- **[.NET SDK](https://dotnet.microsoft.com/download/dotnet)** (for both Windows and Linux)
- an IDE or a text editor. Compatibility of different IDEs with the following *.NET* versions is checked: | IDE | Supported .NET version | |---|---| | MS Visual Studio Code | 8.0.x | | MS Visual Studio 2022 | 8.0.x | > **Notice:** *[Visual Studio Code](https://code.visualstudio.com/download)* is the recommended option.


If you work with *MS Visual Studio Code*, install the C# extension for *Visual Studio Code* powered by *OmniSharp* when first opening the component.


In case of any issues with *.NET*, check the Troubleshooting section on [.NET issues](../../../troubleshooting/dotnet_issues.md).


## Creating a Component


Components are created using the [Editor](../../../editor2/index.md). In the [Asset Browser](../../../editor2/assets_workflow/index.md#asset_browser) right-click and choose **Create Code -> C# Component**.


Specify a name for the component in the prompt dialog, after which a C# script asset file with the corresponding name will be created in the current directory of the Asset Browser.


![](create_component.gif)


Double-click the new script asset to edit the component logic in the default IDE.


> **Warning:** Do not create components in the [mount point](../../../principles/filesystem/index_cpp.md#mount_points).


### Renaming Components


Ideally, you name things properly from the start. The name should be clean and reflective of what it does. But, sometimes things do change, and suddenly you realize that your component's name has to be changed. Since 2.11 it's not a big deal. Actually, there are two ways you can do it:


- Renaming your cs-asset in the *Asset Browser*. Component class and associated property will be renamed automatically. The only thing you have to do in this case is to replace all references to your component class in your source code with new ones in your preferred IDE via *Find&Replace*.
- Using refactoring tools of your IDE (e.g., *[Rename symbol](https://code.visualstudio.com/docs/editor/refactoring#_rename-symbol)* in VS Code or *[Edit -> Refactor -> Rename](https://docs.microsoft.com/en-us/visualstudio/ide/reference/rename)* in *Visual Studio*). After renaming simply open UnigineEditor � the corresponding cs-asset and associated property will be renamed automatically keeping all references. Please be aware that in this case the name of the cs-file containing implementation of your component will change and the file will be removed from the project by your IDE as a missing one. So, you'll have to add the renamed file back to the project in the IDE.


## Structure of a Component


Essentially components are C# classes inherited from the base [Component](../../../api/library/common/logic/component_system/cs/class.component.md) class.


The work of the C# Component System is based on **[properties](../../../principles/properties/index.md)**. When you [create](#create) a new component, it is automatically registered in the [Component System](../../../api/library/common/logic/component_system/cs/class.componentsystem.md) and an internal [*runtime*](../../../editor2/assets_workflow/assets_runtimes.md) property is created and associated with the component via a [*GUID*](../../../principles/filesystem/index_cpp.md#guids). The following ***Component*** class attribute is required for proper work of the component.


```csharp
					[Component(PropertyGuid = "2ae011355ed7f110a202912faa000cc22276e539")]
```


> **Warning:** The value of the ***Component*** attribute must not be changed.


C# components are listed in the [Properties](../../../editor2/properties_settings/organizing_properties/index.md) hierarchy, initially they are inherited from the base **C# Components** property.


![](properties.png)


> **Notice:** Generic auto inheritance of components is not supported, you can derive logic implementation from an arbitrary component manually by inheriting its class from the class of the parent component.


### Simple Inheritance


Suppose you have a component implementing certain functionality, and you need a certain number of subcomponents having exactly the same functionality, but different parameter values. This situation is typical when implementing quality presets or configurations of controls. Just inherit a property from the basiс component in the UnigineEditor for each preset and tweak necessary parameter values. After that you can assign these inherited properties to nodes, thus attaching to them the logic of the basic component with parameter values taken from inherited properties. No excessive copy-pasting, no redundant code.


### Logic


Logic of components is implemented via a set of methods, that are called by the corresponding functions of the [world script](../../../code/fundamentals/execution_sequence/code_update.md):


- **Init()** � create and initialize all necessary resources.
- **UpdateAsyncThread()** � specify all logic functions you want to be called every frame independent of the rendering thread. > **Notice:** This method does not have protection locks, so it is not recommended to modify other components inside this method, unless you are absolutely sure, that these components won't be modified or removed elsewhere.
- **UpdateSyncThread()** � specify all parallel logic functions you want to be executed before the Update(). This method can be used to perform some heavy resource-consuming calculations such as pathfinding, generation of procedural textures and so on. > **Notice:** This method should be used to call only the API methods related to the current node: the node itself, its materials and properties.
- **Update()** � specify all logic functions you want to be called every frame.
- **PostUpdate()** � correct behavior according to the updated node states in the same frame.
- **UpdatePhysics()** � simulate physics: perform continuous operations (pushing a car forward depending on current motor's RPM, simulating a wind blowing constantly, perform immediate collision response, etc.).
- **Swap()** � operate with the results of the *updateAsyncThread()* method � all other methods (threads) have already been performed and are idle. After this function, only two actions occur:

  - All objects that are queued for deletion are deleted.
  - Profiler is updated.
- **Shutdown()** � perform cleanup on component shutdown.


> **Notice:** You can set [multiple methods for each stage](../../../api/library/common/logic/component_system/cs/class.component.md#methods) (e.g. multiple *Update()* methods or just a single *Init()*).


> **Warning:** The ***UpdateAsyncThread()** and **UpdateSyncThread()*** methods allow calling only [thread-safe](../../../code/fundamentals/thread_safety/index.md) engine functions.


### Parameters


Components can have parameters that are editable in the *[**Parameters**](../../../editor2/node_parameters/index.md)* window.


![](params.png)


The following entities have auto-generated UI in the Editor based on the data type and the set of attributes:


- ***public*** fields of the component class
- any *private* and *protected* fields of the [supported types](../../../api/library/common/logic/component_system/cs/class.component.md#parameters) with the **[ShowInEditor]** option enabled


```csharp
public int public_field;

private int private_field;

[ShowInEditor]
private float private_editable_field;

[HideInEditor]
public float public_hidden_field;

```


Parameters and their attributes can be declared for editor widgets.


![](attributes.png)


Refer to the *[**Component**](../../../api/library/common/logic/component_system/cs/class.component.md#parameters)* class for more details on supported parameter types and attributes.


## Applying Component Logic to a Node


Logic implementation described in a component is active at run time only if the component is assigned to a node and both node and component are enabled.


There are several ways of applying a component to a node:


- Select a node, click **Add New Property** and type the name of a `*.cs` asset in the **Node Properties** section of the **Node** tab. You can do it by dragging the `*.cs` asset there from the Asset Browser window as well. ![](assign.png) Dragging to the node in the Editor Viewport is also supported. ![](assign_drag.gif)
- Add a component to a node via code by using the *[AddComponent<T>(Node node)](../../../api/library/common/logic/component_system/cs/class.component.md#addComponent_Node_T)* and Node's *[AddComponent<T>()](../../../api/library/nodes/class.node_cpp.md)* functions.


```csharp
NewComponent component = AddComponent<NewComponent>(node);

NewComponent component = node.AddComponent<NewComponent>();

```


The logic of a certain component is active only when the component and the corresponding node are enabled. Thus, you can enable/disable logic of each particular component at run time when necessary.


You can assign several components to a single node. The sequence, in which the logic of components is executed, is determined by the *[order](../../../api/library/common/logic/component_system/cs/class.component.md#methods)* value specified for the corresponding methods (if *order* values are the same or not specified, the sequence is indeterminable).


Components can interact with other components and nodes.


## Running a Project


To run a project, click the **Play** button on the toolbar. This will run an instance of the application in a separate window.


![](run.png)


> **Notice:** You will see a green notification on successful compilation, while the red one signalizes that errors were found. Clicking the red message displays the details in the Console. All C# compilation and run-time errors are displayed in the Console.
> For error messages to be displayed correctly on Windows, the language for non-Unicode programs should be the same as the current system locale.


Presets of custom run options are available in the list. By default, there is a single **Default (Debug)** preset with the default run options. Click the gear icon to configure the current selected preset of custom run options.


In the window that opens the following run options are available:


| **Configuration** | UNIGINE Engine build to be used: - Debug - Release |
|---|---|
| **Video API** | Graphics API to be used for rendering: - DirectX 12 - Vulkan |
| **Resolution** | Screen size |
| **Fullscreen** | Run the instance in one of the following modes: - Disable � application shall run in the windowed mode - Enable � application shall run in the fullscreen mode - Borderless Window � application shall run in the fullwindow mode, when an application window is rendered without decorations |
| **VR Mode** | Enable compatibility with one of supported XR runtimes: - Disable - OpenVR - OpenXR - Varjo |
| **Video Debug** | Enables the [debug context](../../../code/command_line.md#video_debug) of Vulkan or DirectX: - Disable - Messages - Asserts |
| **Run Current World** | Run the current world opened in the Editor regardless of the default world set by logic. |
| **Arguments** | A set of [startup command-line options](../../../code/command_line.md). |


On changing any custom run option and closing the window, the following actions will be performed depending on the preset selected:


- If the **Default (Debug)** preset is selected in the list, a new [`*.launch`](../../../editor2/assets_workflow/asset_types.md#settings) asset file containing the custom run options will be created in the current folder of the Asset Browser. The corresponding preset will be available in the list of presets.
- If another preset is selected, changes will be applied to it.


> **Notice:** You can rename and delete presets of custom run options by renaming and deleting the corresponding `*.launch` assets.


## Debugging Your C# Components


UnigineEditor automatically re-compiles your C# components as you make code modifications, save them and get back to the Editor. You will see a green notification on successful compilation, while the red one signalizes that errors were found. Clicking the red message displays the details in the Console.


![](compilation_messages.png)


You can inspect the source code of your C# components while your application is running regardless of whether the application is launched via the **Play** button right in the UnigineEditor, or built and launched from an IDE.


See the [Debugging C# Components](../../../code/csharp/debug_components.md) article for details.


## Building the Application


To create a debug or release build of your C# application, use the **File -> Create Build** option available in UnigineEditor.


See the [Packing a Final Build for Publishing](../../../editor2/projects/build_project.md) article for details.


## Usage


As an example, you can use components to implement logic of enemies chasing the player in your game: regardless of their size, shape, speed, all of them will check player's position, and try to find a path to move closer to it as fast as they can. The code will be basically the same, it'll just use different parameters (speed, mesh, or sounds maybe), so you can put all these parameters to a component (to be able to change them at any time) and the code to the corresponding component class (e.g. place enemies in the world in the *Init()* and chase the player in the *Update()* method).


Then you should simply assign the component to all enemy objects and set up parameters (define meshes, sounds, etc.). The Component System will do the rest: execute your code at the corresponding stages of the Engine's [main loop](../../../code/fundamentals/execution_sequence/code_update.md) for all enemy objects using their specific parameters. Should you decide to modify your code later, you can do that in a single source � component class.


Integration with the *[**Microprofile**](../../../tools/profiling/microprofile/index_cpp.md)* tool, enables you to monitor overall performance of the Component System, as well as to add profiling information for your custom components.
