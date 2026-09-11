# Material Parameters Node


![](../img/material_parameters.png)

### Description

Reads the [custom parameters](../../../../../content/materials/custom_parameters/reading_parameters.md) of the material assigned to the surface drawn at a pixel. The node samples a Surface ID Buffer, takes the Material ID stored in the surface block, and gives every value of that material an output port of its own.


The caption follows the buffer selected in the *Type* property, so a node reads *Scene Material Parameters*, *Opaque Material Parameters* and so on. A freshly created node reads the Scene Buffer.


These are the values shared by every surface the material is assigned to. Values that differ between surfaces are read with the [Surface Parameters](../../../../../content/materials/graph/node_library/input/surface_parameters.md) node instead.


## Parameters

| #### Type |
|---|
| The Surface ID Buffer to read. Double-click the node to open the property. One of the following options:: - **Scene** - the composed Scene Buffer - every category stacked into one. Works whatever the Multilayered setting is, which is why it is the default. - **Opaque** - the Surface ID plane of the G-buffer, written by opaque geometry. - **Transparent** - the Transparent Buffer. It exists only while Multilayered is enabled. - **Decal** - the Decal Buffer. It is allocated in either mode, and holds an ID only for decals with Write Surface ID enabled. - **Water** - the Water Buffer. It exists only while Multilayered is enabled. |

#### Ports

| Name | Description |  |
|---|---|---|
| ![](../img/types/int2.png) | **Screen Position** | Pixel coordinates to read the buffer at. Left unconnected, the node reads the pixel being shaded. |
| ![](../img/types/int.png) | **Material ID** | ID of the material. It is allocated when the material is registered and stays with it until it is unloaded. |
| ![](../img/types/int.png) | **Material Mask** | The classic [material mask](../../../../../principles/bit_masking/index.md#material_mask) of the material. |
| ![](../img/types/int.png) | **Screen-Space Shadows** | Feature bit: [screen-space shadows](../../../../../editor2/settings/render_settings/shadows/index.md#screen_space_shadows) are enabled for the material. |
| ![](../img/types/int.png) | **Shoreline Wetness** | Feature bit: [shoreline wetness](../../../../../editor2/settings/render_settings/water_ssr/index.md#water_shoreline_wetness) is enabled for the material. |
| ![](../img/types/int.png) | **Motion Blur** | Feature bit: [motion blur](../../../../../editor2/settings/render_settings/camera_effects/index.md#motion_blur) is enabled for the material. |
| ![](../img/types/int.png) | **SSAO** | Feature bit: [SSAO](../../../../../editor2/settings/render_settings/global_illumination/indirect_diffuse/ssao/index.md) is enabled for the material. |
| ![](../img/types/int.png) | **SSR** | Feature bit: [SSR](../../../../../editor2/settings/render_settings/ssr/index.md) is enabled for the material. |
| ![](../img/types/int.png) | **SSS** | Feature bit: [SSS](../../../../../editor2/settings/render_settings/sss/index.md) is enabled for the material. |
| ![](../img/types/int.png) | **DOF** | Feature bit: [depth of field](../../../../../editor2/settings/render_settings/camera_effects/index.md#dof) is enabled for the material. |
