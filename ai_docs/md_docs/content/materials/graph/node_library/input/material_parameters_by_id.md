# Material Parameters by ID Node


![](../img/material_parameters_by_id.png)

### Description

Reads the [custom parameters](../../../../../content/materials/custom_parameters/reading_parameters.md) of the material with a given Material ID. It is the same node as [Material Parameters](../../../../../content/materials/graph/node_library/input/material_parameters.md), except that the ID comes from an input port instead of a Surface ID Buffer.


In a post-effect graph the input has to be connected - take the ID from the *Material ID* output of the [Surface Parameters](../../../../../content/materials/graph/node_library/input/surface_parameters.md) node. In any other graph the input may be left unconnected, and the node then reads the parameters of the material being shaded.


#### Ports

| Name | Description |  |
|---|---|---|
| ![](../img/types/int.png) | **Material ID** | ID of the material to read. |
| ![](../img/types/int.png) | **Material Mask** | The classic [material mask](../../../../../principles/bit_masking/index.md#material_mask) of the material. |
| ![](../img/types/int.png) | **Screen-Space Shadows** | Feature bit: [screen-space shadows](../../../../../editor2/settings/render_settings/shadows/index.md#screen_space_shadows) are enabled for the material. |
| ![](../img/types/int.png) | **Shoreline Wetness** | Feature bit: [shoreline wetness](../../../../../editor2/settings/render_settings/water_ssr/index.md#water_shoreline_wetness) is enabled for the material. |
| ![](../img/types/int.png) | **Motion Blur** | Feature bit: [motion blur](../../../../../editor2/settings/render_settings/camera_effects/index.md#motion_blur) is enabled for the material. |
| ![](../img/types/int.png) | **SSAO** | Feature bit: [SSAO](../../../../../editor2/settings/render_settings/global_illumination/indirect_diffuse/ssao/index.md) is enabled for the material. |
| ![](../img/types/int.png) | **SSR** | Feature bit: [SSR](../../../../../editor2/settings/render_settings/ssr/index.md) is enabled for the material. |
| ![](../img/types/int.png) | **SSS** | Feature bit: [SSS](../../../../../editor2/settings/render_settings/sss/index.md) is enabled for the material. |
| ![](../img/types/int.png) | **DOF** | Feature bit: [depth of field](../../../../../editor2/settings/render_settings/camera_effects/index.md#dof) is enabled for the material. |
