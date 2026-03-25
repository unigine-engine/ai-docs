# Parallax Simple Node


![](../img/parallax_simple.png)

### Description

This node calculates the offsetted UV with a parallax effect for a certain UV channel.


- UV - input UV to which the parallax effect is to be applied.
- Height Texture - heightmap texture, where R channel stores concavity values. Black - maximum concavity, white - no parallax effect is applied.
- Height - height value (in meters) to which the surface is to be deepened visually if the corresponding texel of the heightmap is black.


## Usage Examples

**Example 1**

[![](../img/parallax_simple_ex_1.png)](../img/parallax_simple_ex_1.png)


The graph illustrates the material for creating a cobblestone pathway.


If you need a more flexible effect (more layers, noise adjustment, UV tiling and offset), use the [Parallax Occlusion Mapping](../../../../../content/materials/graph/node_library/misc/parallax_occlusion_mapping.md) node, but in most cases Parallax Simple node is enough.


| [**View Fullscreen**](https://matgraph.unigine.com/DocsParallaxSimple_2.21/fullView) |
|---|
