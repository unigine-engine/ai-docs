# Screen Space Bevel


The section contains settings that control screen-space bevels. Using bevels allows you to create smoothed edges of geometry and gives a realistic look to objects in the scene.


![](ssbevel.png)

*Screen-Space Bevel Settings*


> **Notice:** Settings are applied to materials with the ***SSBevel*** state enabled.


| Enabled | The value indicating if the Screen-Space Bevels (SSBevel effect) are enabled. **enabled** by default. `Console access:render_ssbevel` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_ssbevel)) |
|---|---|
| Mode | The rendering mode of the screen-space bevels. The following modes are available: - **Better Edges** smoothes vertex and surface normals of the object. In this mode, the relief created by using Normal Mapping will be smoothed along with the mesh edges. - **Better Normals** smoothes only vertex normals. In this mode, only edges of the mesh geometry will be bevelled. The mode may produce visual artifacts on the edges. However, they can be reduced by increasing quality settings of [anti-aliasing](../../../../principles/render/antialiasing/taa.md). To use this option, rendering of SSBevel*[SSBevel](#render_ssbevel)* should be enabled. Option **#1** is selected by default (see above). `Console access:render_ssbevel_vertex_normal` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_ssbevel_vertex_normal)) ![](bevels_mode_0.jpg) ![](bevels_mode_1.jpg) |
| Quality | The [quality mode](../../../../editor2/settings/render_settings/ssbevel/index.md#quality) for the screen-space bevels. One of the following values: - *Low* - low quality - *Medium* - medium quality (by default) - *High* - high quality - *Ultra* - ultra quality `Console access:render_ssbevel_quality` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_ssbevel_quality)) ![](bevels_quality_0.jpg) ![](bevels_quality_1.jpg) |
| Radius | The [size](../../../../editor2/settings/render_settings/ssbevel/index.md#radius) of the Screen-Space Bevel effect. To use this option, rendering of SSBevel *[SSBevel](#render_ssbevel)* should be enabled. Range of values: **[0.0f, inf]**. The default value is : **0.01f**. `Console access:render_ssbevel_radius` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_ssbevel_radius)) |
| Noise | The value indicating if the [noise](../../../../editor2/settings/render_settings/ssbevel/index.md#noise) is enabled for smoothing bevels. It is recommended to use the noise with TAA*[TAA](#render_taa)* enabled to avoid visual artifacts. The bevel noise is applied at a certain distance from the camera (i.e. if the camera is too far from the object with bevels, the noise won't be applied). To use this option, rendering of SSBevel*[SSBevel](#render_ssbevel)* should be enabled. **enabled** by default. `Console access:render_ssbevel_noise` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_ssbevel_noise)) ![](bevels_noise_0.jpg) ![](bevels_noise_1.jpg) |


> **Notice:** To debug rendering of bevels, you can use the *debug_bevel* [debug material](../../../../content/materials/library/debug/index.md) or enable the bevel rendering buffer via *[Rendering Debug](../../../../editor2/interface/index.md#viewports) -> Bevel*.


## Setting Up Bevels Per Material


Screen-space bevels are set up per material. The settings described above allow you to set up bevels for all materials with the *[SSBevel](../../../../content/materials/library/mesh_base/index.md#option_bevel)* option enabled. However, you can also set up bevels for each material individually via the *[Parameters](../../../../editor2/node_parameters/index.md)* window with [material settings](../../../../editor2/materials_settings/index.md).


To set up bevels for a specific material, perform the following:


1. Enable the *[Procedural Effects](../../../../content/materials/library/mesh_base/index.md#option_procedural)* option of the target material.
2. Enable the *[SSBevel](../../../../content/materials/library/mesh_base/index.md#option_bevel)* option of the target material.
3. [Enable](#enabled) the screen-space bevel feature in one of the following ways:

  - Via the *Render Settings* window: go to the *Windows -> Settings -> Runtime -> Render -> SSBevel* section and click **Enabled**.
  - In the *Main Menu* select *Rendering -> Features* and choose **SSBevel**.
4. In the *Render Settings* window, specify the [global SSBevel settings](#enabled) described above.
5. In the [material settings](../../../../editor2/materials_settings/index.md) (the *Parameters* window), specify the [procedural texture](../../../../content/materials/library/mesh_base/index.md#texture_procedural), [UV coordinates transformation](../../../../content/materials/library/mesh_base/index.md#parameters_bevel_uv_transform) or [triplanar blending factor](../../../../content/materials/library/mesh_base/index.md#parameters_bevel_triplanar), [scale](../../../../content/materials/library/mesh_base/index.md#parameters_bevel_scale) for the bevel [radius](#radius).
