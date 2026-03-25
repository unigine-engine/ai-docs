# Material Node


![](../img/material.png)

### Description

Generates a material. The set of input ports and supported features, as well as the type of the generated material, depends on the current [Common Settings](../../../../../content/materials/graph/index.md#common_settings).


> **Notice:** A material graph can contain several **Material** nodes, but only the one connected to the **[Final](../../../../../content/materials/graph/node_library/misc/final.md)** node will be used.


#### Ports

| Name | Description |  |
|---|---|---|
| ![](../img/types/float.png) | **Opacity** | Opacity value: - 0 corresponds to a transparent fragment. - 1 corresponds to a fully opaque fragment. |
| ![](../img/types/float.png) | **Opacity Clip Threshold** | Alpha-test opacity threshold value. |
| ![](../img/types/float3.png) | **Albedo** | RGB [albedo](../../../../../content/materials/library/mesh_base/index.md#parameter_albedo) value. |
| ![](../img/types/float.png) | **Opacity (Albedo)** | Albedo intensity multiplier for *Decal PBR* materials. |
| ![](../img/types/float3.png) | **Color** | RGB fragment color value (for *Mesh Transparent Unlit* materials). |
| ![](../img/types/float.png) | **Metalness** | [Metalness](../../../../../content/materials/library/mesh_base/index.md#parameter_metalness) value. |
| ![](../img/types/float.png) | **Roughness** | [Roughness](../../../../../content/materials/library/mesh_base/index.md#parameter_roughness) value. |
| ![](../img/types/float.png) | **Specular** | [Specular](../../../../../content/materials/library/mesh_base/index.md#specular_color) value. |
| ![](../img/types/float.png) | **Microfiber** | [Microfiber](../../../../../content/materials/library/mesh_base/index.md#microfiber_parameter) value. |
| ![](../img/types/float3.png) | **Normal** | Normal vectors data. The **[Normal Space](../../../../../content/materials/graph/index.md#normal_space)** setting defines how the normal data is treated. |
| ![](../img/types/float.png) | **Translucent** | [Translucency](../../../../../content/materials/library/mesh_base/index.md#parameter_translucency) value. |
| ![](../img/types/float.png) | **Opacity (Metalness, Specular, Translucent)** | Metalness, Specular, and Translucent intensity multiplier for *Decal PBR* materials. |
| ![](../img/types/float.png) | **Opacity (Roughness, Microfiber)** | Roughness and Microfiber intensity multiplier for *Decal PBR* materials. |
| ![](../img/types/float.png) | **Opacity (Normal)** | Normal intensity multiplier for *Decal PBR* materials. |
| ![](../img/types/float.png) | **Ambient Occlusion** | [Ambient occlusion](../../../../../content/materials/library/mesh_base/index.md#option_ao) value. |
| ![](../img/types/float3.png) | **Emissive** | RGB [emission](../../../../../content/materials/library/mesh_base/index.md#option_emission) value. |
| ![](../img/types/float2.png) | **Velocity** | Velocity vectors defining screen-space pixel offset. |
| ![](../img/types/float4.png) | **Auxiliary** | RGBA [auxiliary](../../../../../content/materials/library/mesh_base/index.md#option_auxiliary) value. |
| ![](../img/types/float.png) | **Auxiliary Clip Threshold** | Opacity threshold value for auxiliary clipping. |
| ![](../img/types/float.png) | **Opacity (Auxiliary)** | Auxiliary intensity multiplier for *Decal PBR* materials. |
| ![](../img/types/float.png) | **Blur** | [Transparent blur](../../../../../content/materials/library/mesh_base/index.md#transparent_blur) value. |
| ![](../img/types/float2.png) | **Refraction Screen UV Offset** | [Refraction](../../../../../content/materials/library/mesh_base/index.md#option_refraction) screen-space offset of screen UV coordinates. |
| ![](../img/types/float.png) | **Depth (Offset)** | Custom depth / depth offset value (distance from the camera in the view space), in units. |
| ![](../img/types/float3.png) | **Vertex Position / Offset** | Vertex adjustment data. The [**Vertex Mode**](../../../../../content/materials/graph/index.md#vertex_mode) and [**Vertex Positions Space**](../../../../../content/materials/graph/index.md#vertex_space) settings define the vector space and how the data is treated. > **Notice:** All logic connected to this port is performed on the vertex shader stage. If this port receives any input, an additional option ***Bound Mode*** becomes available in the material's *Base Options*. This option allows configuring the [object bounds](../../../../../principles/world_management/index.md#material_bounds) to take the vertex shift into account. |
| ![](../img/types/float.png) | **Tessellation Factor** | [Tessellation density factor](../../../../../content/materials/library/mesh_base/index.md#tessellation_density_factor). |
| ![](../img/types/float3.png) | **Tessellation Vertex Offset / Position** | Position of tessellated vertices. The [**Vertex Mode**](../../../../../content/materials/graph/index.md#vertex_mode) and [**Vertex Positions Space**](../../../../../content/materials/graph/index.md#vertex_space) settings define the vector space and how the data is treated. |
| ![](../img/types/float.png) | **PostEffects Clip Threshold** | Opacity threshold value for post effects clipping. |
| ![](../img/types/float.png) | **Shadow Clip Threshold** | Opacity threshold value for shadows clipping. |
| ![](../img/types/undefined.png) | **Material** | Material for the **[Final](../../../../../content/materials/graph/node_library/misc/final.md)** node. |
