# Ambient Occlusion Tool


![](../ambient_occlusion.png) **Ambient Occlusion** tool is used for drawing an ambient occlusion texture: a projection of [screen space ambient occlusion](../../../editor2/settings/render_settings/global_illumination/indirect_diffuse/ssao/index.md) calculated from the current camera position is written into the texture.


As the ambient occlusion effect is calculated in the screen space, the painted texture will also include the ambient occlusion shadowing from the other objects in the scene. It is useful when, for example, you need to add some dirt in the shaded areas between objects: paint the ambient occlusion mask and use it to add dirt.


## Baking Ambient Occlusion Texture


To bake the ambient occlusion texture via the Ambient Occlusion tool, perform the following:


1. Prepare a black texture and apply it to the target object as the *Albedo* texture.
2. In the Menu Bar, switch the *Rendering Mode* to *Albedo* for clarity.
3. Choose this texture in the *Texture* field of the Ambient Occlusion tool. ![](texture.png) > **Notice:** Or you can change the texture color via Texture Editor using the *[Brush](../../../editor2/texture_editor/brush_tool/index.md)* tool.
4. Set the *Draw Blend Mode* parameter to **Maximum**. In this case, the texture will be brightened when painting. ![](blend_mode.png)
5. Specify the required *Ambient Occlusion Radius*.
6. Specify the maximum available value (10) for the *Intersection By Depth Threshold* parameter. ![](depth_threshold.png)
7. Choose the *[Fill](../../../editor2/texture_editor/index.md#stroke_mode)* stroke mode and paint the texture. You can use any stroke mode, if necessary. > **Notice:** In "information lost" areas, the ambient occlusion won't be drawn. Rotate the camera around the object to paint such areas.
8. [Save](../../../editor2/texture_editor/index.md#save_texture) the texture.


![](anim.gif)


## Settings


![](ambient_occlusion.png)


| Draw Blend Mode | Sets a blending mode used for painting. For more details, see the *[Brush](../../../editor2/texture_editor/brush_tool/index.md#tools_brush)* tool settings. |  |  |  |  |
|---|---|---|---|---|---|
| Ambient Occlusion | Method of ambient occlusion calculation: - **Classic** method calculates how much the points are illuminated. - **By Distance To Surface** method calculates how close is the nearest surface to the shading point. It allows calculating smooth gradients even around small convexities. \| ![](ao_classic.png) \| ![](ao_distance.png) \| \|---\|---\| \| *Classic Ambient Occlusion* \| *Ambient Occlusion By Distance To Surface* \| As you can see, there is no ambient occlusion effect around the small convexity in the first picture. | ![](ao_classic.png) | ![](ao_distance.png) | *Classic Ambient Occlusion* | *Ambient Occlusion By Distance To Surface* |
| ![](ao_classic.png) | ![](ao_distance.png) |  |  |  |  |
| *Classic Ambient Occlusion* | *Ambient Occlusion By Distance To Surface* |  |  |  |  |
| Ambient Occlusion Radius | Distance for each point in the world space, up to which it can shadow its neighboring points. |  |  |  |  |
| Intersection By Depth Threshold | Depth threshold (in units) limits the ambient oclusion effect in areas where information cannot be obtained. The *higher* the value, the less pronounced the effect is. |  |  |  |  |
