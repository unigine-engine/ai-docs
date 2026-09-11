# Material Editor


![](graph.png)


Material Editor enables you to create your own materials visually without writing a single line of code - just by creating and connecting nodes to build a graph. This is simple enough for users who are new to materials creation and powerful enough to let you do a lot of things. A brief list of features includes:


- Ability to create your own base materials (`*.mgraph`) and use them as directly assigned to objects or as parent materials for hundreds of other materials to avoid reassembling the material graph over and over again. The Materials hierarchy window will help you.
- Ability to create your own custom graph nodes using other nodes ([Subgraphs](#subgraphs)), or using your code. When you change the contents of a Subgraph, all materials using it will be updated as well.
- Ability to switch between material types (there are five available at the moment: *Mesh Opaque PBR, Mesh Alpha Test PBR, Mesh Transparent PBR, Mesh Transparent Unlit, Decal PBR*).
- Optional toggling of performance-affecting features on and off.
- Ability to construct the final material's UI, you can add various parameters and even combine them into groups for convenience.
- **Connector** � a special 'collapsed' mode of a graph node when it occupies less space and can be attached right to an input of another graph node.
- **Expression** � a special node enabling you to write simple arithmetic operations, but the main thing is that you can use it as a swizzle in combination with the ability to change the number of data components. Be sure you'll like it!
- Ability to [write code](#custom_code) in a special Function node, here you can implement even multiple functions calling each other.
- You can drag-n-drop textures from the Asset Browser or directly from your file manager, and they will be automatically imported with the corresponding nodes added to the graph.
- **[Loops](#loops)** � a complex, but very cool feature enabling you to repeat an arbitrary sequence of actions multiple times. We have analyzed multiple existing implementations of graph loops and invented a new one that is almost on par with loops in code. Why not write loops in code then? Because using a graph makes implementation of complex things inside a loop much easier than doing the same in code.
- When working with complex or large graphs, you may end up with your wires are all over the place crisscrossing each other and you may want more visual clarity. That's when [portals](#node_portal) come into play. You can connect a wire to a **Portal In** node at one location and then place a *Portal Out* node at any other location you need and take what you've supplied to **Portal In** from a **Portal Out** (like you dug a tunnel for your wire under the node graph).


### See Also


- [Material Nodes Library](../../../content/materials/graph/node_library/index.md)
- [Material Graph Samples](../../../content/materials/graph/samples/index.md)


## Material Graph Asset


A Material Graph asset (`.mgraph`) is both a **source material network** (node-based description to be compiled into a material) and a [normal base material](../../../content/materials/index.md#base_materials) that can be assigned to a mesh surface.


To create a new Material Graph, right-click in the *Asset Browser* to open the *Create* menu, then select **Create Material** -> **Material Graph**.


![](create_mgraph.png)


Specify a name for your graph asset. A new `*.mgraph` asset will be created in the current folder of your project.


![](mgraph_asset.png)


As the Material Graph asset represents a base material, it is also available in the root of the [Materials Hierarchy](../../../editor2/materials_settings/organizing_materials/index.md) and can be [assigned](../../../editor2/materials_settings/organizing_materials/index.md#assign_material) to supported surfaces and objects. Depending on the material's [type](#type) it can be assigned to the following objects:


- Mesh materials:

  - Surfaces of *[Static](../../../objects/objects/mesh/index.md), [Dynamic](../../../objects/objects/mesh_dynamic/index.md)*, and *[Skinned](../../../objects/objects/mesh_skinned/index.md)* meshes;
  - Surfaces of *[Mesh Clutter](../../../objects/objects/mesh_clutter/index.md) / [Mesh Cluster](../../../objects/objects/mesh_cluster/index.md)*.
- Decal materials:

  - [Projected](../../../objects/decals/proj/index.md), [Orthographic](../../../objects/decals/ortho/index.md), and [Mesh](../../../objects/decals/mesh/index.md) decals.


## Working with Material Graphs


Right-click on the `*.mgraph` asset and choose *Edit Graph* or simply double-click the asset to open it in the *Material Editor* window.


![](material_node_editor.png)


The *Material Editor* window includes the *Graph View* displaying the material graph network and the settings panel.


The material graph network consists of [nodes](#nodes) � functional blocks accountable for processing input data. By composing the graph network, you define the look of your material.


The **[Material](../../../content/materials/graph/node_library/misc/material.md)** node is the master node of your material. It provides a set of inputs for graphic data and generates a material of a specific type depending on the current [settings](#common_settings).


Finally, the output from the Master Node is connected to the **[Final](../../../content/materials/graph/node_library/misc/final.md)** node � the primary output material node.


> **Notice:** A material graph can contain several **Material** nodes, but only the one connected to the **Final** node will be used.


Press the **Save** button to save changes and compile the material graph to a base material. Compilation errors, if any, will be listed in the [Warnings and Errors](#warnings_and_errors) panel and in the *Console* window.


### Navigation Controls


| Mouse Wheel drag / RMB drag | Pan material graph |
|---|---|
| Mouse Wheel scroll | Zoom in/out |
| RMB / Space key | Display node creation palette |
| LMB click | Select node / edge |
| LMB drag on node | Move the selected nodes |
| LMB drag on background | Select nodes with the rectangle tool |
| LMB double-click on background | Display the Node creation menu |
| Shift + LMB on node | Add to node selection |
| Ctrl + LMB on node | Remove from node selection |
| Ctrl + C | Copy the selected nodes to the clipboard |
| Ctrl + V | Paste nodes from the clipboard |
| Ctrl + D | Clone the selected nodes without their connections |
| Ctrl + Shift + D | Clone the selected nodes retaining all their connections |
| Delete Key | Delete the selected nodes / edge |


> **Notice:** Copying and pasting networks of nodes is performed via a text format for convenient sharing of material graphs and their parts, so you can copy a shared text representation of a graph network and paste it right to your material editor.


### Common Settings


The Common Settings define the set of supported features for the material.


![](common_settings.png)


| Type | The type of the output material. - [Physically-based](../../../content/materials/library/mesh_base/pbr.md) mesh materials: - **Mesh Opaque PBR** � [deferred](../../../principles/render/sequence/index.md#opaque_deferred) opaque material - **Mesh Alpha Test PBR** � [deferred](../../../principles/render/sequence/index.md#opaque_deferred) alpha test material - **Mesh Transparent PBR** � [forward](../../../principles/render/sequence/index.md#transparent) (transparent) material - **Mesh Transparent Unlit** � transparent non-physical material - **Decal PBR** � [deferred](../../../principles/render/sequence/index.md#decals) decal material - **Decal Water** � [water](../../../principles/render/sequence/index.md#water_decals) decal material - **Post Effect** � [post-effect](../../../principles/render/sequence/index.md#post_materials) material |
|---|---|
| Vertex Mode | Defines the mode for [vertex adjustment](../../../content/materials/graph/node_library/misc/material.md#vertex) and [tessellation](../../../content/materials/graph/node_library/misc/material.md#tessellation_vertex_object_position) inputs: - **Position** � vertex positions are replaced by new values. - **Offset** � new values are added to original vertex positions. |
| Vertex Space | Defines the [vector space](../../../code/fundamentals/matrices/index.md#vector_spaces) for [vertex adjustment](../../../content/materials/graph/node_library/misc/material.md#vertex) and [tessellation](../../../content/materials/graph/node_library/misc/material.md#tessellation_vertex_object_position). Options depend on the *[Vertex Mode](#vertex_mode)* selected. - *Position Vertex Mode*: - **Camera World** � positions are relative to the camera position. - **Object** � positions are relative to the object's pivot. - **View** � positions are relative to the camera. - **Absolute World** � positions are relative to the world origin. - *Offset Vertex Mode*: - **World** � offsets are relative to the world origin. - **Object** � offsets are relative to the object's pivot. - **Tangent** � offsets are relative to the surface tangent. - **View** � offsets are relative to the camera. |
| Normal Space | Defines the space for [normal vectors](../../../content/materials/graph/node_library/misc/material.md#normal): - **World** - **Object** - **Tangent** - **View** |
| Depth Mode | Defines how the [Depth](../../../content/materials/graph/node_library/misc/material.md#depth) data is treated: - **Offset** - **Override** |
| Depth Shadow | Flag indicating whether custom depth affects shadows. |
| Tessellation | Enables the [Tessellation-related](../../../content/materials/graph/node_library/misc/material.md#tessellation_factor) inputs and [Tessellation](../../../content/materials/library/mesh_base/index.md#tessellation_tips) settings. |
| Two Sided | Enables the *[Two Sided](../../../editor2/materials_settings/index.md#two_sided)* option. |
| Write Velocity Offset | Enables writing velocity offset along with displaying related *[Velocity](../../../content/materials/graph/node_library/misc/material.md#velocity)* input for vectors defining screen-space pixel offset. |
| Advanced Mode | Enables the *[Compilation Settings](#compilation_settings)*. |


#### Transparent Material Settings


The following settings are available only for the **Mesh Transparent PBR** and **Mesh Transparent Unlit** material types.


| Blend Mode | [Blending](../../../principles/render/blending/index.md) preset. One of the following can be selected: - Alpha blend - Additive - Multiplicative - Disabled - Custom |
|---|---|
| Blend Src | Option used to scale the source color (the color of an overlaying material). Available only when **Custom** preset is selected. |
| Blend Dest | Option used to scale the destination color (the color of an obscured material). Available only when **Custom** preset is selected. |
| Overlap | Render polygons, to which the material is applied, on the top of the render. This can be used for UI elements. |
| Depth Test | Depth testing for the material. This option can be used to make the object visible, when occluded by other objects (e.g. a character behind a wall). |
| Write Scene Depth | Toggles writing to the depth buffer for the material on and off. With this option enabled the inner part of a transparent object won't be rendered if the outside surface was rendered first. The same can happen to a concave object. |
| Write Opacity Depth | Toggles writing to the opacity depth buffer for the material on and off. |
| Write Surface ID | Toggles writing the surface ID into the [Surface ID Buffer](../../../content/materials/custom_parameters/ids_and_buffers.md#modes) on and off. The surface ID is what lets effects be applied to a particular surface - decals, or a shader reading its [custom parameters](../../../content/materials/custom_parameters/reading_parameters.md) - and it also carries the classic [material mask](../../../principles/bit_masking/index.md#material_mask). Named **Write Material Mask** before 2.22. |
| Write Velocity | Toggles writing to the velocity buffer for the material on and off. The velocity buffer is used by such effects as TAA and motion blur. |
| Write Reactivity | Toggles writing to the reactivity mask on and off. The mask is used by temporal [upscalers](../../../editor2/settings/render_settings/upscalers/index.md), FSR among them, to reduce ghosting on rapidly changing pixels such as transparent effects. |
| Cast Global Illumination | Controls whether the surface is to be taken into account or ignored when baking Global Illumintaion (similar to the per-surface [*Cast Global Illumination*](../../../editor2/node_parameters/visual_representation/index.md#cast_gi) option). Can be used to ignore all transparent surfaces having the same material at once when baking GI, instead of switching them one by one. |


#### Decal Material Settings


The following settings are available only for the **Decal PBR** material types.


| Normal Under Decal | Defines the tangent space (*Tangent-Binormal-Normal* matrix) used for normal mapping: - **Take From Decal Mesh** � normals of the decal mesh (for *Mesh* decals) or plane (for *Orthographic* and *Projected* decals) are used; - **Up Direction of Decal** � decal's local up vector is used; - **GBuffer Normal** � normals from the screen *normal* buffer are used; - **GBuffer Depth Based Normal** � normals are constructed based on the screen *depth* buffer content. Unlike *GBuffer Normal*, this option provides unaltered normals as they are presented in the scene geometry. |
|---|---|
| Normal Blend Mode | [Blending](../../../principles/render/blending/index.md) mode for decal's normals: - **Alpha Blend** - **Additive** |
| Screen Projection | Enables Screen Projection of the decal instead of projecting it onto a surface (only *Mesh* decals are supported). |


#### Post-Effect Material Settings


The following settings are available only for the **Post Effect** material types.


| User Mode | Defines the way the stages of the rendering sequence are displayed: - **Artist Friendly** � simplified with unnecessary stages hidden. - **Technical Artist Friendly** � all available stages are listed. |
|---|---|
| Render Sequence Order | Specifies the stage of the rendering sequence when the material should be rendered. The set of available options depends on the selected *User Mode*. |
| Textures Streaming Mode | Specifies the streaming mode for the material's textures: - **Force Streaming For All** � forced streaming is applied for all textures of the material. - **Setting For Each Texture** � the forced streaming mode is set per texture in the material. You can toggle it on and off for each texture individually in the [*Parameters*](#params) panel. It is recommended to use this value for materials with textures that continuously change (via code, Tacker, etc.). |
| Use TAA | Toggles Temporal Anti-Aliasing for the material on and off. When enabled, the additional settings given below become available. |
| Color Clamping Mode | Specifies the color clamping mode used to reduce the ghosting effect. Available only when the [*Use TAA*](#use_taa) option is enabled. - **Disabled** � no color clamping. The material has a lag as it is several frames behind. - **By Neighbors** � color clamping with velocity accounted for. - **By Velocity** � simple color clamping mode. |
| Fix Flicker | Removes bright pixels using the pixel brightness information from the previous frame. It is recommended to enable this option for bright thin ropes, wires, and lines. Available only when the [*Use TAA*](#use_taa) option is enabled. |
| Frames By Color | Toggles on and off the accumulation of a variable number of frames over time depending on the pixel color difference between the current and previous frames. When enabled, the image becomes sharper, but it may produce additional flickering. Disabling this option may result in a more noticeable ghosting effect. Available only when the [*Use TAA*](#use_taa) option is enabled. |
| Antialiasing In Motion | Toggles improved anti-aliasing in motion (for moving camera and objects) on and off. Available only when the [*Use TAA*](#use_taa) option is enabled. |
| Diagonal Neighbors | Toggles on and off the consideration of diagonally neighboring pixels in the process of color clamping. Available only when the [*Use TAA*](#use_taa) option is enabled. |
| Catmull Resampling | Toggles the Catmull-Rom resampling on and off. The Catmull-Rom resampling allows you to reduce image blurring when the camera moves forward or backward. It is recommended to disable resampling at low settings. Available only when the [*Use TAA*](#use_taa) option is enabled. |
| Frames By Velocity | Toggles on and off the accumulation of a variable number of frames over time depending on the pixel velocity difference between the current and previous frames. Reprojection of pixels from the previous frame is performed considering the velocity buffer, and then the result is combined with the pixels of the current frame. This option reduces blurring and ghosting in dynamic scenes with numerous moving objects. Available only when the [*Use TAA*](#use_taa) option is enabled. |


#### Compilation Settings


These settings are only for the *[Direct3D](https://docs.microsoft.com/en-us/windows/win32/direct3dhlsl/d3dcompile-constants)* compiler (DirectX API).


> **Warning:** It is not recommended to make changes to the default values without understanding these settings.


| Optimization Level | Level of shader optimization and arithmetic refactoring (such as merging a *multiply* instruction followed by an *add* into a fused *mad*): - The level 0 means no optimization at all. Compilation is fast and provides the slowest code. - The other levels correspond to gradually increasing extent of optimization up to the highest level 4. |
|---|---|
| Warning Mode | The following modes are available: - **Disable** � warnings are disabled. - **Soft** � warnings are logged but ignored. - **Hard** � warnings are considered errors. |
| IEEE Strictness | Forces the IEEE strict compile. |


### Parameters


![](parameters.png)


In the *Parameters* panel, you define the list of material parameters.


The following controls are available:


- ![](parameter_add.png) **Add** � add a new parameter.
- ![](parameter_clone.png) **Clone** � clone the selected parameter.
- ![](parameter_up.png) **Move Up** � move the selected parameter up in the list.
- ![](parameter_down.png) **Move Down** � move the selected parameter down in the list.
- ![](parameter_remove.png) **Remove** � remove the selected parameter.


When adding a new parameter, you should specify the parameter's **Name**, **Type**, and default settings in the parameter creation dialog. The following set of parameter types is provided:


- **Slider** � a float value within the specified range ([0.0f; 1.0f] by default).
- **Color** � a float vector of 4 components representing a color value.
- **Texture2D**, **Texture3D**, **Texture2DArray**, **Texture2DInt**, **TextureCube** � a texture of the corresponding type.
- **Group** � an auxiliary type for grouping parameters. Use the ![](parameter_up.png) and ![](parameter_down.png) buttons to rearrange and group parameters.
- **Float, Float2, Float3, Float4** � a float value or a vector of N float values.
- **Int, Int2, Int3, Int4** � an integer value or a vector of N integer values.


To use a parameter in your material graph, drag the item to the *Graph View* to create a node of the corresponding type:


![](parameter_drag.gif)


Or add it directly via the *Create* menu:


![](parameter_add_via_create.gif)


#### Activity Condition


For each parameter you can specify a condition under which this parameter is active.


*Activity Condition* is an optional logical expression that manages dependencies between parameters, linking the availability of one parameter to the state or value of another.


![](condition.png)


**How It Works:**


The condition references other parameters defined in the same material. The expression is evaluated in real-time as parameter values are adjusted.


- When the condition evaluates to `true`, the parameter is **active** (shown and can be edited).
- When the condition evaluates to `false`, the parameter is **inactive** (hidden or disabled).


Parameters of the following types can be used in *Activity Conditions*:


| Bool | presented as a **checkbox**. Writing just the parameter name, e.g., `detail`, is equivalent to `detail == true`. |
|---|---|
| ComboBox | presented as a **dropdown list**. Values are compared by index or by *Item* label. The number of items is defined by the *Size* field. |
| Static Int | presented as a **numeric input field**. Values are compared using arithmetic operators (e.g., `layers > 1`). |


> **Notice:** You can combine multiple parameters of different types in a single condition using logical operators.


Parameter names used in conditions may contain letters, digits, and the characters `_, -, +`.


The following operators are supported:


| Category | Operators |
|---|---|
| Logical | `&&` `\|\|` `!` |
| Comparison | `==` `!=` `<` `>` `<=` `>=` |
| Bitwise | `&` `\|` `^` `~` `<<` `>>` |
| Arithmetic | `+` `-` `*` `/` `%` |
| Grouping | `(` `)` |


Combine operators to create complex conditional structures for your material parameters.


For example, given a *Bool* parameter `detail`, a *ComboBox* parameter `mode` with items *Opaque (index 0), Alpha (index 1), Additive (index 2)*, a *Static Int* parameter `layers`, and a *Bool* parameter `transparent`, the following conditions can be used:


| Condition | Meaning |
|---|---|
| detail | Active when the toggle is **ON** |
| !detail | Active when the toggle is **OFF** |
| mode == Alpha | Active when *Alpha* is selected **(by label)** |
| mode != Opaque | Active for any **non-*Opaque*** mode |
| mode == 2 | Active when *Additive* is selected **(by index)** |
| detail && mode != Opaque | Active when toggle is **ON** ***AND*** mode is not *Opaque* |
| (detail \|\| layers > 1) && transparent | Active when (toggle is **ON** ***OR*** layers > 1) ***AND*** transparent is **true** |

     Sorry, your browser does not support embedded videos.
### Warnings and Errors


![](warnings_and_errors.png)


The **Warnings and Errors** panel enables you to track problems in the material graph and is visible only if there are any.


The panel lists all problem nodes in the graph, select an entry to see the problems with its ports or data in the *Message* section.


Some warnings may appear after [migrating your content](../../../upgrade/migration_content/index.md) to a higher SDK version. These are reminder warnings meant to notify about changes in the logic of certain nodes. You can discard the warning by using the **Remove Warning** button.


### Nodes


![](nodes.png)


Nodes of Material Editor are functional blocks that represent data sources and processing instructions similar to variables and functions in shader programming.


Most nodes have the output preview shown on a preview sphere (for most nodes) or a plane (for textures).


Some nodes have a set of settings defining their behavior. Double-clicking the node opens the dialog for adjustment of the node's settings.


Nodes that have no more than one input and one output [port](#node_port) have a special **connector** mode � they are *collapsible* for convenience. A collapsed node connected to another node becomes attached to it. Drag the collapsed node to break the connection and detach the node.


![](node_collapse.gif)


Multiple selected nodes are disconnected together.


Nodes are split into [several groups](../../../content/materials/graph/node_library/index.md) based on their applicability and color-coded for better identification.


#### Port


A **port** defines an *input* (left side) or *output* (right side) of a node. Connecting [edges](#node_edge) to a port allows data to flow through the Material Graph node network.


Each port has a data type defining edges that can be connected to it. All data types are color-coded, meaning that each of them has an associated color used for identification.


| ![](node_library/img/types/float.png) **float** | ![](node_library/img/types/float2.png) **float2** | ![](node_library/img/types/float3.png) **float3** | ![](node_library/img/types/float4.png) **float4** |
|---|---|---|---|
| ![](node_library/img/types/int.png) **int** | ![](node_library/img/types/int2.png) **int2** | ![](node_library/img/types/int3.png) **int3** | ![](node_library/img/types/int4.png) **int4** |
| ![](node_library/img/types/float_2x2.png) **matrix** � a matrix of float values: *float2�2*, *float3�3*, *float4�4*. |  |  |  |
| ![](node_library/img/types/texture.png) **texture** � any type of a texture: [Texture 2D](../../../content/materials/graph/node_library/textures/texture_2d.md), [Texture 3D](../../../content/materials/graph/node_library/textures/texture_3d.md), [Texture 2D Array](../../../content/materials/graph/node_library/textures/texture_2d_array.md), [Texture 2D Int](../../../content/materials/graph/node_library/textures/texture_2d_int.md) and [Texture Cube](../../../content/materials/graph/node_library/textures/texture_cube.md). |  |  |  |
| ![](node_library/img/types/bool.png) **bool** � a boolean value used in [logical nodes](../../../content/materials/graph/node_library/logical/index.md) and [loops](#loops). |  |  |  |
| ![](node_library/img/types/undefined.png) **any** � arbitrary data type meaning the port supports several data types. |  |  |  |
| ![](node_library/img/types/unknown.png) **error** � indicates an error (e.g., no required input provided or type conversion has failed). |  |  |  |


Only one edge can be connected to any **input** port, but you can connect multiple edges to an **output** port.


Most input ports have a **default input value**.


#### Edge


An **edge** represents a connection between two [ports](#node_port) (input and output). Edges define how data flows through the Material Graph node network. You can only connect an edge from an output port to an input port.


A new edge is created by dragging from the desired output port to the desired input port or vice versa. To remove an edge select it with the left click and hit **Delete**.


You can reconnect edges to other inputs by dragging the corresponding connectors.


![](edge_reconnect.gif)


### Port Adapters


Port **adapter** is a feature giving you the ability to select data components in an arbitrary order, combine and rearrange them, providing convenient access to elements and a lot of flexibility. It is available for the following data types:


- **bool**
- **float, float2, float3, float4**
- **int, int2, int3, int4**


When you drag a new edge to an input port, a number of available connection options shall appear:


- The = option provides the direct connection in the case the input type can provide all needed data components.
- Selecting another option creates an *[**Expression**](../../../content/materials/graph/node_library/misc/expression.md)* node accountable for type conversion.


![](swizzle.gif)


You can change the adapter later by double-clicking the expression and editing the field. The **Expression** node enables you to write simple arithmetic operations and even use the Unigine Graphic API.


### Adding New Nodes


In order to add a new node, right-click on the background or press **Space** and select a node type from the palette or type its name in the **Search** field to find it.


![](add_node.png)


Dragging an [edge](#node_edge) from an input port opens the node creation palette with a pre-set filter to the required data type for the corresponding port.


Textures can be dragged directly from the Asset Browser. In this case, a **[Sample Texture](../../../content/materials/graph/node_library/textures/sample_texture.md)** node with corresponding settings will be added automatically.


![](node_texture_drag.gif)


## Loops


Sometimes you need to perform certain actions multiple times, cloning the relevant groups of nodes will make your graph overcomplicated very quickly, even if only 10 iterations are required. In UNIGINE, you can create **loops** for that, just like in programming.


[![](loop_small.png)](loop.png)


To create a loop, add the **Loop Begin** and **Loop End** nodes and connect their **Loop** ports.


![](loop_create.png)


By double-clicking the *Loop Begin* node, you can open the Input Constructor enabling you to add, rearrange, rename, delete inputs (changing variables or other auxiliary values) and implicitly set their type as well as set the **maximum number of iterations**.


![](loop_input_constructor.gif)


Then, build a graph implementing the functionality of a single iteration, the result of which should be passed to the **Loop End** node for further iterations. You can use the result of all iterations further in your graph.


You can use the **Index** of the current iteration and the **Maximum Iterations** values in your logic. The *Index* starts with 0 and is equal to Maximum Iterations-1 at the last iteration.


Here's an example of a simple loop, incrementing a value by 0.1 10 times:


![](loop_example.png)


The **Loop End** node has the *break* input port that takes a boolean value, false by default. Passing a truth value (e.g., obtained via [Logical Nodes](../../../content/materials/graph/node_library/logical/index.md)) will interrupt the loop and exit the current iteration.


## Custom Code


No matter how advanced the materials system is, you might want something specific, maybe too complicated to implement via basic nodes. Or sometimes, it might be quicker to write several lines of code for mathematical operations instead of spawning a bunch of nodes and connecting them. The solution is simple � create a **Function** node and wrap any shader function into it. *Input* and *output* [ports](#node_port) for the node shall be automatically generated according to the function's signature.


![](custom_code.jpg)


To add or edit code to the node double-click on the node, the *Code Editor* window will open. You can write as many functions as you need, the last function in the code will be considered the main one.


## Portals


Sometimes, especially in complex material graphs, there are too many crisscrossing edges making the whole graph look like a spiderweb, and the data flow very hard to understand. A **portal** is a set of special nodes including a single *input* and one or more *outputs*, all having the same name. Portals serve to reduce the number of edges and make the graph more 'readable'.


![](portals.jpg)


To create a portal, start with adding a **[Portal In](../../../content/materials/graph/node_library/misc/portal_in.md)** node. Connect an input to the new node and double-click on it to adjust its color and name.


And then you can create as many **[Portal Out](../../../content/materials/graph/node_library/misc/portal_out.md)** nodes as you need. By double-clicking on a *Portal Out* node you can select the name of the desired input portal in case several portals are used.


Existing portals can be added by name via the *Create* menu.


![](add_portal.gif)


## Subgraphs


A **Subgraph** is a special type of material graph, which can be referenced from inside other material graphs. This can be very useful when the same operations are to be performed multiple times in a single graph or across multiple graphs. You simply pack these operations into a box with a set of **inputs** and **outputs** and then use this box anywhere you need. A Subgraph differs from a Material Graph in three main ways:


- A Subgraph does not generate any material, it is used as a building block in material graphs.
- A Subgraph does not have **Material** and **Final** nodes. Instead, it has two nodes called **Inputs** and **Outputs**, defining all input and output ports.
- A Subgraph is stored in a `*.msubgraph` asset.


![](subgraph.png)


Basically, the process of construction of a Subgraph is the same as when you create a Material Graph.


To create a new Subgraph, right-click in the Asset Browser to open the *Create* menu, then select ***Create Material** -> **Material Graph***.


![](create_subgraph.png)


Click **Save** to apply and save changes.


All subgraphs are automatically added to the palette, so if your start typing a name of such a subgraph in the search field of the [node creation palette](#add_node), it will be displayed in the list.


### Configuring Inputs and Outputs


Double click on the **Inputs** node or the **Outputs** node to open the constructor panel enabling you to add, rearrange, delete and set the name and type of input and output ports of the subgraph correspondingly.


![](subgraph_input_constructor.png)


By connecting nodes to the ports of the *Inputs* node, you specify the optional ports of the subgraph having default values.


### Using Subgraphs


To add a subgraph to your material graph currently opened in the Editor, simply find it by name in the [node creation palette](#add_node) or drag it from the *Asset Browser*, or you can add the **[Sub Graph](../../../content/materials/graph/node_library/misc/sub_graph.md)** node to your graph network, specify the `*.msubgraph` asset by double-clicking the node, and connect necessary edges to *input* and *output* ports of the subgraph.


![](add_subgraph.gif)


There is a set of core subgraphs implementing basic functionality (like **contrast, refract, object_triplanar**, etc.) stored in the `core/subgraphs` folder.
