# Engine Architecture


There are different approaches to setting up game architecture, ranging from all-in-one solutions, where game logic is fused with an engine, to a heap of separate modules, each of which is responsible for one part of functionality. UNIGINE is somewhere in the middle of this scale, it incorporates everything one needs to implement a game or other 3D application, except for the application logic, networking, and AI. UNIGINE includes only typical game logic, common for applications of all types, and this is done intentionally.


This may not seem an advantage, because in order to create a game, one needs to do a great deal of programming and by themselves implement common functionality widely used in games of the required genre. However, lack of the genre-specific game logic is not so bad, as it makes UNIGINE a general-purpose library, easily re-usable in different projects. Moreover, developers are not bound to some specific genre, they can experiment with several genres at once, which is extremely difficult if a special-purpose engine is used. For example, it's difficult to make a mix of a shooter and a racing game out of an engine created solely for first-person shooters. Also, UNIGINE allows plugging of external modules, which can contain genre-specific functionality and can be re-used, too. This all makes UNIGINE a rather flexible base for a wide range of 3D applications.


To understand the architecture of UNIGINE is very important both for developers and for content creators. The former will know what they are allowed to do, what they can achieve, and what to expect from UNIGINE. The latter will understand how their content is going to be processed.


> **Notice:** A more detailed and more programmer-oriented description of UNIGINE workflow can be found in the article [Execution Sequence](../../../code/fundamentals/execution_sequence/index.md).


The diagram below demonstrates interrelations between internal components of UNIGINE and different external entities.


[![](engine_architecture_sm.png)](engine_architecture.png)


Everything starts when the custom *application* calls UNIGINE [*C++ API*](../../../api/index.md) functions. These calls are done using C++/C#. A [C++ application](../../../code/cpp/application.md) directly calls functions of the API. A [C# application](../../../code/csharp/application.md) uses the *C# Wrapper* (`UnigineSharp.dll`), which, in turn, uses the *C Wrapper* (`UnigineWrapper.dll`, `UnigineWrapper.so`) to interact with the UNIGINE API.


The application logic can be implemented right in the [*AppWorldLogic*](../../../code/fundamentals/execution_sequence/app_logic_system.md#worldlogic), [*AppSystemLogic*](../../../code/fundamentals/execution_sequence/app_logic_system.md#systemlogic) and [*AppEditorLogic*](../../../code/fundamentals/execution_sequence/app_logic_system.md#editorlogic) classes or via a set of *Components* using the [*Component System*](../../../principles/component_system/index.md) included in the API.


> **Notice:** [*C# Component System*](../../../principles/component_system/component_system_cs/index.md) is a part of the C# Wrapper.


The application functionality can be extended with *Engine Plugins*. UNIGINE provides a set of [ready-to-use plugins](../../../code/plugins/index.md), however, you can implement a custom one. You can also implement custom [*Editor Plugins*](../../../editor2/extensions/index.md) that extend functionality of the [UNIGINE Editor](../../../editor2/index.md).


API calls are passed to the *Engine*, which initializes required resources: registers extensions, loads core data, configuration files, user interface files, plugin directories. As all these resources are organized in a special data directory and, moreover, can be [packed](../../../tools/archiver/index.md), they are loaded by means of the *File System*. In addition, the file system tracks the endianness of files. Note that if you add files to this directory after the initialization is completed, you need to reload the file system component.


After initialization, the Engine runs the other subsystems. The scheme above contains the main ones:


- *App* manages the [main loop](../../../code/fundamentals/execution_sequence/main_loop.md) and controls the graphic context (manages events of the controls, updates window parameters).
- *Render* renders the scene. It needs additional resources to complete its tasks: textures, meshes, and animations. The required graphics resources are passed to the Render from the *File System*.
- *World* loads files which are required to build the current scene, and determines the set of visible nodes, which later will be sent to the *Render*. The World also tells the *Sound*, when and how to play environmental sounds, which sources are placed somewhere in the world and have spatial properties. The World cooperates with the *Physics*, which performs physical calculations (collision detection, joints solving, fluid buoyancy, and so on). To put it shortly, the World does not draw objects, play sounds, or perform physical calculations on its own. Instead, it delegates these tasks to corresponding subsystems.
- *Game* passes to the *World* (on demand) the time in seconds it took to complete the last frame. The *World* is updated according to the received value.
- *Physics* controls the simulation of physics in the *World*.
- *Input (Controls)* handles input from the *Input Devices* and passes the feedback. The application can read and somehow process the obtained input, if required.
- *Materials* and *Properties* manages materials and properties. They are loaded from the *File System*.
- *Sounds* receives sounds from the *File System* and passes them to the *Sound Card* to be played.
- *GUI* draws the user interface. In UNIGINE, GUI objects can be either stand-alone or a part of the displayed virtual world. In the latter case, they are managed by the *World* just like other nodes. When the rendered image, possibly containing the GUI, is displayed, the user starts interacting with the world. The user can influence the world by means of various input devices. Input from these devices is sent to the GUI and to the *Controls*. The GUI processes the input, detects the clicked element, and executes the corresponding callback function. The *Controls* subsystem processes input that is not related to the GUI, for example the player's actions in the game. Note that the GUI always gets the input data before the *Controls* and, therefore, has a higher priority.
