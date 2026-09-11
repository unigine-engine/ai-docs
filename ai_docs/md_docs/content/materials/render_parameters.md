# Custom Render Parameters


A **custom render parameter** is a named value **global for the whole project**, which allows changing the appearance of different materials at once, without editing their assets.


In large projects, material hierarchies can grow into complex structures with parent materials passing properties down to numerous children. While this is convenient for bulk updates - one change propagates through the entire hierarchy - it also has a downside: any modification to a parent material triggers updates for all dependent materials across the project, not just those currently used in the scene. It comes at a high performance cost, especially when thousands of materials are involved.


A custom render parameter instead provides a global value that is read by the materials that use it while the frame is rendered. By default, no shader recompilation is triggered: a single uniform value is updated on the GPU, which gives an instant result. If a material isn't loaded into memory, it won't receive the parameter until it's instantiated.


You define the target parameter once and reference it wherever needed, selectively adjusting the color, surface state, lighting, and so on. This is especially useful for real-time effects such as global wetness after rain, dust, dirt or snow level on objects, modifying global tint, saturation, roughness or emission values, or other gameplay-driven visual effects.


One more benefit is consistency: all team members reference the same global value, which avoids mismatches between materials created by different artists.


> **Notice:** A render parameter is the same for the whole project. When a value has to differ within a scene - a class number for a segmentation pass, the wetness of one particular puddle, the backscatter coefficient of a substance a sensor view reacts to - it belongs to a surface or to a material instead, which [Custom Parameters for Surfaces and Materials](../../content/materials/custom_parameters/index.md) describes. Both kinds are declared on the same settings page, on tabs of their own.


## Creating and Using a Custom Render Parameter


To define and use a custom render parameter, follow these steps:


1. Go to *Settings -> Runtime -> World -> Render -> [Custom Parameters](../../editor2/settings/render_settings/custom_parameters/index.md)* and open the *Render* tab.
2. Click *[Add New Parameter](../../editor2/settings/render_settings/custom_parameters/index.md#add_new)*.
3. Specify the name of the parameter, select its type and set the value, then click *Save*.
4. Open the target material in the *[Material Editor](../../content/materials/graph/index.md)*.
5. Right-click in the Material Editor window and find the custom render parameter by its name.
6. Place the node in the material graph and connect its output either to the required input port of the *Material* node directly, or via additional nodes to achieve more complex behavior.
7. Save the material and close the Material Editor.


![](custom_render_parameter.png)


After that the value of the parameter can be changed on the *Render* tab of the *Custom Parameters* section at any time, and every material using this parameter is updated automatically. Values of custom render parameters can be animated over time by means of the *[Tracker](../../editor2/tools/tracker/index.md)*, the *Sequencer* tool (components of vector parameters can be animated separately), and also be set from code at run time, by the name of the parameter or by its index:


```cpp
Render::setParameterFloat("GlobalWetness", 0.7f);
Render::setParameterFloat3("SunTint", Math::vec3(1.0f, 0.9f, 0.8f));

float wetness = Render::getParameterFloat("GlobalWetness");

// a parameter can also be addressed by index
int num = Render::findParameter("GlobalWetness");
Render::setParameterFloat(num, 0.7f);

```


The index is the position of the parameter in the list and changes when parameters are reordered.


The way the value of a parameter is passed to shaders is defined by the *[Dynamic](../../editor2/settings/render_settings/custom_parameters/index.md#dynamic)* checkbox next to its name.


Values edited in the settings are written to the global *[configuration file](../../code/configuration_file_cpp.md)* (`configs/default.global`) when *Save* is pressed.
