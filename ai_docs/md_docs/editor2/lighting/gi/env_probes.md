# Environment Probes


*[Environment Probe](../../../objects/lights/envprobe/index.md)* represents a reflection volume that stores a cubemap texture (pre-baked or dynamically changing each frame) to be rendered on reflective surfaces.


![](../../../migration/from_unity/unigine_env_probe.png)

*A reflective sphere placed inside anEnvironment Probe*


### See Also


- Light baking is available via code by using the *[BakeLighting](../../../api/library/lights/class.bakelighting_cpp.md)* Class.
- [Video Tutorial: Global Illumination](../../../videotutorials/essentials/global_illumination.md).
- Quick video guide: [How To Bake Reflections to *Environment Probes*](../../../videotutorials/how_to/how_to_rendering/env_probe.md).


## Cubemap Reflections


The primary application of Environment Probes is providing cube-mapped reflections.


The *[Projection Shape](../../../objects/lights/envprobe/index.md#common_params)* defines the type of projection to be used by the Environment Probe:


- **Box projection** - the cubemap is projected onto a box shape defined by the *Box Projection Size* parameter of the probe.
- **Spherical projection** - the cubemap is projected onto a spherical shape.


![](../../../migration/from_unity/unigine_envprobe_sphere.png) ![](../../../migration/from_unity/unigine_envprobe_box.png)


*Box projection is more suitable for box-shaped interiors.*


Spherical Environment Probes can be subject to *Parallax* effect controlled by the [corresponding parameter](../../../objects/lights/envprobe/index.md#light_reflection_parameters). With the value of 0 the reflection shall be projected onto an infinitesimally far sphere, the value of 1 corresponds to the actual probe's bounding sphere defined by the **Attenuation Distance** parameter taking into account the viewer's perspective.


![](../../../objects/lights/envprobe/parallax_0.jpg) ![](../../../objects/lights/envprobe/parallax_1.jpg)


The [Baking Settings](../../../objects/lights/envprobe/index.md#baking_settings) of the probe determine the type of reflections.


### Static Reflections


An Environment Probe with the **Dynamic option disabled** provides static reflections � the same cubemap is used until it is re-baked or replaced.


> **Notice:** It is not recommended to bake cubemaps for environment probes stored in multiple [*Node References*](../../../objects/nodes/reference/index.md) that refer to the same `.node` asset � the assigned cubemaps will be lost. However, you can export an environment probe to a node reference after baking and clone, if needed.


You can specify a custom cubemap texture for the probe or bake it from the environment by using the *[Bake Lighting](../../../editor2/lighting/gi/bake_lighting/index.md)* tool. For this purpose, a set of preparations is needed:


1. Select the **[Static Lighting Mode](../../../editor2/lighting/gi/index.md#lighting_modes)** for surfaces that should be visible in baked reflections or enable the *[Bake to Environment Probe](../../../editor2/node_parameters/visual_representation/index.md#bake_to_environment_probes)* option for surfaces in *Advanced Lighting Mode*. Disable it for dynamic objects. For selective group-based visibility of objects, adjust the *[Viewport Masks](../../../principles/bit_masking/index.md#viewport)*. A surface will be visible in reflections only if its *Viewport Mask* matches the *[Reflection Viewport Masks](../../../objects/lights/envprobe/index.md#baking_settings)* of the Environment Probe.
2. For [light sources](../../../editor2/lighting/lights/index.md#lights) that should be reflected, select the **Static** mode. *Dynamic* lights will be ignored.
3. Check **Grab by Bake Lighting** in the probe's Baking Settings. Adjust other settings, such as the desired cubemap resolution and the supersampling multiplier.
4. Open the *Bake Lighting* window.
5. Enable **Bake Environment Probes**. > **Notice:** Enable *Automatic Rebake* option to make cubemaps for static Environment Probes be automatically rebaked every time you make changes to their settings and transformation.
6. Select the *Number of Bounces*, i.e. the reflection depth. ![](env_bounce_0.png) ![](env_bounce_1.png)
7. Start baking process by clicking *Bake All Lighting* and wait for it to finish.
8. Upon completion, the generated cubemap will be saved in the `bake_lighting/env_probes` folder and assigned to the Environment Probe.


### Dynamic Reflections


Dynamic reflections imply the cubemap of an Environment Probe is grabbed each frame. This mode may make a massive load on the processing unit, so accurate adjustment of the Baking Settings is recommended.


To make an Environment Probe cast dynamic reflections, perform the following:


1. Check the **Dynamic** option for the probe.
2. Adjust the desired Resolution of the cubemap, supersampling and other Baking Settings.
3. Pay attention to the **Faces Per Frame** parameter defining the number of faces of the cubemap rendered each frame. Rendering six faces each frame may significantly affect the performance, so you can spread this number over several frames in a row.
4. Enable the *Dynamic Reflections* option: **Rendering -> Features -> Dynamic Reflections**


## Additional Features


### Ambient Lighting


By default, Environment Probes are used for reflections only, as for lighting, it is recommended to simulate it using *[Voxel Probes](../../../editor2/lighting/gi/voxel_probes.md)* and [lightmaps](../../../editor2/lighting/gi/lightmaps.md). However, cube-mapped [ambient lighting](../../../objects/lights/envprobe/index.md#light_reflection_parameters) by environment probes is available as well.


You can benefit from this approach by enabling the **Dynamic** option for the Environment Probes to get simple real-time global illumination.


![](gi_probes.gif)


### Additive Blending


More flexibility in lighting control is available with the *[Additive Blending](../../../objects/lights/envprobe/index.md#additive_blending)* mode. You can use it to blend reflections of several Environment Probes together and control them separately.


![](foxhole_additive_blending.gif)


### Use Sun Color


An Environment Probe is subject to multiplication by the sun light color if the *[Use Sun Color](../../../objects/lights/envprobe/index.md#use_sun_color)* option is enabled for it.


### Cutout By Shadow


In certain cases reflections baked into environment probes might be clearly seen in areas where they actually shouldn't, resulting in various artefacts that ruin the total look of your scene. This can be especially noticeable when you place environment probes in irregular shaped (non-squared) rooms. By using the **[Cutout By Shadow](../../../objects/lights/envprobe/index.md#cutout_by_shadow)** feature you can enable clipping of reflections occluded by obstacles.


![](cutout_off.jpg) ![](cutout_on.jpg)


To use the feature, perform the following steps:


1. Create meshes that will serve as obstacles for reflections propagation (doorways, windows, etc.).
2. Enable the **[Cast Environment Probe Shadows](../../../editor2/node_parameters/visual_representation/index.md#cast_envprobe_shadows)** flag for surfaces of obstacles.
3. Enable the **[Cutout By Shadow](../../../objects/lights/envprobe/index.md#cutout_by_shadow)** flag for the Environment Probe.
4. Bake the Environment Probe by using the *[Bake Lighting](../../../editor2/lighting/gi/bake_lighting/index.md)* window. This will create a depth texture that will be assigned to the probe and define clipping of reflections.
5. Disable or delete the obstacles.
