# Leaks Tool


![](../leaks.png) **Leaks** tool is used for procedural painting of a leaks mask: a projection of screen space leaks calculated from the current camera position is written into the texture. The leaks mask is a black and white texture (similar to the ambient occlusion texture) that stores gradients directed along the gravity vector. For example, a convex detail on a wall will produce the downward gradient.


The **Leaks** tool is used for painting leaks on complex 3D models, especially on surfaces aligned at an angle to other surfaces, and other places where the leaks may occur. For example:


![](leaks_length.png)


The arrows show direction of the gradient.


Leaks calculation with the *Leaks* tool doesn't depend on the UV map, as it is performed using screen-space tracing.


## Settings


![](leaks.png)


| Draw Blend Mode | Sets a blending mode used for painting. For more details, see the *[Brush](../../../editor2/texture_editor/brush_tool/index.md#tools_brush)* tool settings. |
|---|---|
| Leaks Length | Length of the painted leaks. |
| Leaks Softness | Softness of the painted leaks. |
| Intersection By Depth Threshold | Depth threshold (in units) limits the leaks effect in areas where information cannot be obtained. The *higher* the value, the less pronounced the effect is. |
