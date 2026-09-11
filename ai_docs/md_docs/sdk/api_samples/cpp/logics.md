# App Logic

> **Notice:** The complete sample source code is available on GitHub:
> **[github.com/unigine-engine/cpp-api-samples](https://github.com/unigine-engine/cpp-api-samples)**.


This section contains expamples displaying how to implement the application logic.


## Advanced Event Connection Patterns

This sample demonstrates advanced usage of the UNIGINE **[event system](../../../code/fundamentals/events/index.md)**.


*EventsAdvancedSample.cpp* triggers custom rotation events when specific keys are pressed. Each event passes one or more arguments to connected listeners.


*EventsAdvancedUnit.cpp* shows how to connect various types of handlers, including:


- Class methods with extra arguments
- Free functions with discarded or additional arguments
- Lambdas using *connectUnsafe()*
- Storing connections using *EventConnection* or *EventConnectionId* for later disconnection


This sample helps understand flexible patterns for event handling in modular component systems.


**SDK Path:***<SAMPLES_PROJECT_PATH>/source/app_logic/advanced_event_connection_patterns*
## Component Parameters In Editor

This sample demonstrates possible variations of component parameters. of component parameter types available in the **[Component System](../../../principles/component_system/component_system_cpp/index.md)**. It includes primitive types, vectors, masks, files, properties, materials, nodes, curves, structs, arrays, and advanced features like conditional visibility and value filtering.


Select the **component_parameters** *Node Dummy* in the Editor and explore all parameter variations in the *Parameters* window. This serves as a comprehensive reference for available parameter types and their configuration options.


**SDK Path:***<SAMPLES_PROJECT_PATH>/source/app_logic/component_parameters_in_editor*
## Component System Example

This sample illustrates how to implement your application's logic via a set of building blocks - **components**, and assign these blocks to nodes. A logic component integrates a node, a property, and a C++ class containing logic implementation.


The sample includes a controllable pawn with basic movement, rotating boxes that periodically spawn projectiles, and a floating UI label displaying health, survival time, and active component count.


The sample demonstrates how to:


- Decompose application logic into modular, reusable components
- Create and assign custom logic components at runtime
- Implement interaction between independently managed components.


More details about the Component System sample are available in the official documentation linked below.


**SDK Path:***<SAMPLES_PROJECT_PATH>/source/app_logic/component_system_example*
## Console Interaction

This sample demonstrates how to interact with the Engine's built-in console and add custom console commands and variables via API using the *[Console](../../../api/library/engine/class.console_cpp.md)* and *ConsoleVariable* classes. It shows how to define different types of console variables: *[ConsoleVariableInt](../../../api/library/common/class.consolevariableint_cpp.md)*, *[ConsoleVariableFloat](../../../api/library/common/class.consolevariablefloat_cpp.md)*, and *[ConsoleVariableString](../../../api/library/common/class.consolevariablestring_cpp.md)*, and how to register custom console commands.


Commands are linked to callback functions using *[MakeCallback](../../../api/library/common/class.unigine.namespace_cpp.md#MakeCallback_Retm)*, and can be executed directly from code or entered manually through the console. Commands can also be added and removed dynamically at runtime, making the system flexible for various use cases. Console variables can be accessed or changed through both code and the console interface.


For demonstration, to move the Material Ball in the scene use the custom command `control_node [x] [y] [z]` in the Console (`), where *x, y, z* are the target world coordinates (e.g., `control_node 0 5 1`).


This functionality can be used for development, debugging, rapid prototyping, and runtime adjustments in interactive applications.


**SDK Path:***<SAMPLES_PROJECT_PATH>/source/app_logic/console_interaction*
## Custom Stream

This sample demonstrates how to create a custom stream class by inheriting from *StreamBase* and use it for reading from and writing to files. The resulting stream is used to serialize and deserialize basic data types to and from a binary file.


The sample provides a wrapper around standard *C* file *I/O* functions and integrates with the **UNIGINE** stream system by implementing the *StreamBase* interface. In the sample logic, a binary file is first created and filled with data via *[Stream::writeString()](../../../api/library/common/class.stream_cpp.md#writeString_cstr_int)*, *[writeInt()](../../../api/library/common/class.stream_cpp.md#writeInt_int_int)*, and *[writeFloat()](../../../api/library/common/class.stream_cpp.md#writeFloat_float_int)*. Then the file is reopened in read mode and the same values are read back using the corresponding *Stream 'read'* methods, verifying the functionality of the custom stream.


This example serves as a reference for implementing custom stream sources (e.g., from memory, network, or virtual filesystems) and integrating them with the Engine's serialization tools.


**SDK Path:***<SAMPLES_PROJECT_PATH>/source/app_logic/custom_stream*
## Euler Angle Composition And Decomposition

This sample demonstrates how the order of angles affects the resulting rotation. You can also observe different ways of decomposing the current rotation by various angle sequences.

This example helps to understand 3D rotations using Euler angles. It shows how different sequences can lead to different orientations in space.


**SDK Path:***<SAMPLES_PROJECT_PATH>/source/app_logic/euler_angle_composition_and_decomposition*
## Event Connection Patterns

This sample demonstrates four different patterns for subscribing UNIGINE's *[Events](../../../code/fundamentals/events/index.md)* via the C++ API, highlighting how event handler lifetime and management can vary depending on the approach.


Each method demonstrates a different strategy for connecting to the same event and managing event handler lifetimes:


- *EventConnectionExample* stores a single event handler with manual control over its activation. This type of connection is useful when you need precise control � you can enable, disable, or fully disconnect the handler at any time.
- *EventConnectionsExample* acts as a container for multiple handlers. It handles cleanup automatically (via the destructor) and manually (by calling *[EventConnections::disconnectAll()](../../../api/library/common/events/class.eventconnections_cpp.md#disconnectAll_void)*). This is useful when you have many event handlers with varying lifetimes that need to be grouped.
- *InheritedEventConnectionExample* inherits *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* class, making connection management part of its internal logic. All connected handlers are automatically disconnected when the object is destroyed.
- *CallbackIDConnection* provides a low-level, manual way to manage handlers using a connection ID. It offers flexibility but requires careful memory and lifetime handling. This approach is considered unsafe and should only be used when you fully understand the implications.


Each example connects to a shared *EventHolder*, and handlers are triggered with a sample value. This setup is useful when designing modular, reactive systems that rely on flexible and explicit event-driven logic.


**SDK Path:***<SAMPLES_PROJECT_PATH>/source/app_logic/event_connection_patterns*
## File System External Package

This sample demonstrates how to create a custom data package using code and use it to generate objects in the scene. It creates a box mesh and spawns it 64 times in the scene with varied positions and rotations.


Package is a collection of files and data for UNIGINE projects stored in a single file. The *[Package](../../../api/library/filesystem/class.package_cpp.md)* class is a data provider for the File System. You can use it to load all necessary resources. Packages can be used to conveniently transfer files between your projects or exchange data with other users, be it content (a single model or a scene with a set of objects driven by logic implemented via C++ components) or files (plugins, libraries, execution files, etc.).


The *ExternalPackage* class describes the generation of a mesh (in this case, a box) and its saving to a temporary file at a specified path. The class also implements an interface for searching, reading, and retrieving information about files within the package.


The *ExternalPackageSample* class adds the created external package, and its contents are used to create meshes with different positions and orientations. This approach allows for quick and convenient management of a large number of objects without adding them by hand.


Using this example will help you understand how to organize work with external files, create and manage your own data packages, implement a mechanism for loading and reading data from a package.


**SDK Path:***<SAMPLES_PROJECT_PATH>/source/app_logic/filesystem_external_package*
## File System Mount Points

This sample demonstrates the functionality of [mount points](../../../principles/filesystem/index.md#mount_points) in the Engine file system.


*MountPointsSample.cpp* allows you to add or remove mount points for a folder and a package archive via API. If the mount point is active, an image stored inside will be loaded and displayed.


Mounted paths are shown in the *UI* window, where you can toggle between mounting or unmounting each resource. Images are accessed using virtual paths defined by the mount location.


The sample illustrates the concept of virtualized file access: if a resource is not available via a mount point, it will not be found or displayed by the Engine.


This approach is useful for working with external content (stored outside the **data** folder), modular data loading, or switching asset sets at runtime.


**SDK Path:***<SAMPLES_PROJECT_PATH>/source/app_logic/filesystem_mount_points*
## File Operations

This sample shows how you can create a text file and display its contents inside the widget via C++ API by using the *[File](../../../api/library/filesystem/class.file_cpp.md)* class. To create a text file, type the text from keyboard inside the *Writer* widget and press Write to save. Click **Read** inside the *Reader* widget to display the recorded information. The saved information will be displayed in the same widgets when you start the sample next time.
**SDK Path:***<SAMPLES_PROJECT_PATH>/source/app_logic/file_operations*

## Inverse FPS Usage

This sample demonstrates the importance of using *[Game::getIFps()](../../../api/library/engine/class.game_cpp.md#getIFps_float)* to implement movement logic independent of the frame rate.


The sample features two cubes moving back and forth along the X-axis. Their movement is implemented in the *IFpsMovementController.cpp* file.


The green cube uses *[Game::getIFps()](../../../api/library/engine/class.game_cpp.md#getIFps_float)* to scale its movement by the frame time delta. This ensures consistent speed across varying frame rates.


The red cube does not use *[Game::getIFps()](../../../api/library/engine/class.game_cpp.md#getIFps_float)* and simply applies constant translation per frame, which results in inconsistent behavior when frame rate changes.


Use the *Max FPS* slider to change the target frame rate.


This sample demonstrates why using time-based logic is essential for consistent results at different frame rates.


**SDK Path:***<SAMPLES_PROJECT_PATH>/source/app_logic/inverse_fps_usage*
## JSON

This sample shows how to generate a structured *JSON* document containing objects, arrays, and various data types such as strings, numbers, booleans, and null values. It also demonstrates how to traverse and print this structure recursively with indentation, imitating a pretty-printed output.


The sample begins by constructing a custom *JSON* structure in memory using *[Json::create()](../../../api/library/common/class.json_cpp.md#Json)* and its child manipulation methods. Nodes are added dynamically and include both named and unnamed children of various types. Once built, the structure is traversed recursively and printed to the Console in a readable format using indentation and commas, based on node type and position. The code demonstrates how to distinguish between arrays, objects, and primitive values when printing.


This sample is useful for learning the basics of *JSON* manipulation, such as creating structured data, traversing an element tree, and formatting output. It can serve as a foundation for processing *JSON* data (e.g., responses to *REST API* requests), as well as for complex serialization or debugging tools.


**SDK Path:***<SAMPLES_PROJECT_PATH>/source/app_logic/json*
## Materials And Properties Enumeration

This sample demonstrates how to access all materials and properties in the project via API.


The sample iterates through the list of registered in the *Property Manager* via *[Properties::getProperty()](../../../api/library/engine/class.properties_cpp.md#getProperty_int_Property)* and prints out the names and child counts for each. It also gets all available materials from the *Materials Manager* via *[Materials::getMaterial()](../../../api/library/rendering/class.materials_cpp.md#getMaterial_int_Material)*, and lists them along with their file paths and number of children.


This can be used as a reference for accessing and working with project assets at runtime - whether for inspection, dynamic assignment, or content management logic.


**SDK Path:***<SAMPLES_PROJECT_PATH>/source/app_logic/materials_and_properties_enumeration*
## Type Safe Callbacks

This sample demonstrates how to use the *[CallbackBase](../../../api/library/common/callbacks/class.callbackbase_cpp.md)* class via the C++ API to wrap and call functions and class methods with various numbers of arguments.


Callback mechanism is useful in scenarios such as event-driven systems, user interface interactions, or asynchronous task management in applications requiring dynamic function invocation.


Open the Console (`) to view the callback execution log.


Callbacks are created using the *[MakeCallback](../../../api/library/common/class.unigine.namespace_cpp.md#MakeCallback_Retm)* method for both standalone functions and member methods, including parameterized versions with up to four arguments. Once created, callbacks can be executed using *[CallbackBase::run()](../../../api/library/common/callbacks/class.callbackbase_cpp.md#run_void)* method, optionally passing different arguments at runtime. This allows storing and triggering functions dynamically through a unified interface.


**SDK Path:***<SAMPLES_PROJECT_PATH>/source/app_logic/type_safe_callbacks*
## XML

This sample demonstrates how to create and manipulate an *XML* document using the *[Xml](../../../api/library/common/class.xml_cpp.md)* class. It creates a nested *XML* tree with multiple child nodes, each containing arguments and optionally a text value.


The structure is built using the *[Xml::addChild()](../../../api/library/common/class.xml_cpp.md#addChild_cstr_cstr_Xml)* method, and the arguments are parsed using *[Xml::getArgName()](../../../api/library/common/class.xml_cpp.md#getArgName_int_cstr)* and *[Xml::getArgValue()](../../../api/library/common/class.xml_cpp.md#getArgValue_int_cstr)*. After construction, the *XML* tree is traversed recursively to display the structure and all attributes in the Console output.


This approach demonstrates the use of the *[Xml](../../../api/library/common/class.xml_cpp.md)* class for working with hierarchical data, which is useful for config files, level data, and other structured content in *XML* format.


**SDK Path:***<SAMPLES_PROJECT_PATH>/source/app_logic/xml*
