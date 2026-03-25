# dynamic_01

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


This article describes the `data/samples/objects/dynamic_01.cpp` sample.


The `dynamic_01` sample demonstrates how to create a dynamic mesh by using the **Marching cubes** algorithm.

> **Notice:** In this sample, 3D scalar fields are created one after another.


![](dynamic_01.gif)

*A dynamic mesh created by means of the Marching cubes algorithm*


Also the sample shows, how to start counters for the fields and cubes in the performance profiler. This counters tell the user how many milliseconds have been spent for fields and cubes creation.


### See Also


- Article on the [*Dynamic Mesh*](../../../../objects/objects/mesh_dynamic/index.md)
- Functions of the [ObjectMeshDynamic](../../../../api/library/objects/class.objectmeshdynamic_cpp.md) class
