# Ceiling Node


![](../img/ceiling.png)

### Description

Outputs the smallest integer value, or whole number, that is greater than or equal to the input value.


For example:


- Ceiling(4,2) = 5
- Ceiling(-2,5) = -2


## Usage Examples

**Flipbook Animation**


This material graph implements a **flipbook** for atlas-based texture animation, using the **Ceiling** node as a key component to control frame stepping over time.


![Step function formula](../../node_library/img/floor_ex.gif)


The animation is driven by the **[Time](../../../../../content/materials/graph/node_library/misc/time.md)** node, which is multiplied by a custom *FPS* value to control the animation speed. The **Ceiling** node is then used to ensure that only whole-number frame indices are used � this prevents interpolation and ensures the texture only changes at discrete intervals, creating a clean frame-by-frame animation effect.


That frame index is then wrapped using **[Mod](../../../../../content/materials/graph/node_library/math/mod.md)** (for looping) and separated into *column* and *row* indices based on the texture atlas layout. These indices are then converted into UV offsets and combined with tiling data using the **[Tiling And Offset](../../../../../content/materials/graph/node_library/misc/tiling_and_offset.md)** node, which then passed into the **[Sample Texture](../../../../../content/materials/graph/node_library/textures/sample_texture.md)** node as a new UV.


| [**View Fullscreen**](https://matgraph.unigine.com/DocsCeiling_2.21/fullView) |
|---|
