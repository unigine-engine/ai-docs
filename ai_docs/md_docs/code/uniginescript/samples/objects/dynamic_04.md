# dynamic_04

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


This article describes the `data/samples/objects/dynamic_04.cpp` sample.


The `dynamic_04` sample demonstrates how to create a dynamic mesh with multiple surfaces that are added one after another.


![](dynamic_04.gif)

*A dynamic mesh with multiple surfaces*


In this sample, each box is formed of the triangles created by adding one vertex after another. Once the box is created, it is added to the dynamic mesh as the surface.


### See Also


- Article on the [*Dynamic Mesh*](../../../../objects/objects/mesh_dynamic/index.md)
- Functions of the [ObjectMeshDynamic](../../../../api/library/objects/class.objectmeshdynamic_cpp.md) class
