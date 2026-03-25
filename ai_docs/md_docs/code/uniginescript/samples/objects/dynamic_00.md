# dynamic_00

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


This article describes the `data/samples/objects/dynamic_00.cpp` sample.


The `dynamic_00` sample demonstrates how to create a dynamic wave, namely:

- Create a dynamic mesh with a big number of vertices and add it to the editor
- Calculate normal vectors, tangent vectors and a mesh bounding box


![](dynamic_00.gif)

*Dynamic wave created with the dynamic_00.cpp script*


### See Also


- Article on the [*Dynamic Mesh*](../../../../objects/objects/mesh_dynamic/index.md)
- Functions of the [ObjectMeshDynamic](../../../../api/library/objects/class.objectmeshdynamic_cpp.md) class
