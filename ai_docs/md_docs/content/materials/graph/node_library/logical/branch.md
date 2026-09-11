# Branch Node


![](../img/branch.png)

### Description

This node provides a dynamic branch to the shader. If input Condition is true, the return output will be equal to input True, otherwise it will be equal to input False. This is determined per vertex or per pixel depending on shader stage.


The compilation mode of the branch can be selected with the Mode dropdown parameter (double-click somewhere inside the node to see the dropdown):


- **Flatten** � evaluate both sides of the branch and choose between the two resulting values. However, if the Condition receives a Constant as a value, one of the branches won't be used at all.
- **Branch (DirectX only)** � evaluate only one side of the branch depending on the given condition. Available only for DirectX Graphics API.
- **Auto** � the compiler auto selects the most appropriate mode.


## Usage Examples

**Example 1**


This example demonstrates how to paint the front (visible) and back faces of polygons in different colors using the Branch node, which sets the albedo color based on the value provided by the [Is Front Face](../../../../../content/materials/graph/node_library/input/is_front_face.md) node. This technique allows you to differentiate the appearance of your material on the front and back faces of polygons.


> **Notice:** This functionality is available only when the **[Two Sided](../../../../../editor2/materials_settings/index.md#two_sided)** option is enabled for the material. Otherwise, the back faces of polygons will not be visible.


| [**View Fullscreen**](https://matgraph.unigine.com/DocsBranch_2.21/fullView) |
|---|
