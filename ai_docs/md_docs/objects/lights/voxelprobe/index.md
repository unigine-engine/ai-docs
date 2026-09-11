# Voxel Probe


*Voxel Probe* is a light source which provides static voxel lighting and shading on an object inside *Voxel Probe* by using a prebaked 3D lighting map. *Voxel Probe* stores information on **indirect lighting (light bounces) only**, no direct lighting data at all. Unlike *[Environment Probe](../../../objects/lights/envprobe/index.md)*, *Voxel Probe* provides physically accurate light spreading inside interiors and outdoor static scenes but supports diffuse reflections only.


Also, *Voxel Probe* is great solution for [shading dynamic objects within static areas](#bake_volume).


[![](voxelprobe.png)](../voxelprobe.png)


> **Notice:** Surfaces with enabled [Lightmaps](../../../editor2/node_parameters/visual_representation/index.md#surface_lightmaps) are not illuminated by *Voxel Probe*.


### See Also


- The article on [Light Sources Parameters](../../../objects/lights/parameters/index.md)
- The *[LightVoxelProbe](../../../api/library/lights/class.lightvoxelprobe_cpp.md)* class to manage *Voxel Probe* via API


## Overview


*Voxel Probe* provides box volume composed of voxels and contains parameters used for [light baking](../../../editor2/lighting/gi/voxel_probes.md#bake) inside it.


![](voxel_grid.png)


*Voxel Probe* projects a 3D lighting texture on objects inside it thus providing indirect lighting simulation.


> **Notice:** For a transparent object (with [Alpha Blending](../../../editor2/materials_settings/index.md#blending) enabled) to be affected by *Voxel Probe*, you should toggle on the *[Multiple Environment Probes](../../../content/materials/library/mesh_base/index.md#multiple_env_probes)* state of its material and enable the **Multiple Environment Probes** feature (via *Rendering -> Transparent -> Multiple Environment Probes*).


The texture should have an appropriate resolution which is calculated the following way:


***Resolution = Width � Height � (Depth � 6)***


Each pixel of a texture defines the illuminance of a certain voxel face.


![](map.png)

*An example of a 3D lighting texture*


The inner space of *Voxel Probe* is visualized using spheres. These spheres are used to show the illumination in each voxel from all directions. The visualizer is disabled by default. To enable it, use the *Helpers* menu in Editor Viewport:


![](voxel_probe_v.gif)


*Voxel Probe* Visualizer settings:


- *Grid Size* � number of spheres in every row/column, the value from 7 to 40.
- *Sphere Scale* � size of the visualizing sphere.


*Voxel Probe* is a required object for the [Voxel-Based GI](../../../editor2/lighting/gi/voxel_probes.md) feature, which enables you to generate a lighting texture for *Voxel Probe* and simulate global illumination with indirect lighting for both, interiors and outdoor scenes.


[![](interior_sm.png)](interior.jpg)


> **Notice:** By default, *Voxel Probe* is used for lighting only; as for reflectons, it is recommended to simulate them using *[Environment Probe](../../../objects/lights/envprobe/index.md)*. This approach ensures the best result, however you can still [enable reflections for *Voxel Probe*](#reflections_parameters).


## Adding Voxel Probe


To add *Voxel Probe* to the scene via UnigineEditor, do the following:


1. On the Menu bar, click *Create -> Light -> Voxel Probe*. ![](create_voxelprobe.png)
2. Place *Voxel Probe* somewhere in the world.
3. [Bake Lighting](../../../editor2/lighting/gi/bake_lighting/index.md) or set the *[Texture](#texture_param)* parameter by choosing a prebaked lighting texture from assets.


> **Notice:** Use the **[Cast GI](../../../editor2/node_parameters/visual_representation/index.md#cast_gi)** option to define if a surface should be baked to *Voxel Probe*.


## Voxel Probe Settings


Parameters of *Voxel Probe* are available in the *Node* tab of the *[Parameters](../../../editor2/node_parameters/index.md)* window. It contains both the [common](../../../objects/lights/parameters/index.md) and the specific parameters. A set of parameters specific for *Voxel Probe* is described below.


> **Warning:** Do not use the ***Scale*** transform parameter to change *Voxel Probe* size as it causes visual artifacts.


![](parameters.png)

*Voxel Probeparameters*


### Common Parameters


![](parameters_common.png)


| Box Size | Specifies the size of the box volume. |
|---|---|
| Voxel Size | Sets the size of a voxel. > **Notice:** If the *Box Size* is not divisible to the *Voxel Size* without remainder, *Voxel Probe* uses the lowest volume of voxels covering the box. |


> **Notice:** These two parameters define the resolution of *Voxel Probe*. Note that the memory usage is cubically dependent on the resolution, double growth of the voxel size causes **eight-times** growth of the size of the lighting texture.


### Render Parameters


![](parameters_render.png)


| Color | Sets the light [color](../../../objects/lights/parameters/index.md#color) in the RGBA format. The color defines both the plausibility of virtual representation and its aesthetic component. |
|---|---|
| Intensity | Sets the light color [multiplier](../../../objects/lights/parameters/index.md#intensity), which provides fine control over color intensity of the emitted light: - The minimum value of 1 corresponds to the least saturated light color. - The maximum value of 100 equals the most bright and intense color. |
| Shadow Mask | The *[Shadow](../../../principles/bit_masking/index.md#shadow_mask)* mask controls rendering of a shadow cast by an object lit by a light source. |
| Viewport Mask | Sets the *[Viewport](../../../objects/lights/parameters/index.md#viewport_mask)* mask for the light. |
| Visibility Distance | Distance from the camera, in units, up to which *Voxel Probe* will be rendered. |
| Fade Distance | Distance from the camera, in units, starting from which *Voxel Probe* starts to fade out gradually. |
| Rendering Order | Defines the order in which ***Voxel Probes*** in *[Alfa Blend](../../../objects/lights/voxelprobe/index.md#additive_blending)* mode are rendered. A higher value means a higher priority. |
| Blend Mode | Toggles the blending mode for *Voxel Probe*. This option offers more flexibility in lighting control. The following modes are available: - **Alpha Blend** mode is used to blend several *Voxel Probe* nodes with the current node overlapping other *Voxel Probe* nodes. The node with a smaller voxel size has a higher priority. - **Additive** mode can be used to blend lighting of several *Voxel Probe* nodes together and control them separately (e.g. make a separate *Voxel Probe* for an indoor emissive light source and blend it with another *Voxel Probe* with lighting baked from the sky, having the ability to enable and disable them separately). - **Multiplicative** can be used to blend *Voxel Probe* imitating ambient occlusion with the indirect lighting available underneath the probe. In order to bake ambient occlusion to *Voxel Probe*, you can enable the [Multiply By Sky Color](#sun_color) option, bake the probe with one bounce, and disable that option. As a result, Voxel Probe will contain white color from the sky that may be used as ambient occlusion. > **Notice:** *Voxel Probe* with additive blending enabled cannot be used as an inset to add lighting details (e.g. creating a small high-detail *Voxel Probe* inside a large low-detail one). Such nodes do not replace each other, as they are blended instead. |
| Multiply By Sky Color | Enables the influence of [sky color](../../../editor2/settings/render_settings/environment/index.md#light_lut) on *Voxel Probe*. When enabled, this option makes the *Voxel Probe* color black at night, or orange at sunset. > **Notice:** To bake lighting from the sky separately with this option enabled, it is recommended to enable [baking visibility for the sky](#baking_visibility_sky) only, while disabling it for other light sources. > > > Changing this option requires the lighting to be re-baked. |


### Indirect Diffuse Parameters


![](parameters_ambient.png)


| Normal Bias | Offset for ambient lighting voxel projection along the normal to the surface. |
|---|---|
| Tangent Bias | Additional offset for voxel projection along the surface tangents. Adjusting this setting can help reduce light leaking in dark areas. |
| Translucent Indirect | Intensity of the translucent material's original diffuse lighting, as if its *Translucent* parameter were set to 0. Fine-tuning the current parameter can help correct artifacts caused by *[Translucent Soft Indirect](#DiffuseTranslucentSoftIndirect)*, such as excessive darkening on materials. |
| Translucent Soft Indirect | Intensity of soft diffuse lighting on the translucent material, calculated as the average illumination from all six directions. With such approach to lighting surface normals are not taken into account, thus increasing this value may result in a darker appearance than expected. However, this approach often produces a more realistic look, similar to the appearance of wax figures. |
| Cubic Filtering | Enables the cubic filtering of ambient lighting. > **Notice:** When disabled, the linear filtering is used. |


### Indirect Specular Parameters


![](parameters_reflections.png)


| Enabled | Enables reflections for *Voxel Probe*. By default, *Voxel Probe* is used for lighting only; as for reflectons, it is recommended to simulate them using *[Environment Probe](../../../objects/lights/envprobe/index.md)*. This approach ensures the best result, however you can still enable reflections for *Voxel Probe* via this option. |
|---|---|
| Visibility Roughness Min | Sets the lower bound of the roughness range within which the reflections of *Voxel Probe* are visible. |
| Visibility Roughness Max | Sets the higher bound of the roughness range within which the reflections of *Voxel Probe* are visible. > **Notice:** The roughness range helps to choose between diffuse reflection of the *Voxel Probe* and other ones (reflection from an environment probe, the environment cubemap) for all materials having the **Roughness** parameter. |
| Normal Bias | Specular reflections offset along the normal to the surface. |
| Tangent Bias | Additional offset for specular reflections along the surface tangents. Adjusting this setting can help reduce reflection leaking in dark areas. |
| Reflection Bias | Sets the specular reflections offset along the reflection vector. |
| Cubic Filtering | Enables the cubic filtering of reflection. > **Notice:** When disabled, the linear filtering is used. |


### Baking Settings


![](parameters_bake.png)


> **Notice:** The following parameters describe the way the light shall be baked inside *Voxel Probe*, so you need to re-bake lighting, when you make changes to these parameters.


| Baking Viewport Mask | Sets the baking *Viewport* mask which specifies the surfaces to be baked basing on their material's *[Viewport](../../../principles/bit_masking/index.md#viewport)* mask. |
|---|---|
| Far Clipping | Sets the distance to the far clipping plane used for every voxel during light baking. |
| Bake Internal Volume | Defines the mode of internal volume baking of *Voxel Probe*. - Full option corresponds to baking all voxels of *Voxel Probe* in the full resolution. - Half option corresponds to baking all voxels of *Voxel Probe* as follows: voxels that cover geometry are baked in the full resolution and empty voxels are baked in the half resolution. Having baked internal volume makes it possible to realistically shade dynamic objects that move inside *Voxel Probe* as the lighting texture is projected onto all the geometry. ![](../../../migration/from_unity/unigine_voxel_internal.gif) |
| Bake Quality | Defines the baking quality preset for *Voxel Probe*. - Draft option provides the highest iterativity with the lowest sampling quality and number of rays simulated. - Low option provides low sampling quality and number of light rays simulated. - Medium option corresponds to stable quality level which is good for most cases. - High option corresponds to high sampling quality and number of light rays simulated intended for release production. - Ultra baking quality might be useful to get rid of small inconsistencies on the release production. |
| > **Notice:** You can use the following 7 visibility options together with [additive blending](#additive_blending) to provide more flexibility in [light baking](../../../editor2/lighting/gi/bake_lighting/index.md). Thus, you can make *Voxel Probe* nodes independent of each other and combine them to produce some sort of dynamic GI effect. |  |
| Visibility Sky | Enables baking of lighting from the sky to *Voxel Probe*. |
| Visibility Light World | Enables baking of *[Light World](../../../objects/lights/world/index.md)* to *Voxel Probe*. |
| Visibility Light Omni | Enables baking of *[Light Omni](../../../objects/lights/omni/index.md)* to *Voxel Probe*. |
| Visibility Light Proj | Enables baking of *[Light Projected](../../../objects/lights/proj/index.md)* to *Voxel Probe*. |
| Visibility Voxel Probe | Enables baking of other *Voxel Probe* light sources to *Voxel Probe*. |
| Visibility Environment Probe | Enables baking of *[Environment Probe](../../../objects/lights/envprobe/index.md)* light sources to *Voxel Probe*. |
| Visibility Emission | Enables baking of [emission](../../../content/materials/library/mesh_base/index.md#option_emission) light sources to *Voxel Probe*. |
| Visibility Lightmap | Enables baking of [lightmapped surfaces](../../../editor2/lighting/gi/lightmaps.md) to *Voxel Probe*. |
| Texture | Sets the 3D lighting texture. > **Notice:** Every bake lighting procedure makes changes to the asset which is set for this parameter. > > > You can leave the field **empty** to avoid losing content. In this case a new generated lighting texture will be set for this parameter after the bake lighting procedure. Generated textures are stored in the `data/bake_lighting` folder. |
