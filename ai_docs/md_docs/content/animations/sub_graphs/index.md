# Animation Subgraphs


A subgraph is a reusable animation graph that you create once and use in multiple places. It works like a function: you define a set of inputs and outputs, build the internal logic, save it as a separate file, and then reference it from any other animation graph using a **[Sub Graph](../../../content/animations/graph/node_library/subgraph/sub_graph.md)** node.


Subgraphs help you organize complex animation logic into manageable, reusable pieces. For example, you can package a locomotion state machine, a speed calculation utility, or an additive animation layer into a subgraph and reuse it across multiple character graphs without duplicating the logic.


Subgraphs are saved as `*.asubgraph` files - separate from the main `*.agraph` files. When you modify a subgraph file, all graphs that reference it are automatically updated (see [Automatic Updates](#cascade_regeneration)).


## Creating a Subgraph


To create a new subgraph:


1. In the *Asset Browser*, right-click and select *Create -> Animation Subgraph*. A new `*.asubgraph` file is created. | ![](subgraph_creation.png) | ![](file_animation_subgraph.png) *An .asubgraph asset in the Asset Browser* | |---|---|
2. Double-click the file to open it in the [Animation Graph Editor](../../../content/animations/graph/index.md).
3. Inside, you see a canvas with two special nodes already placed: ![](empty_animation_subgraph.png)

  - **[Sub Graph Inputs](../../../content/animations/graph/node_library/subgraph/sub_graph_inputs.md)** - defines the input ports that the subgraph exposes to parent graphs.
  - **[Sub Graph Outputs](../../../content/animations/graph/node_library/subgraph/sub_graph_outputs.md)** - defines the output ports.
4. Build your animation logic between these two nodes.


The [Sub Graph Inputs](../../../content/animations/graph/node_library/subgraph/sub_graph_inputs.md) node provides values from the parent graph to the internal nodes. The [Sub Graph Outputs](../../../content/animations/graph/node_library/subgraph/sub_graph_outputs.md) node receives the result of the internal logic and passes it back to the parent graph.


## Editing a Subgraph


There are two ways to open a subgraph for editing:


- Open the `*.asubgraph` file directly from the *Asset Browser* by double-clicking it.
- Double-click a **Sub Graph** node in a parent graph. The subgraph opens in a new editor window.


Both methods open the same underlying file. Any changes you make are saved to the `*.asubgraph` file and affect all graphs that reference it.


## Defining Inputs and Outputs


Subgraph inputs and outputs are dynamic - you add, remove, reorder, and rename them as needed.


### Adding an Input or Output


Select the **Sub Graph Inputs** or **Sub Graph Outputs** node. In the right panel, you see a list of the current ports with a toolbar above it. Click the *+* button to add a new port. Each port has:


| Label | The display name of the port (e.g., BasePose, BlendWeight, Direction). |
|---|---|
| Type | The data type of the port (see [Data Types](../../../content/animations/index.md#data_types) for the full list). |


![](custom_input_output.png)


Use the arrow buttons to reorder ports, and the trash icon to remove the selected port.


Changing a port's type or removing a port affects all **Sub Graph** nodes in parent graphs that reference this file - their corresponding ports update automatically during cascade regeneration (see [Automatic Updates](#cascade_regeneration)).


### Input Values


A subgraph keeps **two separate sets of input values**: one it uses **inside a parent graph**, and one it uses **on its own in preview**. The two are fully isolated. A value you set for preview never reaches a parent graph, and a value set on a parent never affects the preview.


Each set has its own connection and its own fallback field, so an unconnected input always has a value to fall back on. The two cases work as follows.


When you **open the subgraph on its own** for preview, there is no parent to supply the inputs, so the values come from the **Sub Graph Inputs** node itself:


- if the left-side pin of a port is connected to a **test driver** (a node that feeds the input a live value, for example an [Animation Player](../../../content/animations/graph/node_library/animation/animation_player.md) providing a pose), its value is used;
- otherwise, the default value typed into the field on the left side of the port is used.


![Subgraph Own Input Values](subgraph_own_input_values.png)

*In standalone preview, inputs come from the Sub Graph Inputs node: ports wired to test drivers (Float, Vec3, Bool) take their live values, while unconnected ports fall back to the value typed on the node.*


When the subgraph runs **inside a parent graph**, the value of each input is taken from the **[Sub Graph](../../../content/animations/graph/node_library/subgraph/sub_graph.md)** node that references the subgraph:


- if the matching port on the **Sub Graph** node is connected, its value is used;
- otherwise, the value typed into the field next to that port on the **Sub Graph** node is used. This lets you set a per-instance value without wiring a connection.


![Subgraph External Input Values](subgraph_external_input_values.png)

*Inside a parent graph, inputs come from the Sub Graph node: a connected port (Input 2) takes the wired value, while unconnected ports (Input 0, Input 3) use the value typed next to them on the node.*


## Testing a Subgraph in Isolation


A subgraph normally receives its inputs and skeleton from the parent graph it is placed in. To let you build and check a subgraph on its own, the editor can run it as a self-contained unit: when you open an `*.asubgraph` file directly, its result plays on a mesh in the preview viewport, just like a full animation graph, without any parent graph involved.


Everything described in this section is used only while working on the subgraph in isolation. None of it affects the subgraph when it is placed inside a parent graph, and none of it is included in a built application.


### Assigning a Preview Mesh


A subgraph has its own preview mesh field, used only in isolation. Assign a skinned mesh in the preview settings and its joints appear in the node dropdowns; without one, the dropdowns are empty. A parent graph always uses its own mesh instead.


![Subgraph Mesh](subgraph_mesh.png)


> **Notice:** For a reusable subgraph, assign a reference mesh that uses the same skeleton as the graphs it will be placed in, so it drops in without changes.


### Driving Inputs and Marking the Output


Because there is no parent to supply data, you provide the inputs and choose the result yourself, using three nodes:


| [Sub Graph Inputs](../../../content/animations/graph/node_library/subgraph/sub_graph_inputs.md) | Connect a source (such as an [Animation Player](../../../content/animations/graph/node_library/animation/animation_player.md)) to the left-side pin of an input to feed it a value for the test run (see [Input Values](#default_values)). |
|---|---|
| [Sub Graph Outputs](../../../content/animations/graph/node_library/subgraph/sub_graph_outputs.md) | Extra pins appear on the right side of this node, visible only while testing in isolation. They expose the subgraph's results so you can route them to the sink node below. |
| [Preview Output Pose](../../../content/animations/graph/node_library/subgraph/preview_output_pose.md) | A sink node that marks which pose is shown in the viewport. Connect the pose you want to preview to it. There can be only one Preview Output Pose per subgraph, and its input accepts a connection only from the **Sub Graph Outputs** node. |


Connections that exist only for this isolated test run are drawn as dashed lines, which keeps them visually distinct from the subgraph's actual logic.


## Using a Subgraph in Another Graph


To use a subgraph inside another animation graph:


1. Right-click on the canvas and select *Sub Graph* from the node creation menu. ![](subgraph_node_creation.png)
2. Select the subgraph from the dropdown list or pick the `*.asubgraph` file via the asset browser. The node's input and output ports update automatically to match the subgraph's defined inputs and outputs.
3. Connect the node's inputs to the appropriate sources in the parent graph.
4. Connect the node's outputs to the rest of the graph.


The **Sub Graph** node displays the same port labels and types as defined in the `*.asubgraph` file. You can use the same file in multiple places - in the same graph, in different graphs, or even nested inside other subgraphs.


## Automatic Updates


When you modify and save a `*.asubgraph` file, all animation graphs that reference it are automatically updated. Each **Sub Graph** node that references the modified file reloads it, regenerates its ports to match the new definition, and preserves existing connections where port types still match. Connections to removed or type-changed ports are disconnected.


This works through any depth of nesting: if subgraph A uses B, and B uses C, saving C updates both B and A.


## Circular Reference Protection


A subgraph cannot reference itself - neither directly nor through a chain of other subgraphs. The following cases are all detected and blocked:


- **Direct** - Subgraph A contains a *Sub Graph* node that points back to A.
- **Indirect** - Subgraph A references B, and B references A.
- **Deep chain** - *A -> B -> C -> ... -> A*, at any nesting depth.


When a circular reference is detected, an error is logged in the console and every **Sub Graph** node involved in the cycle is highlighted with an error color.


![](circular_reference.png)

*A direct circular reference: Subgraph A contains aSub Graphnode that points back to itself. The node is highlighted red. The console displays the error:AnimGraphNodeSubGraph: recursive call for "SubGraphGuid".*


## See Also


- [Animation Graph Editor](../../../content/animations/graph/index.md)
- [Node Library](../../../content/animations/graph/node_library/index.md)
- [Animation Graph Overview](../../../content/animations/index.md)
