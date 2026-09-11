# Planar Reflection Probe


**Planar Reflection Probe** represents a planar surface that captures and projects a reflection relative to the camera onto a surface just like a mirror. For each visible *Planar Reflection Probe* on the scene a new temporary texture is created every frame.


> **Notice:** *Planar Reflection Probes* currently **support opaque materials only**, to enable planar reflections for transparent materials (*Alpha Blend, Additive*, and *Multiplicative* transparency presets) use the *[corresponding option of the **mesh_base** material](../../../content/materials/library/mesh_base/index.md#option_planar_reflection)*.


![](reflection_camera.png)


The texture is projected on a surface placed behind the *Planar Reflection Probe*. With *Planar Reflection Probe* you can create flat mirrors and flat dynamic reflective surfaces: parquet, flat varnished surfaces, etc.


![](planar_anim.gif)


> **Notice:** The reflections of one *Planar Reflection Probe* will not be rendered in the reflections of another *Planar Reflection Probe* (there are no "reflections in reflections").


### See also


- The *[LightPlanarProbe](../../../api/library/lights/class.lightplanarprobe_cpp.md)* class to manage *Planar Reflection Probe* via API
- An article on [Reflections](../../../editor2/lighting/reflections.md)
- An article on [Dynamic Reflections Optimization](../../../content/optimization/reflections/index.md)
- An article on [Screen-Space Reflections](../../../editor2/settings/render_settings/ssr/index.md)


## Adding a Planar Reflection Probe


To add a *Planar Reflection Probe* node to the scene via UnigineEditor, do the following:


1. On the Menu bar, click *Create -> Lights -> Planar Reflection Probe*. ![](create_planar.png)
2. Place *Planar Reflection Probe* onto the surface that you want to make reflective so that it would intersect the surface. ![](planar_created.png)
3. Decrease the **Roughness** parameter of the surface so that it doesn't go beyond the *[Roughness Visibility Min](#roughnessmin)* and *[Roughness Visibility Max](#roughnessmax)* range.
4. Adjust the **Metalness** parameter of the surface material: higher values make the reflection more visible. ![](planar_placed.png)
5. Adjust the *Planar Reflection Probe* settings to achieve the desired reflection result. [Available parameters](#settings) are described below. > **Notice:** Each *Planar Reflection Probe* renders the scene one more time, therefore, using multiple reflections may significantly affect performance.


## Planar Reflection Probe Settings


The *Planar Reflection Probe* settings can be found in the *Node* tab of the *Parameters* window. This tab includes both the parameters attributable to all light sources and the parameters specific for the probe. The *Planar Reflection Probe* parameters are split into:


1. [Common Parameters](#common) for light and rendering configuration.
2. [Planar Reflection Parameters](#reflection) for reflection configuration.


### Common Parameters


![](common_parameters.png)


| Projection Size | Defines the box-shaped influence volume around the probe, in units, in which reflective surfaces (having the appropriate roughness values) shall use the results captured by the probe. |
|---|---|
| Attenuation Power | Sets the [attenuation power](../../../objects/lights/parameters/index.md#attenuation_power) for the projection. The higher the value, the faster the projection decays within the attenuation area. |
| Attenuation Distance | The [attenuation distance](../../../objects/lights/parameters/index.md#attenuation_distance) specifies how far the projection can reach any surfaces from the Probe position. It also specifies the attenuation area around the Probe at which the projection starts to fade out at the specified rate. |
| Color | Sets the [color](../../../objects/lights/parameters/index.md#color) modifier in the RGBA format for the projection that works like a filter. It can be useful when you need to artificially paint over the reflection in some color, or darken it. But if you need a physically correct reflection, then the color has to be strictly white. |
| Intensity | Sets the light color [multiplier](../../../objects/lights/parameters/index.md#intensity), which provides fine control over color intensity of the projection: - The minimum value of 0 removes projection brightness and makes it invisible. - Higher values make a more bright and intense color of projection. |
| Viewport Mask | Sets the *[Viewport](../../../objects/lights/parameters/index.md#viewport_mask)* mask for *Planar Reflection Probe*. |
| Visibility Distance | Distance from the camera in units, up to which reflected projection will be rendered. |
| Fade Distance | Distance from the camera in units, starting from which *Planar Reflection Probe* starts to fade out gradually. |
| Render on Water | Toggles rendering of reflections on the water surface. |
| Render on Transparent | Toggles rendering of reflections on transparent objects. |


### Planar Reflection Parameters


![](reflection_parameters.png)


| Reflection Viewport Mask | The *[Reflection Viewport](../../../principles/bit_masking/index.md#reflection_mask)* mask that controls rendering of *Planar Reflection Probe* reflections into the reflection camera viewport. Objects with matching viewport masks will be rendered. |
|---|---|
| Map Size | Specifies the reflection�s texture resolution in pixels. The texture is squared (height and width are equal). > **Notice:** Using high-resolution maps for reflections may significantly affect performance, as dynamic reflections are rendered each frame. |
| Two Sided | Enables projection for both sides. If this parameter is on, the reflection is projected on both sides of *Planar Reflection Probe* in opposite directions. |
| Stereo per Eye | Enables rendering of the reflection for each eye separately. > **Notice:** This option is very performance-consuming. |
| Roughness Samples | Sets the number of samples used to adjust quality of the blurring effect for the reflection on rough surfaces. - The lowest value of 0 means that the blurring of projection is made using only mipmaps. - Higher values result in better blurring quality, as more more randomized samples are used. > **Notice:** Rougher materials require more samples for smoother blurring reflection, but setting too high number of samples may cause a performance drop. |
| Roughness Visibility Min | Lower surface roughness limit, starting from which the reflection starts to fade out gradually. |
| Roughness Visibility Max | Upper surface roughness limit, starting from which the reflection completely disappears. |
| Distance Scale | Global distance multiplier within the range of [0.0f;1.0f] for the reflection [LODs](../../../content/optimization/geometry/lods/index.md) visibility distance. Distance Scale is applied to the distance measured from the reflection camera to the node (surface) bound. > **Notice:** This option enables rendering of less detailed LODs for reflections to increase performance. |
| Reflection Distance | The render distance for the reflection that specifies how far from the camera the reflection will be rendered. |
| Parallax | Degree of reflection distortion within the range of [0;1]. Distortion depends on an angle between the probe plane and the surface onto which the probe projects reflection. Increasing the value amplifies visual distortion as a result of increasing this angle. |
| Noise Intensity | Additional jitter for roughness samples that creates a noise effect on the reflection. Higher values make the noise effect more noticeable. |
| Reflection Offset | Z axis offset (relative to the probe local coordinate system) for the reflection. Can be used to change the viewpoint of the reflection camera moving it forward or backwards relative to the probe. |
| ZNear | Distance to the near clipping plane defining a frustum to be used for grabbing reflections. |
| ZFar | Distance to the far clipping plane defining a frustum to be used for grabbing reflections. > **Notice:** The higher the value, the more distant objects will be rendered; therefore, high values are not recommended due to possible performance hit. |
| Visibility Sky | Renders sky in the reflection. Can be used, when the reflection is supposed to reflect closeby objects only. |
