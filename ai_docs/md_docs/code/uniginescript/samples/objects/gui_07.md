# gui_05

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


This article describes the `data/samples/objects/gui_05.cpp` sample.


The `gui_05` sample demonstrates how to create a GUI object with a [custom skin](../../../../code/gui/skin/index.md), namely:

- Specify a path to a folder with an `*.rc` file and custom textures when creating a [GUI object](../../../../api/library/objects/class.objectgui_cpp.md)
- Load a user interface by using the constructor of the [UserInterface](../../../../api/library/gui/class.userinterface_cpp.md) class


![](gui_07.gif)

*GUI object with a custom skin*


In this sample, the window assigned to the GUI object is generated from the `samples/objects/interfaces/gui_05.ui` [UI file](../../../../code/gui/ui/index.md).


You can interact with its elements with the mouse as usual: change position of the window, switch between tabs, etc.


### See Also


- Article on the [*GUI Object*](../../../../objects/objects/gui/gui_object.md)
- Article on the [*Skin Layout*](../../../../code/gui/skin/index.md) to learn how to create a custom skin
- Functions of the [ObjectGui](../../../../api/library/objects/class.objectgui_cpp.md) class
- Functions of the [UserInterface](../../../../api/library/gui/class.userinterface_cpp.md) class
