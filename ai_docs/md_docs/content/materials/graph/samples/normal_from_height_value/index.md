# Normal From Height Value Sample


| [**View Fullscreen**](https://matgraph.unigine.com/SampleNormalFromHeightValue_2.21/fullView) |
|---|


This material graph sample demonstrates how to convert height values to normal vectors.


The **[Normal From Height Value](../../../../../content/materials/graph/node_library/misc/normal_from_height_value.md)** node is accountable for conversion from a height value to normals.


In this sample, a *noise* texture is used as a mask adjustable via the *Coverage* and *Contrast* parameters. The black-and-white mask is used as a blending coefficient for the **[Lerp](../../../../../content/materials/graph/node_library/math/lerp.md)** node that performs linear interpolation between two normal maps and as the source height for the **Normal From Height Value** node converting the mask to a normal map.


Finally, the result of two blended normal maps is added as the *Detail Normal* to the edge normals via the **[Reorient Normal Blend](../../../../../content/materials/graph/node_library/misc/reorient_normal_blend.md)** node and the resulting tangent-space normal vector is passed to the material.


The *Albedo* color is obtained from the corresponding parameter.


![](result.jpg)

*Normal From Height Value sample*
