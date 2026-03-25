# Dissolve Sample


| [**View Fullscreen**](https://matgraph.unigine.com/SampleDissolve_2.21/fullView) |
|---|


This material graph sample demonstrates how to create an Alpha Test material with a dissolve effect.


The effect is achieved by sampling data from the *noise_m* noise texture and shifting its values via a [slider](../../../../../content/materials/graph/node_library/input/float.md) parameter. The sharp black-white mask is obtained via the **[Step](../../../../../content/materials/graph/node_library/math/step.md)** node, the output of which is connected to the *Opacity* input of the **[Material](../../../../../content/materials/graph/node_library/misc/material.md)** node. The *Opacity Clip Threshold* is set in the middle of the range via a **[Float](../../../../../content/materials/graph/node_library/input/float.md)** node.


The mask with some *border_width* offset is also treated as a mask for material's *Emission*.


![](../../../../samples/material_examples/dissolve.gif)

*The result*
