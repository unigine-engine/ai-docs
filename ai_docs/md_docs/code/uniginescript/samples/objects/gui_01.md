# gui_01

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


This article describes the `data/samples/objects/gui_01.cpp` sample.


The `gui_01` sample demonstrates how to play a video on a mesh, namely:

- Create a [non-flat GUI display](../../../../api/library/objects/class.objectguimesh_cpp.md)
- Assign an instance of the [WidgetSpriteVideo](../../../../api/library/gui/class.widgetspritevideo_cpp.md) class to the created mesh in order to play a video file


![](gui_01.gif)

*Video on the mesh created with the gui_01.cpp script*


In this sample, each of 3 displays is a surface of the GUI mesh. So, the video is rendered on each of them.

> **Notice:** Texture coordinates of both the left and right surfaces (displays) are two times larger than the texture coordinates of the central surface (display), so the video is rendered four times on each of them.


### See Also


- Article on the [*GUI Mesh*](../../../../objects/objects/gui/gui_mesh.md)
- Functions of the [ObjectGuiMesh](../../../../api/library/objects/class.objectguimesh_cpp.md) class
- Functions of the [WidgetSpriteVideo](../../../../api/library/gui/class.widgetspritevideo_cpp.md) class
