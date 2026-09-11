# Creating C# Application


A Unigine-based application can be implemented by means of C# only, without using UnigineScript. This article describes how to create a new Unigine-based C# application on Windows platform.


Implementation by using the C# language is very similar to C++. Read the [Creating C++ Application](../../code/cpp/application.md) article to get basic principles.


### See Also


- Samples located in the `<UnigineSDK>/source/csharp/samples/Api` and `<UnigineSDK>/source/csharp/samples/App` folders
- The article on [Setting Up Development Environment](../../code/environment/index.md) to learn more on how to prepare the development environment


## Creating Empty C# Application


It is very easy to start your own C# project by using UNIGINE SDK Browser:


1. Open the UNIGINE SDK Browser.
2. Go to the *[Templates](../../sdk/index.md#templates)* tab and click *Create Project* button on the *C# Empty* template card. ![](../../sdk/projects/create_project_cs.png)
3. Specify the following parameters: ![](../../start/quick_start/setup_project/create_new_cs.png) > **Notice:** Read more about these parameters in [this article](../../sdk/projects/index_cpp.md).

  - **Project name** � specify the name of your project.
  - **Location** � specify the path to your project folder.
  - **SDK** � choose the Unigine SDK.
  - **Precision** � specify the precision. In this example we will use [double precision](../../code/double_precision/index.md).
4. Click the *Create New Project* button. The project will appear in the *My Projects* tab list. ![](project_created.png)


You can [run](../../sdk/projects/index_cpp.md#run) your project by clicking the *Run* button.


> **Notice:** By default, in the [world script](../../code/fundamentals/execution_sequence/app_logic_system.md#world_script) file a WorldLight and a PlayerSpectator are created. You can leave functions of the world script empty, and create your own lights and players by using C#.


## Implementing C# Logic


To implement C# logic, use the following approaches either separately, or in combination:


- [C# Component System](../../principles/component_system/component_system_cs/index.md), which is enabled by default and integrated into the Editor: this way it is easier to implement your application logic in components and assign them to any node to be executed. A component can be reused for as many nodes as you need without changing anything in it. If a node is renamed or disabled, the component assigned to it does not require any changes due to that. When you change anything in your component's logic, the changes are applied to all nodes having this component assigned. The Editor also provides for running an instance of the application to check the result immediately.
- [SystemLogic](../../code/fundamentals/execution_sequence/app_logic_system.md#systemlogic) and [WorldLogic](../../code/fundamentals/execution_sequence/app_logic_system.md#worldlogic) global classes that are available in the **/source** folder.


In this section we will add logic to the empty C# application project and rotate the material ball that is created by default.


1. In UNIGINE SDK Browser, choose your C# project created with the *C# (.NET)* option selected as API+IDE, and click the *Open Editor* button. ![](../../sdk/projects/run_editor.png) UnigineEditor will open.
2. In UnigineEditor, create a new C# component via Asset Browser. ![](../../principles/component_system/component_system_cs/create_component.gif) Let's name it `rotator`.
3. By double-clicking a created asset `rotator.cs`, it will open in the default IDE. Add the following code to this file. ```csharp public partial class rotator : Component { public float angle = 30.0f; void Update() { // write here code to be called before updating each render frame node.Rotate(0, 0, angle * Game.IFps); } } ``` All saved changes of the component source code make the component update with no compilation required when the Editor window gets focus.
4. [Add this component](../../principles/component_system/component_system_cs/index.md#apply) to the *material ball*.
5. Run an instance of the application by clicking the *Play* button on the toolbar. ![](usage/using_cs_component_system/run.png)


The component can be assigned to any node or nodes without changing anything in it.
