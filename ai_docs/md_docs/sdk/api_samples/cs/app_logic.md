# App Logic

> **Notice:** The complete sample source code is available on GitHub:
> **[github.com/unigine-engine/csharp-component-samples](https://github.com/unigine-engine/csharp-component-samples)**.


## Advanced Event Connection Patterns

This sample demonstrates advanced ways of subscribing to events in UNIGINE: using extra arguments, discarding parameters, and storing connection handles for disconnection.
**SDK Path:***<SAMPLES_PROJECT_PATH>/data/csharp_component_samples/app_logic/advanced_event_connection_patterns*

## Arcade Game Prototype

![](../../../samples/img/csharp_component_samples_arcade_game_prototype.jpg)

This sample showcases a flexible arcade-style interaction system, built with UNIGINE's C# API. It presents foundational gameplay mechanics commonly used in shooter, and action-style applications. The project serves both as a beginner-friendly learning resource and a base for prototyping more advanced features such as basic non-player behavior or scoring logic.

 **Core Features:**
- **Player Controller:** Control a robot character with keyboard input for movement and rotation.
- **Projectile System:** An automated turret fires projectiles using raycasting for hit detection and visual impact effects.
- **Enemy Turret:** A rotating turret that periodically shoots projectiles at the player.
- **Health System:** The robot takes damage and is destroyed when health reaches zero, with corresponding visual effects and cleanup.
- **Node Spawning & Deletion:** Bullets and particle effects are dynamically created and removed, with timed destruction to manage scene performance.
- **Visual FX (Optional):** Includes particle effects for shooting, impact, and destruction events.

 **Use Cases:**
- **Game Prototyping:** Provides a foundation for building shooter mechanics, or arcade-style gameplay.
- **Physics & Interaction:** Demonstrates raycasting-based hit detection.
- **Learning Tool:** Ideal for beginners exploring the UNIGINE C# API and gameplay scripting.


**SDK Path:***<SAMPLES_PROJECT_PATH>/data/csharp_component_samples/app_logic/arcade_game_prototype*
## Component Parameters In Editor

![](../../../samples/img/csharp_component_samples_component_parameters_in_editor.jpg)

This sample demonstrates possible variations of component parameter types available in the **[Component System](../../../principles/component_system/component_system_cs/index.md)**. It includes primitive types, vectors, masks, files, properties, materials, nodes, curves, structs, arrays, and advanced features like conditional visibility and value filtering.


Select the **component_parameters** *Node Dummy* in the Editor and explore all parameter variations in the *Parameters* window. This serves as a comprehensive reference for available parameter types and their configuration options.


**SDK Path:***<SAMPLES_PROJECT_PATH>/data/csharp_component_samples/app_logic/component_parameters_in_editor*
## Console Interaction

This sample demonstrates how to interact with the Engine's built-in console and add custom console commands and variables via API using the *[Console](../../../api/library/engine/class.console_cpp.md)* and *ConsoleVariable* classes. It shows how to define different types of console variables: *[ConsoleVariableInt](../../../api/library/common/class.consolevariableint_cpp.md)*, *[ConsoleVariableFloat](../../../api/library/common/class.consolevariablefloat_cpp.md)*, and *[ConsoleVariableString](../../../api/library/common/class.consolevariablestring_cpp.md)*, and how to register custom console commands.


Commands are linked to callback functions using *[MakeCallback](../../../api/library/common/class.unigine.namespace_cpp.md#MakeCallback_Retm)*, and can be executed directly from code or entered manually through the console. Commands can also be added and removed dynamically at runtime, making the system flexible for various use cases. Console variables can be accessed or changed through both code and the console interface.


For demonstration, to move the Material Ball in the scene use the custom command `control_node [x] [y] [z]` in the Console (`), where *x, y, z* are the target world coordinates (e.g., `control_node 0 5 1`).


This functionality can be used for development, debugging, rapid prototyping, and runtime adjustments in interactive applications.


**SDK Path:***<SAMPLES_PROJECT_PATH>/data/csharp_component_samples/app_logic/console_interaction*
## Euler Angle Composition And Decomposition

Example of the object rotation using Euler angles. You can also observe different ways of decomposing the current rotation by various angle sequences.


This example helps to understand 3D rotations using Euler angles. It shows how different sequences can lead to different orientations in space.


**SDK Path:***<SAMPLES_PROJECT_PATH>/data/csharp_component_samples/app_logic/euler_angle_composition_and_decomposition*
## Filesystem External Package

This sample demonstrates how to create a custom data package using code and use it to generate objects in the scene.


It creates a box mesh and spawns it 64 times in the scene with varied positions and rotations.


Package is a collection of files and data for UNIGINE projects stored in a single file. The *[Package](../../../api/library/filesystem/class.package_cpp.md)* class is a data provider for the File System. You can use it to load all necessary resources.


The *ExternalPackage* class describes the generation of a mesh (in this case, a box) and its saving to a temporary file at a specified path. The class also implements an interface for searching, reading, and retrieving information about files within the package.


The *ExternalPackageSample* class adds the created external package, and its contents are used to create meshes with different positions and orientations. This approach allows for quick and convenient management of a large number of objects without adding them by hand.


Packages can be used to conveniently transfer files between your projects or exchange data with other users, be it content (a single model or a scene with a set of objects driven by logic implemented via C# components) or files (plugins, libraries, execution files, etc.).


Using this example will help you understand how to organize work with external files, create and manage your own data packages, implement a mechanism for loading and reading data from a package.


**SDK Path:***<SAMPLES_PROJECT_PATH>/data/csharp_component_samples/app_logic/filesystem_external_package*
## Inverse FPS Usage

This sample demonstrates the importance of using *[Game.IFps](../../../api/library/engine/class.game_cpp.md#getIFps_float)* to implement movement logic independent of the frame rate.

The sample features two cubes moving back and forth along the X-axis. Their movement is implemented in the *IFpsMovementController* file. Use the *Max FPS* slider to change the target frame rate.


The green cube uses *[Game.IFps](../../../api/library/engine/class.game_cpp.md#getIFps_float)* to scale its movement by the frame time delta. This ensures consistent speed across varying frame rates.


The red cube does not use *[Game.IFps](../../../api/library/engine/class.game_cpp.md#getIFps_float)* and simply applies constant translation per frame, which results in inconsistent behavior when frame rate changes


This sample demonstrates why using time-based logic is essential for consistent results at different frame rates.


**SDK Path:***<SAMPLES_PROJECT_PATH>/data/csharp_component_samples/app_logic/inverse_fps_usage*
## XML

This sample demonstrates how to create and manipulate an *XML* document using the *[Xml](../../../api/library/common/class.xml_cpp.md)* class. It creates a nested *XML* tree with multiple child nodes, each containing arguments and optionally a text value.


The structure is built using the *[Xml.AddChild()](../../../api/library/common/class.xml_cpp.md#addChild_cstr_cstr_Xml)* method, and the arguments are parsed using *[Xml.GetArgName()](../../../api/library/common/class.xml_cpp.md#getArgName_int_cstr)* and *[Xml.GetArgValue()](../../../api/library/common/class.xml_cpp.md#getArgValue_int_cstr)*. After construction, the *XML* tree is traversed recursively to display the structure and all attributes in the Console output.


This approach demonstrates the use of the *[Xml](../../../api/library/common/class.xml_cpp.md)* class for working with hierarchical data, which is useful for config files, level data, and other structured content in *XML* format.


**SDK Path:***<SAMPLES_PROJECT_PATH>/data/csharp_component_samples/app_logic/xml*
