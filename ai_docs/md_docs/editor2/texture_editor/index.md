# Texture Editor


*Texture Editor* allows painting textures of the materials applied to objects directly in the scene. It is mainly used for painting masks, but also helps editing the existing textures: adding details or fixing mistakes. Moreover, the Texture Editor allows creating a new [surface custom texture](../../editor2/node_parameters/visual_representation/index.md#surface_custom_texture) and paint it from scratch.


The Texture Editor is available when the *Texture Paint Mode* is selected on the [toolbar](../../editor2/interface/index.md#tools_panel):


![](texture_paint_mode.png)


> **Notice:** You can also use the **Shift+2** hotkey to activate the tool.


The *Active Tool* window provides access to the tools of the Texture Editor:


![](active_tool.png)


## Painting Texture with Texture Editor


### Painting Existing Texture


To edit a texture via the Texture Editor, do the following:


1. Select an object, a texture of which should be edited.
2. In the *Texture* field of the Texture Editor, choose the required texture in the drop-down list. ![](texture.png)
3. Paint directly on the object using the available [tools](#tools). > **Notice:** When painting, the original asset is edited.


To undo all changes, select another object in the scene and decline saving changes in the window that opens:


![](save_texture.png)


### Painting New Surface Custom Texture


The Texture Editor allows creating a [surface custom textures](../../editor2/node_parameters/visual_representation/index.md#surface_custom_texture) for static meshes.


To create such texture, do the following:


1. Select a surface of a *static mesh* for which you want to create a texture.
2. In the *Texture* field of the Texture Editor, click *Create Texture*. ![](texture.png)
3. In the *Texture Creator* window that opens, specify the *Size*, *Channels* and *Depth* for the new texture and click *OK*. ![](texture_creator.png) Then specify the texture name and save it. The new texture will be automatically applied to the selected surface. Go to the *[Surface Custom Texture](../../editor2/node_parameters/visual_representation/index.md#surface_custom_texture)* section of the *Parameters* window to check it.
4. In the *Texture* field of the Texture Editor, choose *Custom Surface Texture* in the drop-down list.
5. Paint directly on the surface using the available [tools](#tools). > **Notice:** When painting, the original asset is edited.


### Saving Changes


To save changes, choose one of the following options:


![](save.png)


If you choose *Save as New Texture...*, specify a name and a [texture format](../../editor2/assets_workflow/asset_types.md#texture) in the dialog window that opens.


## Tools


The following tools are available:


- ![](brush.png) **[Brush](../../editor2/texture_editor/brush_tool/index.md)** tool (**B** hotkey) allows painting arbitrary shapes on the texture.
- ![](pencil.png) **[Pencil](../../editor2/texture_editor/pencil_tool/index.md)** tool allows painting hard-edged texels on the texture.
- ![](eraser.png) **[Eraser](../../editor2/texture_editor/eraser_tool/index.md)** tool (**E** hotkey) removes changes.
- ![](smooth.png) **[Smooth](../../editor2/texture_editor/smooth_tool/index.md)** tool (**V** hotkey) blurs texels of the texture.
- ![](smudge.png) **[Smudge](../../editor2/texture_editor/smudge_tool/index.md)** tool smudges the texture.
- ![](contrast.png) **[Contrast](../../editor2/texture_editor/contrast_tool/index.md)** tool changes the texture contrast.
- ![](brightness.png) **[Brightness](../../editor2/texture_editor/brightness_tool/index.md)** tool changes the texture brightness.
- ![](saturation.png) **[Saturation](../../editor2/texture_editor/saturation_tool/index.md)** tool changes intesity of the texture colors.
- ![](replace_color.png) **[Replace Color](../../editor2/texture_editor/replace_color_tool/index.md)** tool replaces all texture colors with the specified one.
- ![](invert.png) **[Invert](../../editor2/texture_editor/invert_tool/index.md)** tool inverts texture colors.
- ![](draw_flowmap.png) **[Draw Flowmap](../../editor2/texture_editor/flowmap_tool/index.md)** tool allows painting a flow map.
- ![](draw_mesh_data.png) **[Draw Mesh Data](../../editor2/texture_editor/mesh_data_tool/index.md)** tool allows drawing textures that store mesh data (positions, mesh normals).
- ![](ambient_occlusion.png) **[Ambient Occlusion](../../editor2/texture_editor/ambient_occlusion_tool/index.md)** tool allows drawing an ambient occlusion texture.
- ![](curvature.png) **[Curvature](../../editor2/texture_editor/curvature_tool/index.md)** tool allows painting a curvature texture.
- ![](leaks.png) **[Leaks](../../editor2/texture_editor/leaks_tool/index.md)** tool allows painting leaks.
- ![](color_picker.png) **[Color Picker](../../editor2/texture_editor/color_picker_tool/index.md)** tool allows picking a texture color.


## Common Settings


Depending on the selected tool, a set of available settings varies. However, there are settings common for most of the tools:


| Texture | Texture to be edited. |  |  |  |  |  |  |  |  |  |  |
|---|---|---|---|---|---|---|---|---|---|---|---|
| Show Debug | Show per-channel changes. |  |  |  |  |  |  |  |  |  |  |
| Stroke Mode | - ![](brush_stroke.png) **Brush** � draw a stroke of brush marks. - ![](stamp.png) **Stamp** � draw a sigle brush mark. - ![](lasso.png) **Lasso** � fill the selected rectangular area with a specified color. By default, areas of the object that are visible in the current viewport are filled. - ![](gradient.png) **Gradient** � draw a linear gradient. - ![](line.png) **Line** � draw a line. It can be used, for example, to align edges of a mask. - ![](fill.png) **Fill** � fill the texture with a specified color. > **Notice:** The set of tool settings changes depending on the *Stroke Mode*. See the [Stroke Mode Specific Settings](#stroke_mode_settings) chapter for details. |  |  |  |  |  |  |  |  |  |  |
| Rotate Along Stroke | Orients the brush marks to follow the stroke direction. \| ![](rotate_0.png) \| ![](rotate_1.png) \| \|---\|---\| \| *Rotate Along Stroke Disabled* \| *Rotate Along Stroke Enabled* \| | ![](rotate_0.png) | ![](rotate_1.png) | *Rotate Along Stroke Disabled* | *Rotate Along Stroke Enabled* |  |  |  |  |  |  |
| ![](rotate_0.png) | ![](rotate_1.png) |  |  |  |  |  |  |  |  |  |  |
| *Rotate Along Stroke Disabled* | *Rotate Along Stroke Enabled* |  |  |  |  |  |  |  |  |  |  |
| Brush Texture | Texture that defines shape of the brush. \| ![](brush_texture_0.png) \| ![](brush_texture_1.png) \| ![](brush_texture_2.png) \| \|---\|---\|---\| | ![](brush_texture_0.png) | ![](brush_texture_1.png) | ![](brush_texture_2.png) |  |  |  |  |  |  |  |
| ![](brush_texture_0.png) | ![](brush_texture_1.png) | ![](brush_texture_2.png) |  |  |  |  |  |  |  |  |  |
| Brush Texture Opacity | 1-channeled opacity texture that controls application of the [Brush Texture](#brush_texture). White areas of the texture make the corresponding areas of the Brush Texture fully visible, black ones make them fully transparent. |  |  |  |  |  |  |  |  |  |  |
| Brush Radius | Radius of the brush. > **Notice:** You can change the brush radius by scrolling the mouse wheel. \| ![](brush_radius_0.png) \| ![](brush_radius_1.png) \| \|---\|---\| \| *Brush Radius = 0.03* \| *Brush Radius = 0.01* \| | ![](brush_radius_0.png) | ![](brush_radius_1.png) | *Brush Radius = 0.03* | *Brush Radius = 0.01* |  |  |  |  |  |  |
| ![](brush_radius_0.png) | ![](brush_radius_1.png) |  |  |  |  |  |  |  |  |  |  |
| *Brush Radius = 0.03* | *Brush Radius = 0.01* |  |  |  |  |  |  |  |  |  |  |
| Brush Spacing | Distance between the brush marks in the stroke, in percent. 0 means the brush mark is drawn each frame (i.e. no spaces). \| ![](brush_spacing_0.png) \| ![](brush_spacing_1.png) \| \|---\|---\| \| *Brush Spacing = 0* \| *Brush Spacing = 100* \| | ![](brush_spacing_0.png) | ![](brush_spacing_1.png) | *Brush Spacing = 0* | *Brush Spacing = 100* |  |  |  |  |  |  |
| ![](brush_spacing_0.png) | ![](brush_spacing_1.png) |  |  |  |  |  |  |  |  |  |  |
| *Brush Spacing = 0* | *Brush Spacing = 100* |  |  |  |  |  |  |  |  |  |  |
| Brush Angle | Angle of the brush marks, in degrees. \| ![](brush_angle_0.png) \| ![](brush_angle_1.png) \| ![](brush_angle_2.png) \| \|---\|---\|---\| \| *Brush Angle = 0* \| *Brush Angle = 30* \| *Brush Angle = 60* \| | ![](brush_angle_0.png) | ![](brush_angle_1.png) | ![](brush_angle_2.png) | *Brush Angle = 0* | *Brush Angle = 30* | *Brush Angle = 60* |  |  |  |  |
| ![](brush_angle_0.png) | ![](brush_angle_1.png) | ![](brush_angle_2.png) |  |  |  |  |  |  |  |  |  |
| *Brush Angle = 0* | *Brush Angle = 30* | *Brush Angle = 60* |  |  |  |  |  |  |  |  |  |
| Opacity | Strength of the brush. Higher values create more opaque bush strokes. Multiple applications of the brush with low opacity to the same place create a more opaque image. It can be used for drawing smooth gradients. \| ![](opacity_0.png) \| ![](opacity_1.png) \| ![](opacity_2.png) \| \|---\|---\|---\| \| *Opacity = 0.3* \| *Opacity = 0.3, multiple brush applcations* \| *Opacity = 1.0* \| | ![](opacity_0.png) | ![](opacity_1.png) | ![](opacity_2.png) | *Opacity = 0.3* | *Opacity = 0.3, multiple brush applcations* | *Opacity = 1.0* |  |  |  |  |
| ![](opacity_0.png) | ![](opacity_1.png) | ![](opacity_2.png) |  |  |  |  |  |  |  |  |  |
| *Opacity = 0.3* | *Opacity = 0.3, multiple brush applcations* | *Opacity = 1.0* |  |  |  |  |  |  |  |  |  |
| Color | Color of the brush. You can specify the *Main* and the *Spare* color and switch them by pressing X when painting the texture. To pick a texture color, press C or click the *Pick Screen Color* button in the *Select Color* window and sample the color. |  |  |  |  |  |  |  |  |  |  |
| Color Intensity | Intensity of the brush color. It allows changing shades of the same color: the *lower* the value, the darker the result. \| ![](color_intensity_0.png) \| ![](color_intensity_1.png) \| ![](color_intensity_2.png) \| \|---\|---\|---\| \| *Color Intensity = 1.0* \| *Color Intensity = 0.5* \| *Color Intensity = 0.1* \| | ![](color_intensity_0.png) | ![](color_intensity_1.png) | ![](color_intensity_2.png) | *Color Intensity = 1.0* | *Color Intensity = 0.5* | *Color Intensity = 0.1* |  |  |  |  |
| ![](color_intensity_0.png) | ![](color_intensity_1.png) | ![](color_intensity_2.png) |  |  |  |  |  |  |  |  |  |
| *Color Intensity = 1.0* | *Color Intensity = 0.5* | *Color Intensity = 0.1* |  |  |  |  |  |  |  |  |  |
| Brush Backface Culling Angle | Normal angle at which the surface is ignored by the brush. It allows you to avoid painting across certain surfaces. \| ![](culling_0.png) \| ![](culling_1.png) \| \|---\|---\| \| *Culling Angle = 90* \| *Culling Angle = 120* \| | ![](culling_0.png) | ![](culling_1.png) | *Culling Angle = 90* | *Culling Angle = 120* |  |  |  |  |  |  |
| ![](culling_0.png) | ![](culling_1.png) |  |  |  |  |  |  |  |  |  |  |
| *Culling Angle = 90* | *Culling Angle = 120* |  |  |  |  |  |  |  |  |  |  |
| Radius Jitter | Random radius of the brush marks in the stroke. 0 means no randomness. ![](radius_jitter.png) |  |  |  |  |  |  |  |  |  |  |
| Angle Jitter | Random rotation angle of the brush marks in the stroke (in degrees). 0 means no randomness. ![](angle_jitter.png) |  |  |  |  |  |  |  |  |  |  |
| Position Jitter | Random position offset of the brush marks in the stroke (in units). 0 means no randomness. ![](position_jitter.png) |  |  |  |  |  |  |  |  |  |  |
| Procedural Mask | Limits brush application to a certain area: - Normal � paint without restrictions. - Dark Area of Ambient Occlusion � paint only dark areas of ambient occlusion. When this option is used, [settings of the ambient occlusion](../../editor2/texture_editor/ambient_occlusion_tool/index.md#tools_ambient) are available. - Light Area of Ambient Occlusion � paint only light areas of ambient occlusion. When this option is used, [settings of the ambient occlusion](../../editor2/texture_editor/ambient_occlusion_tool/index.md#tools_ambient) are available. \| ![](ao.png) \| ![](procedural_ao_0.png) \| ![](procedural_ao_1.png) \| \|---\|---\|---\| \| *Ambient Occlusion* \| *Dark Area of Ambient Occlusion* \| *Light Area of Ambient Occlusion* \| - Cavity � paint only cavity areas. When this option is used, [settings of the curvature](../../editor2/texture_editor/ambient_occlusion_tool/index.md#tools_ambient) are available. - Convexity � paint only convex areas. When this option is used, [settings of the curvature](../../editor2/texture_editor/ambient_occlusion_tool/index.md#tools_ambient) are available. \| ![](cavity.png) \| ![](convexity.png) \| \|---\|---\| \| *Cavity* \| *Convexity* \| Painting the cavity/convex area can be useful when, for example, you need to paint a cavity/convexity mask for a huge building. | ![](ao.png) | ![](procedural_ao_0.png) | ![](procedural_ao_1.png) | *Ambient Occlusion* | *Dark Area of Ambient Occlusion* | *Light Area of Ambient Occlusion* | ![](cavity.png) | ![](convexity.png) | *Cavity* | *Convexity* |
| ![](ao.png) | ![](procedural_ao_0.png) | ![](procedural_ao_1.png) |  |  |  |  |  |  |  |  |  |
| *Ambient Occlusion* | *Dark Area of Ambient Occlusion* | *Light Area of Ambient Occlusion* |  |  |  |  |  |  |  |  |  |
| ![](cavity.png) | ![](convexity.png) |  |  |  |  |  |  |  |  |  |  |
| *Cavity* | *Convexity* |  |  |  |  |  |  |  |  |  |  |
| Active Channels | Channels that are modified when painting the texture. |  |  |  |  |  |  |  |  |  |  |
| UV Channel | UV channel that is used when painting the texture. - UV Channel 0 � 1st UV channel. - UV Channel 1 � 2nd UV channel. There are no specific requirements for the number of UV channels � you can have either one or both. Just make sure to choose the correct channel when painting: you should know in advance which UV channel the texture will use. For example, if a mask for blending materials uses 2nd UV channel, you will choose *UV Channel 1* when editing this mask. > **Notice:** Painting the texture using both channels will produce the incorrect result. By default, textures use the 1st UV channel. If necessary, you can change it in the material via the [Material Editor](../../content/materials/graph/index.md). If you want to use the 2nd UV channel when painting, but it is empty, you can perform [automatic unwrapping for this channel](../../editor2/fbx/index.md#options_lightmaps) when importing the model into UNIGINE. |  |  |  |  |  |  |  |  |  |  |


### Stroke Mode Specific Settings


The [Rectangle](#stroke_mode) and [Linear Gradient](#stroke_mode) stroke modes have additional specific settings described below.


| Depth Limit | Depth limit for filling areas of the object that are not visible in the current viewport (i.e. occluded by other objects). |  |  |  |  |
|---|---|---|---|---|---|
| Depth Limit Gradient Length | Size of the gradient along the edges of the filled area. |  |  |  |  |
| Rectangle Texture | Texture that fills the selected rectangular area. Available for the [Rectangle](#stroke_mode) mode only. \| ![](rectangle_texture_0.png) \| ![](rectangle_texture_1.png) \| \|---\|---\| \| *Object with Original Texture* \| *Rectangular Texture Applied* \| | ![](rectangle_texture_0.png) | ![](rectangle_texture_1.png) | *Object with Original Texture* | *Rectangular Texture Applied* |
| ![](rectangle_texture_0.png) | ![](rectangle_texture_1.png) |  |  |  |  |
| *Object with Original Texture* | *Rectangular Texture Applied* |  |  |  |  |
| Rectangle Texture Opacity | 1-channeled opacity texture that controls application of the [Rectangle Texture](#rectangle_texture). White areas of the texture make the corresponding areas of the Rectangle Texture fully visible, black ones make them fully transparent. |  |  |  |  |
