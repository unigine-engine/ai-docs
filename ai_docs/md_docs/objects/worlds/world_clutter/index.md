# World Clutter


The **World Clutter** node allows **scattering** a set of identical nodes (node references) randomly across the scene practically in one click. There is no need any longer to position, scale, and rotate every single object by hand and constantly mind the performance factor. *World Clutter* automatically places nodes in the scene with random parameters, all of which can be efficiently controlled, and renders them only around the camera. *World Clutter* is used to scatter non-geometry objects, such as decals, particles systems, and so on. But if you want to scatter identical meshes, it is better to use [Mesh Clutter](../../../objects/objects/mesh_clutter/index.md).


*World Clutter* scatters objects procedurally and therefore even more memory-efficient. At the same time it means that scattered objects cannot be moved.


> **Notice:** *World Clutter* uses only [Reference Nodes](../../../objects/nodes/reference/index.md), because when the world is loaded they are scattered around the camera much faster.


[![](world_clutter_sm.jpg)](world_clutter.jpg)

*Scattered wood chips created usingWorld Clutter*


### See also


- The *[WorldClutter](../../../api/library/worlds/class.worldclutter_cpp.md)* class to edit *World Clutter* via API


## Creating a World Clutter


To create *World Clutter*, do the following:


1. Add a *World Clutter* node: in the [Menu](../../../editor2/interface/index.md#menu_bar), choose *Create -> Clutter -> Node*. ![](world_clutter_create.png)
2. Locate *World Clutter* on the scene.


## World Clutter Objects


Objects in *World Clutter* are node references that are scattered throughout a definite area and for each of which the probability of its appearing is controlled.


![Node references that are contained in the clutter](world_clutter_elements.png)

*List of node references inWorld Clutter*


| Probability slider | The *higher* the probability, the more often a node reference can be seen compared to other *World Clutter* objects. Let's say, we create a coast with wood chips and algae. We create wood chips decal and algae decal and save them as `*.node` files ([create a NodeReference file](../../../objects/nodes/reference/index.md#reference_creation)). If the probability slider for algae is near to zero, the coast is thick with wood chips and only several algae are seen among them. Changing the probability of appearing does not affect the number of rendered objects, it only specifies the proportion between several *World Clutter* objects. - If the probability is set to zero, the object is not rendered at all. - If there is only one object in *World Clutter*, the probability parameter (except when it equals zero) is ignored and the object occurrence depends solely on the [density](#density). |
|---|---|
| Add | Add a node reference to the list of *World Clutter* objects. |
| Remove | Delete ***all selected*** node references from the list. To select an object, a box near it should be checked. |
| Reload | Reload all the node references in *World Clutter*. After a node reference was edited, the saved changes are not automatically applied to the same nodes scattered by *World Clutter*. It happens because a reference node after being loaded once is copied from the internal cache, which allows creating a lot of copies really fast. Reload option updates this cache and the changes in objects parameters come in effect. |


## World Clutter Parameters


*World Clutter* is rendered as a 2D grid, in each cell of which a number of *World Clutter* objects are randomly placed depending on the *World Clutter* density and probability of appearing. The cells are generated one by one starting from the nearest ones. This approach allows to control how close or far the scattered objects are from each other and at the same time reduce the rendering load when the camera moves and farther cells become visible.


Once added and scattered, the objects cannot be moved or rotated. The only way to change the scattering pattern is to change the [seed](#seed).


| Size X Size Y | The size of the *World Clutter* bounding box along X and Y axis. Within this area objects will be scattered with specified density. The size is measured in units. |  |  |
|---|---|---|---|
| Step for Cells | Cell size in units. The number of cells in *World Clutter* is defined in the following way: **[size](#size)** of *World Clutter* (both along*X* and *Y*) is divided by the step. The higher the number of cells (i.e. the *smaller* the step), the higher the load. However, to create one large cell takes longer time. When the camera moves fast enough, small cells will be created very slow, but large ones can noticeably pop into sight and cause a small rendering lag. |  |  |
| Density | Density specifies how many objects there are per square unit. In case there is more than one object in *World Clutter*, [probability](#probability) will be taken into account, but will not change the resulting number of all rendered objects. If the density value is too high, objects can be penetrating each other. \| [![Lower Density](density_low_sm.jpg)](density_low.jpg) *Lower Density* \| [![Higher Density](density_high_sm.jpg)](density_high.jpg) *Higher Density* \| \|---\|---\| | [![Lower Density](density_low_sm.jpg)](density_low.jpg) *Lower Density* | [![Higher Density](density_high_sm.jpg)](density_high.jpg) *Higher Density* |
| [![Lower Density](density_low_sm.jpg)](density_low.jpg) *Lower Density* | [![Higher Density](density_high_sm.jpg)](density_high.jpg) *Higher Density* |  |  |
| Visibility Distance | Across the visibility distance the number of objects is strictly specified by the [density](#density) parameters. It means that all objects that should be present are found in place. - If set to inf, the *[Fade Distance](#fade_distance)* parameter will be ignored. - The real radius of *World Clutter* visibility directly depends on the object (surface) [maximum visibility distance](../../../principles/world_management/index.md#visible) and also its [fade out distance](../../../principles/world_management/index.md#fading). However, even in case it disappears at closer distance, further increase of the visible distance will carry performance penalty, because cell generation-related calculations are still performed. - The visibility distance is actually measured up to the cell: when the camera moves on the specified distance form it, the cell is generated. Without the *[Fade Distance](#fade_distance)* or the object *[Maximum Visibility Distance](../../../principles/world_management/index.md#visible)*, objects will be rendered in noticeable squares. |  |  |
| Fade Distance | Across the fade distance the number of objects gradually decreases, as they disappear randomly one by one. Fade distance is measured starting from the *[Visibility Distance](#visible_distance)*. If fade distance is set, there is no clear line where the objects that are contained in *World Clutter* abruptly disappear. Instead, a few of them will be left smoothly blend into the background without any visual noise. > **Notice:** For the best result, it is also recommended to combine this effect with [objects fade-out](../../../principles/world_management/index.md#fading). |  |  |
| Spawn Rate | Determines how many cells (in which *World Clutter* is rendered) are updated each frame. > **Notice:** Setting too high number of updated cells may lead to a performance spike. |  |  |
| Seed | The seed value for pseudo random number generator allows to create different patterns of automatic positioning. The seed is either be set manually or an engine provides a random value for a seed (**Randomize** option). |  |  |


## Randomizing World Clutter Objects


To randomize the appearance of objects that compose the *World Clutter*, two types of values are used:


- **Mean values** (*[Scale](#scale), [Offset](#offset), [Rotation](#rotation)*) define the average value. These are the basic values that will be randomly made higher or lower.
- **Spread values** (*Spread*) define the range for possible variation of the parameter. The higher the value, the more diverse the final result will be. The spread value is *optional*: if set to 0, it will not influence the simulation process and only the mean value will be used for all objects.


After these values are specified, each parameter is calculated according to the following formula:


Result = **Mean** + *Random* * **Spread**


where *Random* is a random value in range from -1 to 1. For example, if a *Mean* value of the parameter equals 3 and a *Spread* value equals 1, the final result will be any in range from 2 to 4.


| Scale | The scale mean value of scattered objects depends on the minimum and maximum scale mean values and the [image mask](#mask) values: the mask values are used to linearly interpolate between the minimum and maximum scale values. The [mean](#mean) scale value cannot be negative. \| Min Scale \| Sets the scale mean value for objects scattered in the areas with low density (according to the [image mask](#mask)). The higher the value, the bigger the objects will be in such areas. > **Notice:** When image mask is not set, this parameter isn't taken into account as the default mask stores only the [maximum mask values](#maximum_mask_value) (there are no areas with low density). \| \|---\|---\| \| Max Scale \| Sets the scale mean value for objects scattered in the areas with high density (according to the [image mask](#mask)). The higher the value, the bigger the objects will be in such areas. \| | Min Scale | Sets the scale mean value for objects scattered in the areas with low density (according to the [image mask](#mask)). The higher the value, the bigger the objects will be in such areas. > **Notice:** When image mask is not set, this parameter isn't taken into account as the default mask stores only the [maximum mask values](#maximum_mask_value) (there are no areas with low density). | Max Scale | Sets the scale mean value for objects scattered in the areas with high density (according to the [image mask](#mask)). The higher the value, the bigger the objects will be in such areas. |
|---|---|---|---|---|---|
| Min Scale | Sets the scale mean value for objects scattered in the areas with low density (according to the [image mask](#mask)). The higher the value, the bigger the objects will be in such areas. > **Notice:** When image mask is not set, this parameter isn't taken into account as the default mask stores only the [maximum mask values](#maximum_mask_value) (there are no areas with low density). |  |  |  |  |
| Max Scale | Sets the scale mean value for objects scattered in the areas with high density (according to the [image mask](#mask)). The higher the value, the bigger the objects will be in such areas. |  |  |  |  |
| Offset | Height offset parameter controls whether all objects are positioned at one height or some are found higher or lower. For example, with offset stones can be dug deep into the ground so that only a small top part is visible, or placed higher and look bigger. The offset is measured in units. |  |  |  |  |
| Rotation�X Rotation�Y Rotation�Z | These parameters allow to randomly orient the scattered objects. The rotation is set in angles. If a spread value is set to 180, objects will be rotated by 360 degrees. |  |  |  |  |


## Masking Areas with Objects


Having objects uniformly scattered in all directions and places is naturally not very convenient. Instead of creating a number of small *World Clutter* nodes that cover a limited location, a big one can be used with a mask.


| Image Mask | Areas across which the objects are randomly scattered and areas without any objects from the list. For example, on the terrain, a mask allows to scatter debris across certain areas, while leaving other places free of it. > **Notice:** When the image mask is not set, the default mask with maximum mask values will be used. The maximum mask value is 255. - The mask is one-channel texture (R8). If there are more channels in the provided mask, they will be ignored. - Zero color value specify the areas without *World Clutter* objects. - The *higher* the color value is, the more objects there are in this area and the denser they are positioned. - Color value of 255 means the density is as specified in by the [corresponding parameter](#density). - Masking is done for all objects that are contained in *World Clutter* list. ![World Clutter mask for scattering](mask.jpg) > **Notice:** To paint the image mask directly in the scene, use *[Mask Editor](../../../editor2/mask_editor/index.md)*. |  |  |
|---|---|---|---|
| Threshold for Mask | To control the strength of masking, a mask threshold is used. It checks the masked density for an area and if a threshold value is *higher* than the color value of the mask, objects are scattered across it. If the masked density is not enough, the place is left bare. - With the minimum value of 0, the mask is applied as it is. - With a *higher* threshold value, the objects are scattered only in areas marked by the mask as dense. Instead of sparse distribution, objects scattered here and there, they are likely to be rendered in dense isolated groups. - With the maximum value of 1, there will be no objects scattered at all. \| [![Minimum Threshold](threshold_0_sm.jpg)](threshold_0.jpg) *Threshold = 0* \| [![Maximum Threshold](threshold_1_sm.jpg)](threshold_1.jpg) *Threshold = 1* \| \|---\|---\| | [![Minimum Threshold](threshold_0_sm.jpg)](threshold_0.jpg) *Threshold = 0* | [![Maximum Threshold](threshold_1_sm.jpg)](threshold_1.jpg) *Threshold = 1* |
| [![Minimum Threshold](threshold_0_sm.jpg)](threshold_0.jpg) *Threshold = 0* | [![Maximum Threshold](threshold_1_sm.jpg)](threshold_1.jpg) *Threshold = 1* |  |  |
| Mesh Mask | A mesh-based mask can be used to place objects. Vector masking makes it possible not to depend on the mask texture resolution, and create roads, rivers, etc. with extremely high precision. A mesh for masking should be a simple planar mesh. |  |  |
| Inverse | Toggling the flag makes the objects be placed within or outside the mesh contour. |  |  |
| Min and Max mask values | As a solution for advanced objects distribution and memory consumption optimization, not only a whole mask, but any required part of it can be applied to the object. It means that different objects can share the same mask, but use different levels. By default, each channel of the [Image Mask](#mask) specifies the areas and the density of growth in the [0;255] color density range. However, by using the minimum and the maximum value, you can specify any color density range within, and the part of the mask that contains the corresponding values will be used to scatter the nodes. Let's take the following R8 [Image Mask](#mask) as an example: ![](image_mask.png) Several objects that represent nodes of different heights can share this mask as follows: - In range from 100 to 200 density one type of nodes can be stored. - In range from 190 to 255 density another type of nodes can be stored. |  |  |
| Flip X | Horizontal flip of the [Image Mask](#mask). |  |  |
| Flip Y | Vertical flip of the [Image Mask](#mask). |  |  |
| Cutout Intersection | Cutout bit mask. This mask is used to cut out *World Clutter* objects in the areas of intersection with objects and decals (e.g. to remove vegetation under houses or from the surface of roads projected using decals). *World Clutter* objects are cut out by objects and decals that have their *Intersection* masks matching this one (one bit at least). |  |  |
| Cutout Inverse | Toggles the value that indicates whether *World Clutter* objects should be rendered inside or outside the areas determined by the [cutout intersection](#cutout_intersection) mask. |  |  |


## Orienting along the Relief


Unless objects in *World Clutter* are scattered over a completely flat and non-tilted surface, they can be automatically positioned to precisely repeat ups and downs of the relief without any effort. For that, an underlying surface should be made a **parent** of the *World Clutter* node. (If there are some nodes in the hierarchy between a terrain or mesh node and *World Clutter*, intersections will still be checked.)


A parent for intersection can only be a [terrain](../../../objects/objects/terrain/index.md) or a **mesh** object. The mesh should be terrain-like, i.e. it should have only one surface vertically, along the Z coordinate.


> **Notice:** *World Clutter* performs only one vertical intersection testing with parent **mesh** geometry. If there are surfaces underneath the upper surface, they will be ignored. For example, to scatter reference nodes across the whole sphere, two hemisphere meshes need to be used.


| Intersection | After the *Intersection* box is checked, objects in *World Clutter* are scattered across the surface of the parent object. It does not matter if *World Clutter* is bigger than the parent object in size � the scattering area will still be limited to parent object surfaces. |  |  |
|---|---|---|---|
| Orientation | This option allows setting a parent surface normal vector as the initial orientation for scattered objects. It means if the surface in some place is vertical, the *up* direction for objects scattered over it will be actually pointing to the side. The objects can be still randomly [rotated](#rotation) but relatively to the orientation of the parent normal. This parameter is enabled only if the *[Intersection](#intersection)* option is enabled. \| [![Orientation disabled](orientation_0_sm.jpg)](orientation_0.jpg) *Orientation disabled* \| [![Orientation enabled](orientation_1_sm.jpg)](orientation_1.jpg) *Orientation enabled* \| \|---\|---\| | [![Orientation disabled](orientation_0_sm.jpg)](orientation_0.jpg) *Orientation disabled* | [![Orientation enabled](orientation_1_sm.jpg)](orientation_1.jpg) *Orientation enabled* |
| [![Orientation disabled](orientation_0_sm.jpg)](orientation_0.jpg) *Orientation disabled* | [![Orientation enabled](orientation_1_sm.jpg)](orientation_1.jpg) *Orientation enabled* |  |  |
| Angle | Just like in the case with [grass](../../../objects/objects/grass/settings.md#angle), scattering can take into account how steep the slope is. - By the minimum value of 0, it makes no difference how flat or how tilted the surface over which *World Clutter* objects are scattered. - The *bigger* the value, the flatter the place should be for objects to be scattered over it. So, higher values make less steep surfaces bare. - By the maximum value of 1, the objects can be scattered only over perfectly horizontal surface. This parameter is enabled only if the *[Intersection](#intersection)* option is checked. |  |  |
