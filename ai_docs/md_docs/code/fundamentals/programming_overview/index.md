# Programming Overview


This article describes ways of creating projects in Unigine.


The main purpose of the article is to provide insight into setting up the development environment and give the overview of programming. It contains links to other articles that help you to prepare the development environment, choose the language to programming and so on.


## Languages


To create your own project with Unigine, you can use the following programming languages:


- [UnigineScript](../../../code/uniginescript/index.md)
- C++, by using [C++ API](../../../api/index.md)
- C#, by using [C# API](../../../code/csharp/index.md)


UnigineScript can be easily extended through the Unigine API. The Unigine engine enables exporting the C++ and C# code and vice versa. You can write some functionality by using the C++ or C# language, and export it to the UnigineScript. See usage examples articles of *[C++ API](../../../code/cpp/usage/index.md)* and *[C# API](../../../code/csharp/usage/index.md)* to know more.


## Platforms


Unigine supports the following platforms:


- Windows (10/11)
- Linux (kernel 4.19+)


A 64-bit system is required to develop applications using UNIGINE 2 SDK. The engine fully and efficiently uses multi-core CPU architecture.


With Unigine you can build applications for these platforms with a single codebase.


Read more about the [Hardware Requirements](../../../start/requirements.md).


## Development Environments


You can use any of these PC platforms to write your Unigine-powered project:


- Windows
- Linux


In addition to UNIGINE SDK, each platform requires specific software that you need to install in order to start coding. You can find requirements for each platform here:


- [development for Windows](../../../code/environment/windows.md)
- [development for Linux](../../../code/environment/linux.md)


## Execution Sequence


Unigine's [Application Logic System](../../../code/fundamentals/execution_sequence/app_logic_system.md) has three main concepts of logic:


- **System logic** - the logic of the application. You can implement your logic that will be performed during application life cycle. Your custom logic can be put in the [system script](../../../code/fundamentals/execution_sequence/app_logic_system.md#system_logic) file (*by using UnigineScript API only*), or you can inherit [SystemLogic class](../../../api/library/common/logic/class.systemlogic_cpp.md) and implement your logic (*C++ and C# APIs*). UnigineScript `unigine.usc` system script file is created automatically in the your project's folder. When you create a new *C++ / C# project*, it has already inherited system logic class with implemented methods to put your logic code inside.
- **World logic** - the logic of the world - here you should put the logic of the virtual [scene](../../../start/index.md#world). The logic takes effect when the world is loaded. You can put your logic inside the [world script](../../../code/fundamentals/execution_sequence/app_logic_system.md#world_logic) file (*by using UnigineScript API only*), or you can inherit [WorldLogic class](../../../api/library/common/logic/class.worldlogic_cpp.md) and implement your logic (*C++ and C# APIs*). The world script `*.usc` file is automatically created with the new world and has the name of your project. When you create a new *C++ / C# project*, it has already inherited world logic class with implemented methods to put your logic code inside.
- **Editor logic** - this component is to be used in case you need to implement your own Editor. It has more implemented methods providing you with clear understanding of the current Engine events (a node has been created, a property has been deleted, a material has been changed, etc.). You can inherit [EditorLogic class](../../../api/library/common/logic/class.editorlogic_cpp.md) and implement your logic in C++ or C#. Default UnigineScript logic for the Editor is loaded from the `editor2/editor.usc` file stored inside `editor2.ung`. You can override this UnigineScript logic file by creating a folder named `editor2` in your `data` folder and putting there the `editor.usc` file with the following code (you can modify this script, but do not remove existing *include* lines as they are required for Editor operation): <details> <summary>editor.usc | Close</summary> *editor.usc* ```text #include <editor2/editor_tracker.h> #include <editor2/editor_video_grabber.h> int init() { return 1; } int update() { return 1; } int shutdown() { return 1; } ``` </details>


> **Notice:** In case of inheriting `*Logic` classes (*C++ / C#*), implemented methods will be called right after corresponding scripts' methods.


The UNIGINE engine internal code and the application logic are executed in the pre-defined order:


1. [**Initialization**](../../../code/fundamentals/execution_sequence/init.md). During this stage, the required resources are prepared and initialized. As soon as these resources are ready for use, the engine enters the main loop.
2. [**Main loop**](../../../code/fundamentals/execution_sequence/main_loop.md). When UNIGINE enters the main loop, all its actions can be divided into three stages, which are performed one by one in a cycle: This cycle is repeated every frame while the application is running.

  1. [Update](../../../code/fundamentals/execution_sequence/main_loop.md#update) stage containing all logic of your application that is performed every frame
  2. [Rendering](../../../code/fundamentals/execution_sequence/main_loop.md#postUpdate) stage containing all rendering-related operations, physics simulation calculations, and pathfinding
  3. [Swap](../../../code/fundamentals/execution_sequence/main_loop.md#swap) stage containing all synchronization operations performed in order to switch between the buffers
3. [**Shutdown**](../../../code/fundamentals/execution_sequence/shutdown.md). When UNIGINE stops execution of the application, it performs operations related to the application shutdown and resource cleanup.


Read [this article](../../../code/fundamentals/execution_sequence/code_update.md) to know where to put your logic code.


Also, read the [Execution Sequence](../../../code/fundamentals/execution_sequence/index.md) and [Logic System](../../../code/fundamentals/execution_sequence/app_logic_system.md) articles to know the detailed workflow of the Unigine engine.


## Applying Logic to Objects


For an object to be conveniently integrated into application logic, it is required to specify the set of user-defined parameters and the way the object will behave and interact with other objects and the scene environment.


Depending on the programming language selected in UNIGINE, you also define the way you are going to apply the logic to objects:


- By assigning C# [**components**](../../../api/library/common/logic/component_system/cs/class.component.md), which are the part of [**C# Component System**](../../../principles/component_system/component_system_cs/index.md) (.NET) enabled by default and integrated into the UnigineEditor. It is the easiest way to implement your application logic: all parameters and logic are added to components that can be assigned to any node to be executed.
- By assigning [**properties**](../../../principles/world_structure/index.md#properties) (for C++). Properties can be used on their own for [**accessing nodes and files**](../../../code/fundamentals/file_access/index.md) or as an integral part of [**C++ Component System**](../../../principles/component_system/component_system_cpp/index.md) to extend the functionality of nodes. While the property represents a tag for logic and provides a set of user-defined parameters, the logic **component** integrates a node, a C++ class, containing logic implementation, and a property.


To learn more on the usage of Component Systems, see the following usage example articles:


- [**Using C# Component System**](../../../code/csharp/usage/using_cs_component_system/index.md)
- [**Using C++ Component System**](../../../code/usage/using_component_system/index.md)


## Usage Examples


There are three sections with usage example samples:


- [UnigineScript Sample](../../../code/uniginescript/application.md)
- [C++ Sample](../../../code/cpp/application.md)
- [C# Sample](../../../code/csharp/application.md)


The programming code is the same for all supported platforms, the difference is in compiling.


For all of these samples we create new projects by using the [SDK Browser](../../../sdk/projects/index_cpp.md#creation). Each world contains a basic set of content, including [World Light](../../../objects/lights/world/index.md) source, a plane mesh, and a few objects.
