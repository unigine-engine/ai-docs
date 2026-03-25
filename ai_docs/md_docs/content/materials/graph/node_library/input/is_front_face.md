# Is Front Face Node


![](../img/is_front_face.png)

### Description

Outputs a boolean value indicating which polygon face is surrently rendered, front (*True*) or back (*False*). You can pass this value to a [Branch](../../../../../content/materials/graph/node_library/logical/branch.md) node to change the look of your material for back faces of polygons. This functionality is available only when the **[Two Sided](../../../../../editor2/materials_settings/index.md#two_sided)** option is enabled for the material, otherwise backfaces of polygons simply won't be visible.


## Usage Example

| [**View Fullscreen**](https://matgraph.unigine.com/DocsIsFrontFace_2.21/fullView) |
|---|
