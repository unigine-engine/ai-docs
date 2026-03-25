# Vertex UV 1 Node


![](../img/vertex_uv_1.png)

### Description

This node retrieves *the second set of UV coordinates* from a mesh's vertex data, defining how textures are wrapped around a 3D model and positioned on the mesh. The **Vertex UV 1** node is used for sampling textures, for example albedo, normal textures, baked lighting, damage or dirt masks. It is commonly utilized for additional secondary texture layers such as detail maps, decals, or lightmaps.


The **Vertex UV 1** node outputs a **float2** value representing the UV coordinates stored in the second UV channel.


Use the ***[Vertex UV 0](../../../../../content/materials/graph/node_library/input/vertex_uv_0.md)*** node to access *the first UV set of the UV coordinates*.


## Usage Examples

**Creating A Brick Wall With Patches Of Dirt**

[![](../img/vertex_uv_1_ex_1.png)](../img/vertex_uv_1_ex_1.png)


Let's create a brick wall with certain areas covered in dirt.


1. First, unwrap the mesh in a 3D editor, ensuring it has *two UV sets* - one for the brick texture (albedo) and another for the dirt overlay.
2. Import the mesh into the editor.
3. Use ***[Vertex UV 0](../../../../../content/materials/graph/node_library/input/vertex_uv_0.md)*** node to map the main brick texture and **Vertex UV 1** for the dirt texture.
4. Blend them, using the ***[Lerp](../../../../../content/materials/graph/node_library/math/lerp.md)*** (linear interpolation) node with the dirt texture's Alpha channel as the blending coefficient.


This setup allows the dirt to appear only in specific areas while preserving the brick texture underneath.


| [**View Fullscreen**](https://matgraph.unigine.com/DocsVertexUV1_2.21/fullView) |
|---|
