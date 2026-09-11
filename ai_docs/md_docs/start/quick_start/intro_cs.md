# Quick Start with Component System (CS)


Let's create a small game project to illustrate typical use cases and best practices for the [C# Component System](../../principles/component_system/component_system_cs/index.md).


![](color_zone/emission.png)


## What You Will Learn


The game that you will create is a simple top-down shooter with physics mechanics. The player controls the character with *WASD* buttons and rotates it to fire bullets using the cursor. The level has some geometric objects (cubes, spheres, etc) that can be thrown to holes by either pushing or shooting. The game has a time limit based on which the game ends. The application also provides a user interface to show the timer and the current amount of objects left to clear. At the end, the game outputs a widget with the reset functionality.


You will acquire some basic [UNIGINE Editor](../../editor2/index.md) skills and knowledge about the UNIGINE engine in general. The basic workflow for game logic implementation with the C# Component System is given below.


[C# Component System](../../principles/component_system/component_system_cs/index.md) enables you to implement your application's logic via a set of building blocks � components, and assign these blocks to objects (*nodes*), giving them additional functionality. A logic component integrates a node and a C# class, containing logic implementation (actions to be performed), defining a set of additional parameters to be used.


In this tutorial you will learn how to:


1. [Set Up the Project](../../start/quick_start/setup_project/index_cs.md)
2. [Create the Controllable Character](../../start/quick_start/character/index_cs.md)
3. [Implement Shooting](../../start/quick_start/shooting/index_cs.md)
4. [Generate Physical Objects](../../start/quick_start/physical_objects/index_cs.md)
5. [Implement Color Zone](../../start/quick_start/color_zone/index_cs.md)
6. [Play Background Music](../../start/quick_start/music/index_cs.md)
7. [Manage Game Rules](../../start/quick_start/game_rules/index_cs.md)
8. [Create the End UI](../../start/quick_start/end_ui/index_cs.md)
9. [Build the Project](../../start/quick_start/build/index_cs.md)


> **Notice:** The following tutorial is written with float coordinates precision for the **Community** edition of the SDK. If you wish to follow it using an SDK version with double coordinates precision, you must change data types in the code snippets accordingly (*vec3* -> *dvec3*, and so on).


## What You Need to Start Coding


To start developing your code, you need to set up an **IDE**.


In most cases, it is enough. However, if you have issues, check the articles in the [Setting Up Development Environment](../../code/environment/index.md) section.


You can use any IDE suitable for C# development. However, note that within this guide we will use [Visual Studio Code](https://code.visualstudio.com/download):

1. Follow the link and choose the required version for downloading.
2. Open the downloaded file and follow the instructions on installation.


If UNIGINE doesn't use your IDE as the default one for editing the code of the C# project, you can set it [manually](../../videotutorials/how_to/how_to_basics/custom_ide.md) via the UNIGINE SDK.


You may also need to install **[.NET SDK](https://dotnet.microsoft.com/en-us/download)**: click *Download .NET SDK*, run the downloaded file and follow the instructions on installation. .NET SDK is required to develop projects using [C# Component System](../../principles/component_system/component_system_cs/index.md). See also [here](../../troubleshooting/dotnet_issues.md#install_dotnet_sdk_windows) how to install **.NET SDK** and check its version.


## Additional Reference Materials


For more details refer to the [Programming Quick Reference](../../start/quick_start/pqr/index_cs.md) article to learn key information on the workflow stages for developing a project with UNIGINE. It contains code examples that will be useful when developing your first UNIGINE projects.
