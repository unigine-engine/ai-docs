# gui_02

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


This article describes the `data/samples/objects/gui_02.cpp` sample.


The `gui_02` sample demonstrates how to display the current scene on a virtual monitor created with the WidgetSpriteViewport and assigned to a GUI object, namely:

- Create the flat [GUI object](../../../../api/library/objects/class.objectgui_cpp.md)
- Create an instance of the [WidgetSpriteViewport](../../../../api/library/gui/class.widgetspriteviewport_cpp.md) class and associate it with the camera
- Assign the created instance to the GUI object
- Set modelview and projection matrices for the associated camera and change them according to the time spent since the world loading. It will force the camera go round the objects in the scene.


![](gui_02.gif)

*WidgetSpriteViewport assigned to the GUI object*


### See Also


- Article on the [*GUI Object*](../../../../objects/objects/gui/gui_object.md)
- Functions of the [ObjectGui](../../../../api/library/objects/class.objectgui_cpp.md) class
- Functions of the [WidgetSpriteViewport](../../../../api/library/gui/class.widgetspriteviewport_cpp.md) class
