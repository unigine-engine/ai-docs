# Debug Materials


A *debug material* is a material that can be used for debugging of the image generation stages. By using the debug materials, you can check how the scene looks on a certain stage, visualize contents of the rendering buffers, check how they are blended into the final image. It means that you can render only reflections, or lighting, or only cubemaps, and so on.


![](debug_0.jpg) ![](debug_1.jpg)


The debug materials also allow you to check how sRGB correction and automatic exposure affect the final image.


The debug material includes all deferred buffers that are used on the *[Deferred Composite](../../../../principles/render/sequence/index.md#deferred_composite)* stage of the rendering sequence: you can compose contents of these buffers in any desired way. However, note that according to the rendering sequence, the debug materials are rendered after [transparent objects rendering](../../../../principles/render/sequence/index.md#transparent). So, the deferred buffers will contain data written by the transparent objects (if their materials have the *Deferred Buffers* flag set).


> **Notice:** The debug material can be used as a [composite material](../../../../content/materials/library/debug/debug_materials/index.md#debug_composite).


UNIGINE provides a set of [preconfigured materials](#debug_materials_presets) inherited from the *[debug_materials](../../../../content/materials/library/debug/debug_materials/index.md)* material: you can use one of them or inherit from *debug_materials* and set up your own debug material.


> **Notice:** The debug material doesn't change the image rendered in the viewport: it is rendered atop the current viewport as a *debug image*. This image can be modified: you can change its [size](../../../../content/materials/library/debug/debug_materials/index.md#parameter_width), or specify an [offset](../../../../content/materials/library/debug/debug_materials/index.md#parameter_offset_x) along the axes.


The debug materials have the higher priority than the settings in the *[Rendering Debug Panel](../../../../editor2/interface/index.md#viewports)* of the UNIGINE Editor.


## Applying Debug Materials


To apply a debug material, perform the following:

1. Enable rendering of the debug materials in one of the following ways:

  - Via the UNIGINE Editor: on the Menu Bar, choose *Rendering -> Features -> Debug Materials*.
  - Via the console: specify 1 for the *[render_debug](../../../../code/console/index.md#render_debug)* console command.
2. In the *[Debug Materials](../../../../editor2/settings/render_settings/debug/index.md)* tab of the *Settings* window, click **Add New Material** and specify the material that should be applied in the field that appears.


> **Notice:** You can add several materials: the last material in the list will be rendered atop the other debug materials. To change the rendering order, click ![](change_order.png).


## Masking Debug Materials


By using the mask, you can control the area of debug material visibility. For example, by using the mask, you can create a smooth transition between the image that displays a rendering buffer and the final image. Or you can combine these images as follows:


![](mask_applied.png)

*Diffuse Lighting Image (debug_lightsmaterial) Combined with Final Image*


## Debug Materials Presets


UNIGINE provides a set of preconfigured debug materials that allow debugging lighting, reflections, screen space effects, and so on. These materials are available in the *[Materials Hierarchy Window](../../../../editor2/materials_settings/organizing_materials/index.md)*:


![](debug_materials_presets.png)

*Debug Materials Presets in Materials Hierarchy*


Such materials are inherited from *[debug_materials](../../../../content/materials/library/debug/debug_materials/index.md)*. You can [apply](#applying) one of them as is, or inherit a new material from one of them and change the parameters, apply a [mask texture](#masking), or toggle the states on and off.


The following pictures demonstrate some of the preconfigured debug materials applied to the scene:


| ![](debug_ssao.jpg) | ![](debug_ssr.jpg) |
|---|---|
| *debug_ssao Material* | *debug_ssr Material* |
| ![](debug_ambient_light.jpg) | ![](debug_diffuse_light.jpg) |
| *debug_ambient_light Material* | *debug_diffuse_light Material* |
