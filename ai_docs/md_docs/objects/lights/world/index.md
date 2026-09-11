# Light World


**Light World** is an infinitely remote light source casting orthographically projected beams onto the scene. The shadows cast by this light are parallel, which provides a realistic simulation of the sunlight.


![](world_light_index.png)


*Light World* shadows have an *adaptive bias* that is adjusted automatically on shadow maps applying: depending on the slope angle of *Light World* and its resolution, an offset of the depth value stored in the shadow map is calculated.


### See Also


- The *[LightWorld](../../../api/library/lights/class.lightworld_cpp.md)* class to manage *Light World* via API
- The part of the Lighting video tutorial dedicated to [working with *Light World*](https://youtu.be/6PNOp963S4U?t=207)
- The article on *Light World* [scattering](../../../editor2/lighting/environment.md#scattering)


## Adding World Light


To add *Light World* to the scene via UnigineEditor, do the following:


1. [Run](../../../sdk/projects/index_cpp.md#run) the project with UnigineEditor.
2. On the Menu bar, click *Create -> Light -> World*. ![](create_world.png)
3. Place *Light World* somewhere in the world. > **Notice:** The physical position of the source is not important, only the direction matters, as it defines the shadow casting orientation. To change the light's direction use the [rotation manipulator](../../../editor2/select_position_nodes/index.md#rotate_object).
4. Adjust the *Light World* [settings](#settings).


## World Light Settings


The following set of options is available for *Light World* in the *Node* tab of the *[Parameters](../../../editor2/node_parameters/index.md)* window. It includes both the [common parameters](../../../objects/lights/parameters/index.md) and the parameters specific for *Light World*. The specific ones are described below.


### Light Settings


![](light_settings.png)


| Disable Angle | The angle between the light source and the zenith at which the light source is disabled (shadows and the diffuse component is disabled). However, the light source still affects scattering. |  |  |  |  |
|---|---|---|---|---|---|
| Scattering | A lighting type: - **None** � render the atmosphere as if there were no global lights, that is, there will be no sky color gradient in any direction. - **Sun** � render the atmosphere in accordance with the Sun's lighting. - **Moon** � render the atmosphere in accordance with the Moon's lighting. > **Notice:** [Light scattering](../../../editor2/lighting/environment.md#scattering) is defined by a combination of [environment scattering LUTs (Look-Up Textures)](../../../editor2/settings/render_settings/environment/index.md#lut_settings) describing different states of the sky during the day. The atmosphere is rendered based on interpolation between these LUTs. \| ![](world_scattering_0.png) \| ![](world_scattering_1.png) \| \|---\|---\| \| *Scattering = Sun* \| *Scattering = Moon* \| | ![](world_scattering_0.png) | ![](world_scattering_1.png) | *Scattering = Sun* | *Scattering = Moon* |
| ![](world_scattering_0.png) | ![](world_scattering_1.png) |  |  |  |  |
| *Scattering = Sun* | *Scattering = Moon* |  |  |  |  |


### Shadow Settings


![](shadow_settings_.png)


| Shadow | Enables or disables the [PSSM](../../../principles/render/lights_shadows/shadows/pssm.md) technique. |  |  |  |  |
|---|---|---|---|---|---|
| Cascade Mode | Shadow cascade generation mode to be used (available for the *Static* [light mode](../../../objects/lights/parameters/index.md#light_mode) only): - **Dynamic** � In this mode shadow cascades are built dynamically relative to the camera position making it possible to change the time of day (day-night cycle). - **Static** � In this mode shadow cascades are built relative to the light source position and baked. This mode is suitable as a performance optimization technique for small-area ArchViz projects where shadow cascades can be divided into 2 sections: walkable area with high-resolution shadows (as they're observed closely) and non-walkable area with low-resolution shadows (as they're observed from a distance). > **Notice:** - Changing the time of day is not available in this mode, as shadow cascades are baked. > - Shadows cast by transparent surfaces cannot be baked. To make such shadows visible when any light-baking mode is enabled, configure the transparent surfaces: toggle the dynamic lighting mode for them (Surface -> Rendering -> Lighting Mode -> Dynamic). |  |  |  |  |
| One Cascade Per Frame | Toggles the One Cascade Per Frame mode on and off. This mode distributes the update of shadow cascades across multiple rendering frames: shadows from static geometry are rendered into only one cascade per frame. > **Notice:** Shadows cast by transparent surfaces cannot be baked. To make such shadows visible when any light-baking mode is enabled, configure the transparent surfaces: toggle the dynamic lighting mode for them (Surface -> Rendering -> Lighting Mode -> Dynamic). |  |  |  |  |
| Visibility Distance | Distance at which shadows from the light source start fading out until they are completely invisible. Distance up to which shadows are rendered is defined by the *[Max Visibility Distance](../../../editor2/settings/render_settings/shadows/index.md#distance)* setting. |  |  |  |  |
| Resolution | Size of the [shadow map](../../../objects/lights/parameters/index.md#resolution) that defines shadow quality. |  |  |  |  |
| Number of cascades | A number of cascades with different shadow maps. Each cascade requires a separate rendering pass. All the shadow maps have the same resolution (the **Shadow Resolution** parameter value), but are applied to different cascades. Thus, close-range shadows are of higher quality and distant ones of lower. The minimum number of cascades is 1, the maximum is 4. Increasing the number of cascades enhances the rendered image quality. However, at that, performance efficiency drops. > **Notice:** To visualize the cascades, enable *[Helpers](../../../editor2/using_visual_helpers/index.md) -> Shadow cascades*. In Static cascade mode, shadow cascades are additionally visualized by the boxes that define the shadow area. \| Cascade Mode: *Static* \| Cascade Mode: *Dynamic* \| \|---\|---\| \| ![](world_cascades_static_0.png) ![](world_cascades_static_1.png) \| ![](world_cascades_0.png) ![](world_cascades_1.png) \| | Cascade Mode: *Static* | Cascade Mode: *Dynamic* | ![](world_cascades_static_0.png) ![](world_cascades_static_1.png) | ![](world_cascades_0.png) ![](world_cascades_1.png) |
| Cascade Mode: *Static* | Cascade Mode: *Dynamic* |  |  |  |  |
| ![](world_cascades_static_0.png) ![](world_cascades_static_1.png) | ![](world_cascades_0.png) ![](world_cascades_1.png) |  |  |  |  |
| Cascade border | A multiplier for the distance to the border of the cascade in range [0;1]. **Distance to the border** depends on the *[Cascade Mode](#shadow_cascade_mode)* and is set as follows: - For *Dynamic mode* � corresponds to the *[Shadows Max Visibility Distance](../../../editor2/settings/render_settings/shadows/index.md#distance)* value and is measured from the *Camera* position. - For *Static mode* � is defined by the dimensions of the [shadow area box](#static_shadow_cascade_mode_settings) projection and measured from the *Light World* position. The number of cascade borders depends on the number of cascades: - For one cascade, there is no cascade border. - For 4 cascades, there are 3 cascade borders (for the first three cascades). For the last cascade, the multiplier is always 1. Setting the cascade borders allows you to accurately adapt the quality of the shadows depending on their remoteness from the viewer. - *Decreasing* the multiplier value makes the cascade smaller, more compact positioned and covering less distance. At the same time, the resulting shadow is of a higher quality. - *Increasing* the multiplier value makes the cascade larger with broader coverage of the area. \| ![](world_border_0.png) \| ![](world_border_1.png) \| \|---\|---\| \| *Cascade border 0 = 0.02 (shadow of higher quality)* \| *Cascade border 0 = 0.1* \| | ![](world_border_0.png) | ![](world_border_1.png) | *Cascade border 0 = 0.02 (shadow of higher quality)* | *Cascade border 0 = 0.1* |
| ![](world_border_0.png) | ![](world_border_1.png) |  |  |  |  |
| *Cascade border 0 = 0.02 (shadow of higher quality)* | *Cascade border 0 = 0.1* |  |  |  |  |


Enabling *[Static Cascade Mode](#shadow_cascade_mode)* makes extra parameters available. In addition to the [static shadow parameters common for all light sources](../../../objects/lights/parameters/index.md#shadow_settings), there are parameters that define the size of the box within which the static shadows are rendered:


| Height | Size of the shadow area box along the X axis. |
|---|---|
| Width | Size of the shadow area box along the Y axis. |
| ZFar | Distance from the light source position along the light direction vector. > **Notice:** Ensure that *ZFar* distance is big enough to have both objects and surfaces that take shadows within the shadow area box. ![](zfar_0.png) ![](zfar_1.png) |
