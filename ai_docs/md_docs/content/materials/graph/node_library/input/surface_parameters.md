# Surface Parameters Node


![](../img/surface_parameters.png)

### Description

Reads the [custom parameters](../../../../../content/materials/custom_parameters/reading_parameters.md) of the surface drawn at a pixel. The node samples a Surface ID Buffer, finds the block that ID belongs to, and gives every value in it an output port of its own.


The caption follows the buffer selected in the *Type* property, so a node reads *Scene Surface Parameters*, *Opaque Surface Parameters* and so on. A freshly created node reads the Scene Buffer.


Custom parameters have to be [declared](../../../../../content/materials/custom_parameters/declaring_and_setting_cpp.md#declare) for the ports to appear: the node is rebuilt from the current layout, and a node in an open graph picks up a new parameter as soon as the declaration is saved.


## Parameters

| #### Type |
|---|
| The Surface ID Buffer to read. Double-click the node to open the property. One of the following options:: - **Scene** - the composed Scene Buffer - every category stacked into one. Works whatever the Multilayered setting is, which is why it is the default. - **Opaque** - the Surface ID plane of the G-buffer, written by opaque geometry. - **Transparent** - the Transparent Buffer. It exists only while Multilayered is enabled. - **Decal** - the Decal Buffer. It is allocated in either mode, and holds an ID only for decals with Write Surface ID enabled. - **Water** - the Water Buffer. It exists only while Multilayered is enabled. |

#### Ports

| Name | Description |  |
|---|---|---|
| ![](../img/types/int2.png) | **Screen Position** | Pixel coordinates to read the buffer at. Left unconnected, the node reads the pixel being shaded. |
| ![](../img/types/int.png) | **Node ID** | ID of the node the surface belongs to. |
| ![](../img/types/int.png) | **Surface** | Number of the surface within that node. This is not the Surface ID, which is never exposed as a port. |
| ![](../img/types/int.png) | **Instance** | Number of the instance for a [Mesh Cluster](../../../../../objects/objects/mesh_cluster/index.md), whose instances carry values of their own. |
| ![](../img/types/int.png) | **Material ID** | ID of the material assigned to the surface. Feed it to the [Material Parameters by ID](../../../../../content/materials/graph/node_library/input/material_parameters_by_id.md) node to reach the values of that material. |
| ![](../img/types/int.png) | **Light Map** | Feature bit: the surface is lit by a [lightmap](../../../../../editor2/lighting/gi/lightmaps.md). |
