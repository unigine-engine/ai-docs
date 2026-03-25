# Rotate Space Node


![](../img/rotate_space.png)

### Description

This node is used to transform a **DIRECTION** vector from one space (*World, Object, Tangent, View*) to another space.


Suppose you have a vector in *Object* space and you want to use it where the same vector is required but in a different space - *Tangent*, for example. You can use this node to switch to the required space.


> **Notice:** Double-click somewhere within a node to change initial (*From*) and target (*To*) space.


## Usage Examples

**Rotate Space within Vertex Animation**

[![](../img/../../../../samples/material_examples/vertex_animation.gif)](../img/../../../../samples/material_examples/vertex_animation.gif)


In the **[Vertex Animation Sample](../../../../../content/materials/graph/samples/vertex_animation/index.md)**, the animation is baked into a texture, and the normals are stored in **object space** (a `.tga` texture with normals). To properly blend them with another normal map, the **object space** normals must first be transformed into **tangent space**.


Since the material is set up to use **object space** normals, the blended result is then converted back to **object space** after the mixing process using the **Rotate Space** node again.


| [**View Fullscreen**](https://matgraph.unigine.com/SampleVertexAnimation_2.21/fullView) |
|---|


**Rotate Space for View-Facing Projection**


In this example, the vector **(0, 0, 1)** in **tangent space** represents the surface normal. When transformed into **view space**, it indicates the direction the surface is facing relative to the camera.


Using this transformed vector as UV coordinates results in a projection aligned to the camera view. As a result, the texture appears to follow the camera orientation, effectively creating a view-facing projection.


| [**View Fullscreen**](https://matgraph.unigine.com/DocsRotateSpace_2.21/fullView) |
|---|
