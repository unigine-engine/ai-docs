# Texture Resolution Node


![](../img/texture_resolution.png)

### Description

This node takes an input Texture and outputs its Width and Height, is case a [3D Texure](../../../../../content/materials/graph/node_library/textures/texture_3d.md) or a [2D Texture Array](../../../../../content/materials/graph/node_library/textures/texture_2d_array.md) is connected to the input the node shall also output Depth or the number of Layers.


## Usage Examples

**Example 1**


If you want to make a 1-texel UV offset you should know the size of this texel relative to UV, which can be obtained by dividing UV by texture resolution provided by this node.
