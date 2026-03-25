# Blackbody Sample


![](result.jpg)

*Blackbody sample*


These material graph samples demonstrate how to implement simulation of black-body radiation for physically accurate emissive materials. Two material graphs are included.


| [**View Fullscreen**](https://matgraph.unigine.com/SampleBlackbodyBox_2.21/fullView) |
|---|


The `blackbody_box` material showcases the change of color based on the temperature on a box.


The horizontal component of UV coordinates taken via the **x** [port adapter](../../../../../content/materials/graph/index.md#adapter) from the **[Vertex UV 0](../../../../../content/materials/graph/node_library/input/vertex_uv_0.md)** node is multiplied by the **Temperature** value (in Kelvin) provided by the **[Slider](../../../../../content/materials/graph/index.md#params)** parameter node (enabling you to adjust the maximum temperature in the *Parameters* panel). Thus the changing temperature values are mapped horizontally on the box faces.


Then, we simply pass the temperature to the **[Blackbody](../../../../../content/materials/graph/node_library/misc/blackbody.md)** node to get the corresponding color.


Additionally, the source temperature in the [0; 1000] range is remapped (the **[Rerange](../../../../../content/materials/graph/node_library/math/rerange.md)** node) to the [0; 1] range and multiplied by the **U** texture coordinate and the color is [multiplied](../../../../../content/materials/graph/node_library/math/multiply.md) by the [saturated](../../../../../content/materials/graph/node_library/math/saturate.md) result preventing cold parts from being red.


Finally, the resulting sRGB color is to be converted to RGB values via the **[SRGB Inverse](../../../../../content/materials/graph/node_library/misc/srgb_inverse.md)** node and passed to the material's *Emissive* port.


*Albedo* and *Specular* values are specified directly using the **[Float](../../../../../content/materials/graph/node_library/input/float.md)** nodes.


| [**View Fullscreen**](https://matgraph.unigine.com/SampleBlackbodyRifle_2.21/fullView) |
|---|


The `blackbody_rifle` material graph contains a ready-to-use implementation of blackbody-based emission of hot parts of an object.


Temperature-based colorization is applied the same way as in the previous sample, but this time [vertex positions](../../../../../content/materials/graph/node_library/input/vertex_position.md) in the object space are used to define the hot parts. The y component of the **[Vertex Position](../../../../../content/materials/graph/node_library/input/vertex_position.md)** node is adjusted via the **[Contrast](../../../../../content/materials/graph/node_library/misc/contrast.md)** node to make a sharper transition along the Y axis.


And the resulting mask multiplied by the Temperature parameter is used in the familiar network implementing the blackbody emission.


*Albedo, Metalness* and *Roughness* values are obtained from the corresponding textures via the **[Sample Texture](../../../../../content/materials/graph/node_library/textures/sample_texture.md)** nodes and multiplied by the corresponding intensity parameters. The *Specular* value is specified directly using the **[Float](../../../../../content/materials/graph/node_library/input/float.md)** nodes.
