# Procedural Tiles Sample


| [**View Fullscreen**](https://matgraph.unigine.com/SampleProceduralTiles_2.21/fullView) |
|---|


This material graph sample demonstrates how to create a procedurally damaged tiled material with two layers.


The material graph performs blending of two sets of textures (*background* and *tiles*) by using a set of mask textures and the *damage_level* slider controlling the transition. The **[Parallax Simple](../../../../../content/materials/graph/node_library/misc/parallax_simple.md)** and **[Normal From Height Value](../../../../../content/materials/graph/node_library/misc/normal_from_height_value.md)** nodes are used for additional bumping for the overlaying textures.


![](../../../../samples/material_examples/procedural_tiles.gif)

*The result*
