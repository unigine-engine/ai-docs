# Fade By Depth Sample


| [**View Fullscreen**](https://matgraph.unigine.com/SampleFadeByDepth_2.21/fullView) |
|---|


This material graph sample demonstrates how to implement an effect of fading by depth.


The *Mesh Transparent PBR* material has white *albedo* color and the *emission* color controlled via the *Parameters* panel, the resulting appearance is controlled by *opacity*.


Resulting *Opacity* is defined by the combination of:


- the Fresnel effect (glow in the areas along the edges). Here we find the angle between the mesh�s surface [normal](../../../../../content/materials/graph/node_library/input/vertex_normal.md) and [view direction](../../../../../content/materials/graph/node_library/input/view_direction.md) using the **[Dot Product](../../../../../content/materials/graph/node_library/math/dot_product.md)** node, which looks like a �glow� around the edge of the object. We can increase the *Fresnel Power* input to make this glow thinner and closer to the edges.
- data on intersected geometry of the scene (shield contours shall be projected onto intersected geometry). Here we�ll handle the intersection effect with scene geometry.  Via the **[Texture Buffer Depth Opacity](../../../../../content/materials/graph/node_library/textures/texture_buffer_depth_opacity.md)** node we get Scene Depth and subtract the object's depth (the distance to the **[Vertex Position](../../../../../content/materials/graph/node_library/input/vertex_position.md)** in the view space), then we [saturate](../../../../../content/materials/graph/node_library/math/saturate.md) the result in the **[0.0f; 1.0f]** range and [subtract](../../../../../content/materials/graph/node_library/math/subtract.md) it from 1 to get an inverse intensity. This gives us values close to 1 in the area of intersection with the geometry of other objects. At this point we can add a **[Power](../../../../../content/materials/graph/node_library/math/power.md)** node to be able to control the intensity using a value provided by a **[Slider](../../../../../content/materials/graph/index.md#params)** node (enabling you to adjust float values via the *Parameters* panel in UnigineEditor).


Both these components are [added](../../../../../content/materials/graph/node_library/math/add.md) together and [saturated](../../../../../content/materials/graph/node_library/math/saturate.md).


![](result.jpg)

*The result*
