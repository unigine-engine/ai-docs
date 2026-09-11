# Static Mesh


A ![](mesh.png) �**static mesh** is an object that represents a collection of vertices, edges and triangular faces (organized in polygons) defining the object's geometry. The static mesh can be moved, rotated and scaled, but cannot be modified: vertices of the static mesh are immutable.


Static meshes are usually used to add non-animated geometry: buildings, furniture, vehicles, and so on.


![](static_1.png)


Static meshes consist of groups of polygons that are called **surfaces**. Each surface requires a separate draw call to the GPU. To render a surface, the material should be assigned to it. Each surface has 2 UV channels. Read more about surfaces and materials [here](../../../principles/world_structure/index.md#objects).


Static meshes are created in the third-party graphics programs (such as *3ds Max, Maya*, etc.) and can be [imported](../../../editor2/assets_workflow/assets_create_import.md) via UnigineEditor and converted to the UNIGINE native format (`.mesh`). In UNIGINE meshes have a float precision. That is why it is highly recommended to export meshes from third-party graphic programs near the origin and then place the mesh in UnigineEditor.


The **mesh limitations** set in UNIGINE:


| Maximum number of **vertices** per mesh | 4,294,967,295 |
|---|---|
| Maximum number of **surfaces** per mesh | 32,768 |


### See Also


- The *[ObjectMeshStatic](../../../api/library/objects/class.objectmeshstatic_cpp.md)* class to edit static meshes via API
- A set of samples located in the `data/samples/objects/` folder:

  - [`mesh_00`](../../../code/uniginescript/samples/objects/mesh_01.md)
  - [`mesh_01`](../../../code/uniginescript/samples/objects/mesh_02.md)


## Adding a Static Mesh


To add a static mesh to the scene via UnigineEditor do the following:


1. [Run](../../../editor2/index.md#run) UnigineEditor.
2. On the Menu bar, click **Create* -> *Mesh* -> *Static**. ![](static_create.png)
3. In the dialog window that opens, choose the path to the `.mesh` file.
4. Place the mesh somewhere in the world.


> **Notice:** You can change the path to the mesh at any time in the *Mesh* field.
