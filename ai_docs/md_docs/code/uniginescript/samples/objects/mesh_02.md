# mesh_01

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


This article describes the `data/samples/objects/mesh_01.cpp` sample.


The `mesh_01` sample demonstrates how to deform a static mesh as a dynamic mesh, namely:

- Load the static mesh from a given file and copy it to the dynamic mesh by using the [*setMesh()*](../../../../api/library/objects/class.objectmeshdynamic_cpp.md#setMesh_Mesh_int) function
- Deform vertices of the dynamic mesh
- Add the deformed dynamic mesh [as the static mesh](../../../../api/library/objects/class.objectmeshdynamic_cpp.md#getMesh_Mesh_int) to the editor


![](mesh_02.png)

*49 dynamic ObjectMeshes*


> **Notice:** The static mesh used in this sample is stored in the `samples/objects/meshes/mesh_01.mesh` file.


### See Also


- Article on [*Static Mesh*](../../../../objects/objects/mesh/index.md)
- Article on [*Dynamic Mesh*](../../../../objects/objects/mesh_dynamic/index.md)
- Functions of the [*ObjectMeshStatic*](../../../../api/library/objects/class.objectmeshstatic_cpp.md) class
- Functions of the [*ObjectMeshDynamic*](../../../../api/library/objects/class.objectmeshdynamic_cpp.md) class
