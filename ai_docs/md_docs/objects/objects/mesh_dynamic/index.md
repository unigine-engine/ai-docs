# Dynamic Mesh


A ![](dynamic.png) � **dynamic mesh** is an object that represents a collection of vertices, edges and triangular faces (organized in polygons) defining the object's geometry that can be modified procedurally. It has all the static meshes' shader functionalities, so you can load an existing static mesh as a dynamic one in order to modify it.


It is usually used to modify the mesh instance because of interaction (impact, shot, tear-out, etc.) or, for example, to create dynamic changing surface: cloth, rope, wire, liquid and so on.


![](dynamic_1.png)


Dynamic meshes can be procedurally created by using Unigine or third-party plugin or library.


The **mesh limitations** set in UNIGINE:


| Maximum number of **vertices** per mesh | 4,294,967,295 |
|---|---|
| Maximum number of **surfaces** per mesh | 32,768 |


### See Also


- *[ObjectMeshDynamic](../../../api/library/objects/class.objectmeshdynamic_cpp.md)* class to edit the *dynamic mesh* via API
- A set of samples located in the `data/samples/objects/` directory:

  - [`dynamic_00`](../../../code/uniginescript/samples/objects/dynamic_00.md)
  - [`dynamic_01`](../../../code/uniginescript/samples/objects/dynamic_01.md)
  - [`dynamic_02`](../../../code/uniginescript/samples/objects/dynamic_02.md)
  - [`dynamic_03`](../../../code/uniginescript/samples/objects/dynamic_03.md)
  - [`dynamic_04`](../../../code/uniginescript/samples/objects/dynamic_04.md)
  - [`dynamic_05`](../../../code/uniginescript/samples/objects/dynamic_05.md)


## Adding a Dynamic Mesh


To add a *dynamic mesh* to the scene via UnigineEditor do the following:


1. [Run](../../../editor2/index.md#run) UnigineEditor.
2. On the Menu bar, click *Create -> Mesh -> Dynamic*. ![](dynamic_create.png)
3. In the dialog window that opens, choose the path to the `.mesh` file.
4. Place the mesh somewhere in the world.


> **Notice:** You can change the path to the mesh at any time in the *MeshDynamic* tab.
