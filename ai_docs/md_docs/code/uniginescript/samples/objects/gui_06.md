# gui_04

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


This article describes the `data/samples/objects/gui_04.cpp` sample.


The `gui_04` sample demonstrates how to attach a GUI object to a static mesh, namely:

- Create a [GUI object](../../../../api/library/objects/class.objectgui_cpp.md) without a [background](../../../../api/library/objects/class.objectgui_cpp.md#setBackground_bool_void) and  set the value indicating if the GUI object should be a billboard to the 1.
- Assign an instance of the [WidgetLabel](../../../../api/library/gui/class.widgetlabel_cpp.md) class to the created object
- Add the GUI object with the text label to the static mesh as a child


![](gui_06.png)

*GUI object attached to the static mesh*


If you change the mesh position, the label position is also changed.


> **Notice:** If you want to delete an instance of the ObjectGui class, first you have to delete the label assigned to it in your script.


### See Also


- Article on the [*GUI Object*](../../../../objects/objects/gui/gui_object.md)
- Article on the [*Static Mesh*](../../../../objects/objects/mesh/index.md)
- Functions of the [ObjectGui](../../../../api/library/objects/class.objectgui_cpp.md) class
- Functions of the  [ObjectMeshStatic](../../../../api/library/objects/class.objectmeshstatic_cpp.md) class
- Functions of the [WidgetLabel](../../../../api/library/gui/class.widgetlabel_cpp.md) class
