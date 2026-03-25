# Cubemap Texture Sample


These material graph samples demonstrate creation of materials applying custom cubemap textures for reflective and refractive materials.


![](result.jpg)


## Cubemap Reflection Sample


| [**View Fullscreen**](https://matgraph.unigine.com/SampleCubemapReflection_2.21/fullView) |
|---|


First, we get a reflection vector based on current *camera's view direction* vector and the *object's normal* vector, both in the world space. So, to the input ports of the **[Reflect](../../../../../content/materials/graph/node_library/misc/reflect.md)** node we connect outputs of the **[Vertex Normal](../../../../../content/materials/graph/node_library/input/vertex_normal.md)** node and the **[View Direction](../../../../../content/materials/graph/node_library/input/view_direction.md)** node (using the **-X|-Y|-Z** [port adapter](../../../../../content/materials/graph/index.md#adapter) to get the opposite direction, as incident vector is the opposite of the view vector).


Then, according to the obtained coordinates in the world space, the **[Sample Texture](../../../../../content/materials/graph/node_library/textures/sample_texture.md)** node obtains the pixel data from the cubemap (**[Texture Cube](../../../../../content/materials/graph/node_library/textures/texture_cube.md)** node), sampling a specified MIP-level provided by the **[Slider](../../../../../content/materials/graph/index.md#params)** parameter node (adjustable via the *Parameters* panel in UnigineEditor) to fake roughness of the surface. The color value is passed to the *Emissive* slot of the material.


The zero *Albedo* value (to preserve initial colors of the cubemap texture) is specified directly.


Finally, the data output is passed to the **[Final](../../../../../content/materials/graph/node_library/misc/final.md)** node.


## Cubemap Refraction Sample


| [**View Fullscreen**](https://matgraph.unigine.com/SampleCubemapRefraction_2.21/fullView) |
|---|


First, we get a refraction vector based on current *camera's view direction* vector and the *object's normal* vector, both in the world space. So, to the input ports of the **[Refract](../../../../../content/materials/graph/node_library/misc/refract.md)** node we connect the outputs of the **[Vertex Normal](../../../../../content/materials/graph/node_library/input/vertex_normal.md)** node and the **[View Direction](../../../../../content/materials/graph/node_library/input/view_direction.md)** node (using the **-X|-Y|-Z** [port adapter](../../../../../content/materials/graph/index.md#adapter) to get the opposite direction, as incident vector is the opposite of the view vector).


The *Refraction Index* is the ratio of indices of refraction of two environments, so we pass 1 (*IOR* of air) divided by the desired *IOR* value of our material.


Then, according to the obtained coordinates in the world space, the **[Sample Texture](../../../../../content/materials/graph/node_library/textures/sample_texture.md)** node obtains the pixel data from the cubemap (**[Texture Cube](../../../../../content/materials/graph/node_library/textures/texture_cube.md)** node), sampling a specified MIP-level provided by the **[Slider](../../../../../content/materials/graph/index.md#params)** parameter node (adjustable via the *Parameters* panel in UnigineEditor) to fake roughness of the surface. The first three components (x,y,z) of the color value are passed to the *Emissive* slot of the material.


The zero *Albedo* and *Roughness* values (to preserve initial colors of the cubemap texture) are specified directly.


Finally, the data output is passed to the **[Final](../../../../../content/materials/graph/node_library/misc/final.md)** node.
