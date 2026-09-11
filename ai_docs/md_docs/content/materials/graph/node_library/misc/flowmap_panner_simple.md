# Flowmap Panner Simple Node


![](../img/flowmap_panner_simple.png)

### Description

This node creates a flow effect for a source texture based on a flow map. Using this node, water or lava flowing in different directons can be created. The flow map can be [drawn in UNIGINE Editor](../../../../../editor2/texture_editor/flowmap_tool/index.md): the direction of flowing is set by the brush.


> **Notice:** When simulating a fast-flowing liquid (for example, a mountain stream), flickering may occur. In such case, it is recommended to use the **[Flowmap Panner](../../../../../content/materials/graph/node_library/misc/flowmap_panner.md)** node. Also this node is used if the custom sampling settings are required.


The workflow is as follows:


1. Using the flowmap texture, offset for UV coordinates is applied twice with a time shift.
2. Using 2 different UVs from the previous stage, source texture sampling is pefromed. In the result, 2 textures distorted over time according to the flowmap are created.
3. The created textures are blended (linear interpolation) using the time coefficient to make even and continuous distortion.


#### Ports

| Name | Description |  |
|---|---|---|
| ![](../img/types/texture.png) | **Source Texture** | Texture for which the flow effect will be created (albedo, normal, heightmap and so on). |
| ![](../img/types/texture.png) | **FlowMap Texture (0-1)** | Flowmap texture that stores values in range [0;1]. Note that: - It is recommended to use a 16-bit format. However, a 8-bit format can be used as well: simply choose the *[Normal](../../../../../editor2/assets_workflow/texture_import.md#texture_preset)* preset when importing the texture. - Only the R and G texture channels are used as they store coordinates of the direction vector. - [Mipmaps SRGB correction](../../../../../editor2/assets_workflow/texture_import.md) must be disabled on texture importing. |
| ![](../img/types/float2.png) | **Source UV** | UV channel for the source texture. |
| ![](../img/types/float2.png) | **Source Tiling** | Source texture tiling. |
| ![](../img/types/float2.png) | **FlowMap UV** | UV channel for the flowmap texture. |
| ![](../img/types/float2.png) | **FlowMap Tiling** | Flowmap texture tiling |
| ![](../img/types/float2.png) | **Phase 2 UV Offset** | Offset of the final UV coordinates for the second texture. Using this value you can reduce repeatability of the pattern (if any). The default value is (0.5, 0.5). |
| ![](../img/types/float.png) | **Speed** | Panner speed. |
| ![](../img/types/float.png) | **Strength** | Intesity of texture distortion. |
| ![](../img/types/float.png) | **Normal Intensity** | Intensity of normals (if a normal texture is passed as a source texture to the subgraph). Texture sampling is performed in the subgraph, however, the normal intensity is set up in the **[Sample Texture](../../../../../content/materials/graph/node_library/textures/sample_texture.md)** node, so it is specified separately. |
| ![](../img/types/float4.png) | **Color** | Color data of the texture resulting from blending textures. |
| ![](../img/types/float3.png) | **Normal (Tangent Space)** | Normals of the texture resulting from blending normal textures. |
