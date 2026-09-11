# Scenario Manager Plugin


> **Warning:** The functionality described here is **EXPERIMENTAL** and is **not recommended for production use**. Future releases may bring significant changes to API and features. Backward compatibility of the final production-ready version is not guaranteed.


**Scenario Manager** - is a visual tool for *[creating](../../../code/plugins/scenariomanager/editor.md#sm_create)* and running lightweight scenario logic in your application. It is a framework that uses a node graph executed every frame to let you design multi-step action chains, instead of writing code manually.


[![](img/sm_framework_sm.png)](img/sm_framework.png)


The framework operates through two cooperating parts:


- **Scenario Manager Editor** - a web interface for building application logic through a visual node-based system, available at `http://localhost:8080`. It enables you to create logic of your application by connecting nodes (blocks) into a lightweight node graph that defines scenario behavior, with no recompilation required. Each node performs a specific operation: flow control, event handling, math or logical operations, data access, and others. The graph asset is stored as an `.sgraph` file (in JSON format). > **Notice:** The default IP address and port can be changed using the `scenario_manager_server` console command.
- **Application** - the Engine instance that hosts the editor and executes the scenario logic defined in the Scenario Manager editor, evaluating the node graph every tick. Communication between the editor and the engine is handled through a built-in HTTP server. > **Notice:** The editor is only available while the Engine is running, since the editor server runs inside the Engine process.


Scenario Manager communicates with the application world through the ***[DataBridge](../../../code/plugins/databridge/index_cpp.md)*** system.


It is also an integral part of the ***[MRO Template](../../../sdk/templates/maintenance/index.md)***. To open the Scenario Manager editor:


- Run the **MRO Template**.
- With the application running, open `http://localhost:8080` in your web browser.


## Key Concepts


### Graph


A graph is a visual representation of your scenario logic, consisting of nodes and connections that describe a single unit of logic, serialized to JSON format.


![Scenario Manager graph](img/sm_graph_overview.png)


### Script


A script is a graph instance currently loaded into the Scenario Manager for execution. A single graph can produce several script-instances, each running independently with its own state and variables.


![Scenario Manager script](img/sm_script_overview.png)


### Node


Nodes are the building blocks of a Scenario Manager graph. Each node represents a specific operation: flow control, event handling, performing math or logical operations, data access.


Nodes placed on the canvas have input and output ports that define what data they receive and produce. Depending on the node type, nodes may also have one or more configurable parameters (e.g., a DataBridge path, a portal name, an interval value, or other node-specific settings).


![Scenario Manager node](img/sm_node_s.png)

*DataBridgeSet Parameternode with a configurable parameter. Input ports on the left, output port on the right*


Every node available in the graph, with its ports and parameters, is described in the *[Scenario Manager Nodes](../../../code/plugins/scenariomanager/node_library/index.md)* reference.


### Ports and Connections


![](img/sm_connections.png)


**Ports** are connection points on nodes. Input ports are located on the left side of a node, output ports on the right side. Each port has a specific data [*type*](#sm_types) that determines which connections are valid. Two types of ports are available:


- **White - execution ports (flow)**. Control the order of execution.
- **Colored - data ports** (color indicates type: bool, float, vec3, etc.). Pass values between nodes.


**Connections** are links between an output port of one node and an input port of another. They define how data flows through the graph. Connections are type-checked: you can only connect ports with compatible data types - types must match or be implicitly convertible. Two types of connections are available:


- **White - execution** flow.
- **Colored - data** (color indicates type: bool, float, vec3, etc.). A connection with a color gradient indicates an implicit type conversion.


> **Notice:** Data output ports can connect to multiple inputs, but each input port accepts only one connection. Execution ports are limited to a single connection - one wire per port.


To see the type/color mapping in the editor, open the menu and select *Palette (types)*.


![](img/sm_palette.png)


### Interface


Interface is an exposed port (input or output) of a subgraph. These ports define what data the subgraph receives and returns. Interfaces are controlled via the *[Interface](../../../code/plugins/scenariomanager/editor.md#panel_interface)* panel of the editor.


![](img/sm_interface.png)

*Interface definition of a graph (left) and its output ports as seen on the subgraph node (right)*


### Variables and Constants


Variables are named values stored within a graph. Their name, type (bool, float, string, array, etc.), and default value are configured in the editor:


- **Local variables** are defined in the *Variables* panel. They belong to the current graph and are not visible outside it.
- **Global variables** are shared across all graphs and are defined in the *Global Variables* panel.


**Constants** are a group of data nodes (e.g., *Int, Bool, Float, String, Vec3*, etc.) that hold fixed values set directly in the node parameters. Unlike variables, constants have no name and cannot be modified at runtime. They are added to the canvas from the *Constants* category of the node palette.


![](img/sm_variables.png)

*Local variable incremented by a constant*


## Graph Structure


A Scenario Manager graph is a multi-level structure with at least one entry point that combines data reading/writing and execution flow through nodes and nested `.sgraph` files (subgraphs).


### Entry Points


A logic graph must have a clearly defined entry point, an event that initiates graph execution. Scenario Manager has several out of the box events such as:


- **On Init** - triggers once when the script is loaded.
- **On Update** - triggers every frame (each tick) during the main loop.
- **On Shutdown** - triggers once when the script is unloaded, on any unload path: when the script is stopped from the editor or from code, when it is reloaded, and when the application is closing.
- **On Timer** - triggers periodically based on the *interval* parameter.
- **Custom Event** - a pair of nodes: *Send Event* (execution input) and *On Event* (execution output). Enables communication between scripts through named events.
- **On Parameter Changed** - triggers each time a parameter at a specified DataBridge path changes its value.
- **Event Subgraph** - a [*subgraph*](#graph_subgraphs) node that allows emitting events outward.


![On Update event node](img/sm_event.png)


### Execution Flow


This flow is responsible for organizing the order of execution within the graph. Execution progresses from one node to another through execution connectors, determining when and in what sequence operations are performed.


**Execution flow includes:**


- **Branching** - if-else *Branch* and *Switch* nodes for conditional routing.
- **Looping** - For *Loop* and *While* Loop nodes for iterative execution.
- **Sequencing** - *Sequence* node for ordered progression and *Delay* node for timed pauses.
- **Conditional flow control** - *Gate* node for enabling/disabling execution and *Do Once* for one-time execution until reset.


### Data Flow


This flow is responsible for data transfer within the graph. Data is passed between nodes through data connectors, which are color-coded according to the data type they carry (see the *[palette reference](#sm_types)* for the complete type-color mapping), enabling the graph to compute, store, and exchange information throughout execution.


**Data flow includes:**


- **Variables** - local and global variables, constants.
- **Math operations** - arithmetic, comparisons, boolean logic, trigonometry, vector and matrix operations, rotations, random generation, interpolation.
- **DataBridge integration** - reading and writing parameters by path, reactive change events, batch operations, path construction.


![Execution and Data flow within a Scenario Manager graph](img/sm_flow.png)


### Subgraphs


A subgraph is a graph stored as a separate ***.sgraph** file that can be referenced as a node inside another graph. Subgraphs enable you to encapsulate common application logic and build modular, maintainable logic by reusing the same subgraph across multiple graphs. Each subgraph defines its own input and output ports via the *Interface* panel of the editor. These ports appear as ***data*** and ***execution*** connectors on the subgraph node when used in another graph. A subgraph is read from its file when the graph referencing it is loaded, so changes to a subgraph take effect in a running script the next time that script is reloaded or started again.


![Subgraph ports defined in the Interface panel of the editor](img/sm_sg_inputs.png)


For faster navigation, you can use the built-in search feature when selecting a graph to use as a subgraph.


![](img/sm_subgraph_search.png)


### Debug and Utility


This category includes nodes for debugging, diagnostics, and auxiliary operations that assist during development and runtime monitoring, such as:


- **Comment** - a meta-node that displays as a text block in the editor without affecting runtime behavior.
- **Diagnostics** - *Log, Format Log, Console Command, Print to Screen*, and *Assert* nodes for logging, debug output, console interaction, and condition validation.
- **Type Conversion** - explicit type casting between supported types.
- **Portals** - *Exec Portal In* / *Exec Portal Out* and *Data Portal In* / *Data Portal Out* nodes that serve as named tunnels for wires under the graph, reducing visual clutter in complex graphs by avoiding crossing and tangled connections. A portal pair is matched by the *name* parameter: execution reaching an *Exec Portal In* continues from the *Exec Portal Out* with the same name, and a *Data Portal Out* provides the value received by the *Data Portal In* with the same name.

 Best PracticeNodes can be organized into named ***[groups](../../../code/plugins/scenariomanager/editor.md#layout_canvas_groups)*** for better visual organization of complex graphs.
## Data Types


Every port and connector in the graph is color-coded. White connectors carry the execution flow. Data connectors are color-coded according to the type of value they carry. A wire with a color gradient indicates an implicit type conversion between compatible types. The following types are available:


| ![](img/types/float.png) **Float** | ![](img/types/vec2.png) **Vec2** | ![](img/types/vec3.png) **Vec3** | ![](img/types/vec4.png) **Vec4** |
|---|---|---|---|
| ![](img/types/int.png) **Int** | ![](img/types/ivec2.png) **Ivec2** | ![](img/types/ivec3.png) **Ivec3** | ![](img/types/ivec4.png) **Ivec4** |
| ![](img/types/string.png) **String** | ![](img/types/dvec2.png) **Dvec2** | ![](img/types/dvec3.png) **Dvec3** | ![](img/types/dvec4.png) **Dvec4** |
| ![](img/types/mat2.png) **Mat2** - a 2x2 matrix. | ![](img/types/mat3.png) **Mat3** - a 3x3 matrix. | ![](img/types/mat4.png) **Mat4** - a 4x4 matrix. | ![](img/types/dmat4.png) **Dmat4** - a double-precision 4x4 matrix. |
| ![](img/types/quat.png) **Quat** - a quaternion, used for rotations. |  |  |  |
| ![](img/types/bool.png) **Bool** - a boolean value (true or false). |  |  |  |
| ![](img/types/array.png) **Array** - an ordered list of values, accessed by index. |  |  |  |
| ![](img/types/any.png) **Any** - a universal port type resolved automatically based on the connected port. For example, an Any input that receives a Vec3 connection becomes a Vec3 port. |  |  |  |


## Using Scenario Manager in Your Project


To use Scenario Manager in your own project, do the following:


1. Open the *Templates* tab in the SDK Browser and choose a template that meets your needs. Click *Create Project*. ![](../../../sdk/projects/create_project_cpp.png)
2. In the project creation window that opens, click *Advanced Settings > Plugins*. ![](img/add_plugin.png)
3. Enable the `Scenario Manager plugin`, click *Add* and *CREATE NEW PROJECT*. The project will appear in the *My Projects* tab list. > **Notice:** For Scenario Manager to work properly, the [DataBridge](../../../code/plugins/databridge/index_cpp.md) plugin is required. It will be added to the project configuration automatically.
4. Run the project and load the plugin with the `plugin_load UnigineScenarioManager` console command, or specify the `extern_plugin` command line option on the application start-up: ```bash -extern_plugin "UnigineScenarioManager" ``` > **Notice:** DataBridge plugin is loaded along with Scenario Manager automatically.
5. To use Scenario Manager in **UnigineEditor**, click the *Customize Unigine Editor Options* button on the project's card, and add the same argument `-extern_plugin "UnigineScenarioManager"`.


Once the plugin is loaded, open `http://localhost:8080` in your web browser to access the *[Scenario Manager editor](../../../code/plugins/scenariomanager/editor.md)*.


> **Warning:** Using Scenario Manager with the **UnigineEditor** is currently **experimental** and may cause *[crashes](#sm_troubleshooting_name)*. Future releases will bring improvements to functionality and stability.


## Troubleshooting


1. **Unable to connect to localhost:8080** - The application is not running or the plugin is not loaded. Start the application first, then refresh the page. Use the `plugin_load UnigineScenarioManager` command in the console to load the plugin.
2. **Port 8080 is already in use** - Another running Engine instance is holding the port. Close the extra instance.
3. **Changes in the graph do not apply** - Save the graph (*Ctrl+S*). If the graph is already running, wait for hot reload to apply the changes, or reload the application.
4. **Graph name displays incorrectly in UnigineEditor** - Update the name attribute in the `*.graph.meta` file. Renaming a graph in the Scenario Manager editor changes the `.sgraph` file name, but the `.sgraph.meta` file, located in the same folder, still keeps the old one. Therefore, when assigned to a property in UnigineEditor, the graph will still be displayed under its original name. To fix this, update the `<runtime name=".sgraph"/>` tag manually in the `*.sgraph.meta` file. > **Warning:** Renaming a graph while the **UnigineEditor** is running may cause the Editor crash.


## See also


- *[ScenarioManager Plugin](../../../api/library/plugins/scenariomanager/index.md)* classes
- *[DataBridge Plugin](../../../api/library/plugins/databridge/index.md)* classes
- [MRO Simulator Template](../../../sdk/templates/maintenance/index.md) with Scenario Manager integration
