# Curvature Tool


![](../curvature.png) **Curvature** tool is used for painting a curvature texture: a projection of screen space curvature calculated from the current camera position is written into the texture. It avoids generating the curvature texture with both the front and back faces visible. For example, using this tool, you will never get the curvature texture for the table where the table leg is visible behind the tabletop.


## Settings


![](curvature.png)


| Draw Blend Mode | Sets a blending mode used for painting. For more details, see the *[Brush](../../../editor2/texture_editor/brush_tool/index.md#tools_brush)* tool settings. |
|---|---|
| Curvature Radius | Radius of the curvature mapping. |
| Intersection By Depth Threshold | Depth threshold (in units) limits curvature mapping in areas where information cannot be obtained. The *higher* the value, the less pronounced the curvature effect is. |


> **Notice:** You can use the [*Fill*](../../../editor2/texture_editor/index.md#stroke_mode) stroke mode for fast texture painting.
