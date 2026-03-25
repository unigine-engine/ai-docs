# Fresnel Effect Sample


| [**View Fullscreen**](https://matgraph.unigine.com/SampleFresnelEffect_2.21/fullView) |
|---|


This material graph sample demonstrates how to implement the Fresnel effect with respect to a normal map used when creating materials.


The data from the *Albedo* texture is sampled (in accordance with the *default UV*) by the **[Sample Texture](../../../../../content/materials/graph/node_library/textures/sample_texture.md)** node connected to the **Albedo** port of the master material node.


The tangent-space normal data taken from the **Normal** texture is passed to the **[Fresnel](../../../../../content/materials/graph/node_library/misc/fresnel.md)** node accountable for the effect intensity, the effect power is controlled by the **Power [Slider](../../../../../content/materials/graph/node_library/input/float.md)** parameter node. Thus the Fresnel effect is based on data from the normal map and not the vertex normals.


The output [multiplied](../../../../../content/materials/graph/node_library/math/multiply.md) by the color from the **[Color](../../../../../content/materials/graph/node_library/input/color_float3.md)** parameter node (enabling you to adjust a color value via the *Parameters* panel in UnigineEditor) is plugged into the **Emission** port of the material. Thus the emission color is applied only in the areas where the fresnel effect takes place.


![](result.jpg)

*The result*
