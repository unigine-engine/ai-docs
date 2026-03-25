# dynamic_05

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


This article describes the `data/samples/objects/dynamic_05.cpp` sample.


The `dynamic_05` sample demonstrates how to copy geometry of a static mesh to a dynamic object.

> **Notice:** The material which is used for the dynamic object is specified in the `dynamic_05.mat` file.


Since the dynamic object requires a custom shader for rendering, in this sample, the shader that is used for a mesh is [applied](../../../../code/formats/materials_formats/ulon_materials/binds.md) to the dynamic object to avoid creating the new shader.


![](dynamic_05.gif)

*The left statue is the dynamic object copied from the static mesh (the right statue)*


### See Also


- Functions of the [ObjectDynamic](../../../../api/library/objects/class.objectdynamic_cpp.md) class
- Articles on [*Materials Files*](../../../../code/formats/materials_formats/index.md) formats to learn more about the `*.basemat` and `*.mat` files
- Article on [*Built-in Base Materials*](../../../../content/materials/library/index.md) to choose the material, from which the material for the dynamic object can be inherited
