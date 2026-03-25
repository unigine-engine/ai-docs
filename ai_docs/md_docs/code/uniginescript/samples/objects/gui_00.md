# gui_00

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


This article describes the `data/samples/objects/gui_00.cpp` sample.


The `gui_00` sample demonstrates how to play a video on a GUI object positioned in the world, namely:

- Create a flat [GUI object](../../../../api/library/objects/class.objectgui_cpp.md)
- Assign an instance of the [WidgetSpriteVideo](../../../../api/library/gui/class.widgetspritevideo_cpp.md) class to the created object in order to play a video file


![](gui_00.gif)

*Video on the GUI object created with the gui_00.cpp script*


### See Also


- Article on the [*GUI Object*](../../../../objects/objects/gui/gui_object.md)
- Functions of the [ObjectGui](../../../../api/library/objects/class.objectgui_cpp.md) class
- Functions of the [WidgetSpriteVideo](../../../../api/library/gui/class.widgetspritevideo_cpp.md) class
