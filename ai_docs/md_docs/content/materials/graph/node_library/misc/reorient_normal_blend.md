# Reorient Normal Blend Node


![](../img/reorient_normal_blend.png)

### Description

This node is used for blending normals while preserving their correct orientation. It ensures that two normals are properly combined and remain correctly applied to a mesh.


**Functionality**


**Inputs:**


- **Base Normal** **(float3)** � The base layer of normals, which can come from either geometry vertex normals or a normal map texture.
- **Detail Normal** **(float3)** � The secondary normal map to be blended with the base normal, adding supplementary surface details.


**Output:**


- **Blended Normal** **(float3)** � The resulting normal vector after correctly reorienting and blending the two input normal maps, ensuring a properly oriented final normal.


## Usage Examples

**Blending Two Normal Maps**

[![](../img/reorient_normal_blend_ex_1.png)](../img/reorient_normal_blend_ex_1.png)


Let's take an object that already has a normal map applied and add another one to introduce additional surface details. Directly combining two normal maps without reorienting their vectors might lead to incorrect shading, or an unnatural lighting response.


To avoid this, use the **Reorient Normal Blend** node, which ensures the additional normal map correctly conforms to the base normal, preserving accurate shading and surface details.


| Original normal map | Two maps (***[Add](../../../../../content/materials/graph/node_library/math/add.md)*** node) | Two maps (Reorient Normal Blend node) |
|---|---|---|
| ![](../img/reorient_normal_blend_ex_2.png) | ![](../img/reorient_normal_blend_ex_3.png) | ![](../img/reorient_normal_blend_ex_4.png) |


| [**View Fullscreen**](https://matgraph.unigine.com/DocsReorientNormalBlend_2.21/fullView) |
|---|
