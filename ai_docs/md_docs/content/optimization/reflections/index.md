# Dynamic Reflections Optimization


Dynamic reflections in the scene may significantly drop the performance if they aren't properly set up. For example, the planar reflection doubles the polygon count since it takes into account all geometry in the scene by default. It may raise performance issues in large and heavy scenes.


As an alternative, you can try to keep the number of reflections as low as possible. However, there is a way to optimize dynamic reflections usage without visual losses.


> **Notice:** For dynamic reflections to be rendered, the *Rendering -> Dynamic Reflections -> Enabled* flag should be set.


The number of reflection polygons for each surface can be checked using the [Surfaces](../../../editor2/assets_optimize/content_profiler/surface_profiler.md) tab of the [Content Profiler](../../../editor2/assets_optimize/content_profiler/index.md) tool.


## Using Reflection Masks


The *[*Reflection* mask](../../../principles/bit_masking/index.md#reflection_mask)* allows controlling rendering of dynamic reflections into the reflection camera viewport. This mask can be set for dynamic Environment Probes and *planar reflections*.


### Optimizing planar reflections


To optimize the scene with *[planar reflection probes](../../../objects/lights/planar/index.md)*, you can apply the following approach: set up the scene so that only the required planar reflections are rendered, and use less consuming *Screen Space Reflections ([SSR](../../../editor2/settings/render_settings/ssr/index.md))* for other reflections. An example workflow is as follows:


1. Decide, which bit of the viewport mask would be responsible for reflection of the object.
2. Open the [Camera Settings window](../../../editor2/camera_settings/index.md#setup_camera) and enable the selected bit in the *Reflection Viewport* mask of the camera. ![](camera_settings.png)
3. In the Materials Hierarchy, select the reflective material and enable the same bit in the *Reflection Viewport Mask* in the *Parameters* tab of the Material Editor. ![](planar_parameters.png)
4. In the World Hierarchy, select the node to be reflected and go to the *Node* tab of the *Parameters* window.
5. In the *Surfaces* section, enable the selected bit in the *[Viewport Mask](../../../editor2/node_parameters/visual_representation/index.md#viewport_mask)* for all surfaces that should be reflected. > **Notice:** You can create the special low-poly LOD surface that will be used for reflections only; the viewport mask of such a LOD shouldn't match the camera's viewport mask to exclude it from rendering.
6. In the Materials Hierarchy, select the material of the node that should be reflected and enable the selected bit in the *[Viewport Mask](../../../editor2/materials_settings/index.md#viewport_mask)* in the *Common* tab of the Materials Editor. In the picture below, the reflection viewport mask of the plane has the same matching bit (or bits) with the camera reflection viewport mask **and** the *Viewport* masks of the red material ball and its material. The viewport masks of the other material balls don't have a matching bit with the reflection camera viewport mask and/or with the planar reflection viewport mask and, therefore, they aren't reflected: ![](planar_reflection_masked.png) *Masked planar reflection*
7. Enable *[Screen Space Reflections](../../../editor2/settings/render_settings/ssr/index.md)* to produce reflections of other nodes in the scene: on the Menu Bar, toggle the *Rendering -> Features -> SSR* option on. > **Notice:** The SSR effect should be also enabled for the reflective material: go the *Post Processing* section of the *States* tab and check if the *[SSR](../../../content/materials/library/mesh_base/index.md#post_processing)* option is enabled. ![](planar_ssr.png) *Masked planar reflection + SSR*


### Optimizing environment probe reflections


Dynamic reflections provided by Environment Probes can be optimized in the same way as described above. To specify the *Reflection Viewport* mask for the Environment Probe, go to the *Environment Probe* section of the *Parameters* window and set the *Reflection Viewport Mask* parameter in the *Baking Settings* section.


> **Notice:** The *Reflection Viewport* mask takes effect only when the *[Realtime Update](../../../objects/lights/envprobe/index.md#mode)* mode is set for the Environment Probe.


In the left picture below, the reflection viewport mask of the Environment Probe matches the camera's *Reflection Viewport* mask and the *Viewport* masks of the red material ball and its material. In the right picture, the *Reflection Viewport* mask of the Environment Probe doesn't match the camera's *Reflection Viewport* mask:


![](env_probe_reflections.png) ![](env_probe_no_reflections.png)


*Masked reflection provided by environment probe*


> **Notice:** An example of using reflection masks is also available in the [![](../youtube_link.png)Content Optimization](https://youtu.be/Iqsr3fEvnis?t=770) video tutorial.


## Setting Up Reflection Distance


One more method that allows optimizing rendering of dynamic reflections is to set the distance at which reflections are turned off.


### Environment Probes


This method is suitable for dynamic reflections provided by [Environment Probes](../../../objects/lights/envprobe/index.md) only.


1. In the Menu Bar, choose *Windows -> Settings* and go to the *[Visibility Distances](../../../editor2/settings/render_settings/visibility_distances/index.md)* section of the Settings window that opens. ![](distance_reflection.png)
2. For the *[Dynamic Reflections](../../../editor2/settings/render_settings/visibility_distances/index.md#reflection_distance)* parameter, specify the distance from the camera, starting from which the reflections aren't rendered.


### Planar Reflection Probes


To optimize [Planar Reflection Probe](../../../objects/lights/planar/index.md), you can try to adjust the following parameters of its material:


![](planar_reflection_parameters.png)


- **[Visibility Distance](../../../objects/lights/planar/index.md#visibility_distance)** and **[Fade Distance](../../../objects/lights/planar/index.md#fade_distance)** not to render the reflecting surface at all, when the camera is far from it.
- **[Reflection Distance](../../../objects/lights/planar/index.md#reflection_distance)** to avoid rendering reflections that can't be seen, when the camera is far from the reflecting surface.
- **[Distance Scale](../../../objects/lights/planar/index.md#distance_scale)** to apply the less detailed LODs to reflections at a closer distance, than to the corresponding reflected objects.
- **[ZFar](../../../objects/lights/planar/index.md#zfar)** to limit the viewing frustum that is used for reflection grabbing to avoid rendering reflections of unnesessary distant objects.
