# From Graph to Runtime


When you save a graph in the Scenario Manager editor, it is serialized into a JSON `.sgraph` file that is interpreted directly at runtime. Instead of generating native code, Scenario Manager loads the graph, parses the JSON, and executes it on the fly, making it a convenient tool that greatly simplifies writing and iterating on **lightweight scenario logic**. This approach eliminates the need for a compiler toolchain and enables hot reload, allowing changes to take effect without restarting the application.


## What Is an .sgraph


An `.sgraph` file is the JSON-based graph definition stored on disk. Each `.sgraph` file represents one graph and contains all nodes, connections, and metadata required for execution. When loaded, it produces a **script** instance that runs within the Scenario Manager runtime.


### The .sgraph File Structure


- **Metadata** - contains the graph's version, name, description, author, created and modified timestamp.
- **Nodes** - contains the complete list of nodes in the graph. Each node includes:

  1. *id* - a unique numeric identifier within the graph
  2. *type* - a string that references a registered node type in the Scenario Manager node registry
  3. *size and position (pos)* - the node's width and height in pixels and position on the editor canvas
  4. *inputs and outputs* - arrays describing the node's ports. Each port specifies a name, a type (data type or -1 for execution flow), and a links array referencing connection indices
  5. *properties* - node-specific parameters that are configurable in the editor (e.g., path for DataBridge nodes, condition for Branch nodes, interval for Timer nodes)
  6. *title and color* - optional visual metadata for display in the editor.
- **Connections** - defines the links between nodes. Each connection specifies `from_node` and `from_port`, and `to_node` and `to_port`. Ports are identified by their index in the node's inputs/outputs array.
- **Subgraphs** - reference another `.sgraph` file via a file property. Exposed input and output ports are defined in the subgraph's *[Interface](../../../code/plugins/scenariomanager/editor.md#panel_interface)* panel and stored in the node's properties
- **Variables** - include a name, type (*bool, int, float, string, vec3, vec4, mat4, array*), and a default value.
- **Groups** - visual organization containers that help structure complex graphs. Each group includes a title, bounding box (position and size), and a color for visual distinction.


As the `.sgraph` format stores both editor-specific and runtime data, this allows the graph to be loaded exactly as it was saved, preserving layout and organization alongside execution logic.


## Runtime Pipeline


When you save the graph in the Scenario Manager editor, the following steps happen automatically:


1. The editor serializes the graph into a JSON `.sgraph` file and sends it to the built-in HTTP server.
2. The Scenario Manager reads the `.sgraph` file, parses the JSON, and builds the in-memory graph representation.
3. Nodes are sorted by execution order at load.
4. The graph is executed directly from the in-memory representation. Execution starts from *[event nodes](../../../code/plugins/scenariomanager/index.md#graph_entry)* and proceeds through execution connections. Data nodes are evaluated lazily, only when their output is requested by a flow node. During this step, nodes that interact with *DataBridge* read from and write to *DataBridge* parameters, and subscribe to change events, enabling reactive logic that responds to the application world state.


Scenario Manager supports multiple scripts (graph instances) running simultaneously - each script has its own independent context: separate variables, state, and execution pointer. A script's **[state](../../../api/library/plugins/scenariomanager/class.scenariomanager_cpp.md#SCRIPT_STATE)** - loading, running, paused on a *[debugger](../../../code/plugins/scenariomanager/editor.md#panel_debug)* breakpoint, stopped by an execution error, or finished - can be queried from code via . Only running scripts are ticked: a script that hits an execution error stops being updated.


## Console Commands and Variables


The following console commands are available while the plugin is loaded.


| scenario_manager_log |  |
|---|---|
| **Description:** - **Variable.** Prints whether the plugin writes its messages, warnings, and errors to the engine log. - **Command.** Enables or disables the plugin's log output. ```text scenario_manager_log 0 ``` | **Arguments:** - ***1***, ***on***, or ***true*** - enable logging (by default) - ***0***, ***off***, or ***false*** - disable logging |
| scenario_manager_server |  |
| **Description:** - **Variable.** Prints the address and port the built-in HTTP server is bound to, and whether it is listening. - **Command.** Changes the bind target of the HTTP server that hosts the [Scenario Manager editor](../../../code/plugins/scenariomanager/editor.md). Rebinding drops all connected clients; if the new address and port cannot be bound, the previous ones are restored. ```text scenario_manager_server 127.0.0.1 8080 ``` | **Arguments:** - Port number alone - rebinds to this port, keeping the current address - Address in the *xxx.xxx.xxx.xxx* format followed by a port number - rebinds to both `127.0.0.1` and `8080` by default; can be changed via the [configuration file](#sm_config) or the [startup arguments](#sm_config_args). |


## Configuring the Plugin


### Via Configuration File


The address and port of the web editor server, and the plugin's log output, are set in the `scenario_manager.xml` configuration file shipped at `data/plugins/Unigine/ScenarioManager/`:


```xml
<?xml version="1.0" encoding="utf-8"?>
<scenario_manager>
	<server enabled="1" address="127.0.0.1" port="8080"/>
	<log enabled="1"/>
</scenario_manager>

```


To customize these settings for a project, simply copy this file with your own parameters to the project's `data` folder - it will take priority over the default one.


### Using Startup Arguments


The same settings can also be specified as *[startup arguments](../../../code/command_line.md)*, which override the configuration file:


- `-sm_addr` - the IPv4 address the web editor server binds to, in the *xxx.xxx.xxx.xxx* format.
- `-sm_port` - the TCP port of the web editor server, in the [1; 65535] range. Out-of-range values are ignored with a warning.
- `-sm_server` - 0 leaves the listener closed at start-up: scenarios still run, but the web editor stays unreachable until `scenario_manager_server` is run in the console.
- `-sm_log` - 0 mutes all log output of the plugin.
- `-sm_config` - path to a configuration file to read instead of the default one.


```bash
-sm_addr 0.0.0.0 -sm_port 9000
```


## Controlling Scripts from Code


Besides the editor and the command line, scripts can be loaded and controlled from application code via the *[ScenarioManager](../../../api/library/plugins/scenariomanager/class.scenariomanager_cpp.md)* class.


A graph is started by one of the load functions, each returning the **script ID** that addresses the running script afterwards:


- - loads a graph file.
- - the same, additionally binding the script to an entity identifier.
- - loads a graph straight from a JSON string instead of a file (this is how the editor runs a graph).


Scripts that are already running can be:


- **enumerated** with  and  - top-level scripts only, event-subgraph children are not counted.
- **found** by name or entity via  and .
- **stopped** with  or .


To communicate with running graphs, dispatch a named custom event via : it triggers every matching *On Event* node in every running graph. The script lifecycle can be observed through the following events:


- - a script is loaded.
- - a script is unloaded.
- - a custom event is dispatched.


Each of the load and unload functions also has a deferred variant - , , and  - that queues the operation to the start of the next update instead of performing it immediately. The direct variants cannot be called from the event callbacks above, where they deadlock.
