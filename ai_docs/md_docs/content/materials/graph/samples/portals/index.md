# Portals Sample


| [**View Fullscreen**](https://matgraph.unigine.com/SamplePortals_2.21/fullView) |
|---|


This material graph sample demonstrates how to use [portals](../../../../../content/materials/graph/index.md#node_portal) in your materials.


Two colors (*A* and *B*) are blended by the **[Lerp](../../../../../content/materials/graph/node_library/math/lerp.md)** node controlled by the coefficient provided by the **[Slider](../../../../../content/materials/graph/index.md#params)** parameter node (enabling you to adjust float values via the *Parameters* panel in UnigineEditor).


Both colors and the control slider are connected to the corresponding ports of the **Lerp** node via portals (*Color A*, *Color B*, and *Lerp Slider*). The result is connected to the *Albedo* input of the **[Material](../../../../../content/materials/graph/node_library/misc/material.md)** node.
