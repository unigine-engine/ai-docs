# Mesh Clutter


**Mesh Clutter** is an object that can contain a great number of identical meshes which are positioned, oriented and scaled randomly and cannot be managed manually. Meshes of the *Mesh Clutter* object can be scattered in the certain areas by using an image or mesh mask.


The *Mesh Clutter* object is usually used for vegetation (for example, forest, leaves on the ground), for strewing identical objects (for example, rubbish).


*Mesh Clutter* is used to **scatter** identical meshes across the world (or the part of the world) or terrain. *Mesh Clutter* scatters objects procedurally, and renders only those objects which are in the viewing frustum. This allows to render the large number of meshes while keeping performance high.


[![](clutter_1_sm.png)](clutter_1.png)


> **Notice:** *Mesh Clutter* is always culled by the [Occlusion Query](../../../content/optimization/geometry/culling/index.md) and not rendered when outside the viewing frustum. At that, meshes of *Mesh Clutter* are not subject to culling via [Occluders](../../../objects/worlds/world_occluders/index.md).


### See also


- The *[ObjectMeshClutter](../../../api/library/objects/class.objectmeshclutter_cpp.md)* class to edit clutters via API
- The `Clutter` sample located in the `Art Samples` suite


## Creating Mesh Clutter


To create *Mesh Clutter*, simply perform the following steps:


1. On the Menu bar, click *Create -> Clutter -> Mesh*. ![](clutter_create.png)
2. In the dialog window that opens, choose the path to the `.mesh` file. This mesh would be used as the source one for the *Mesh Clutter*.
3. Place the *Mesh Clutter* object somewhere in the world.
4. Specify the [*Mesh Clutter* parameters](#params).


## Mesh Clutter Parameters


The *Mesh Clutter* is very much the same as *[World Clutter](../../../objects/worlds/world_clutter/index.md)* (that operates on different node references). It is rendered as a 2D grid, in each cell of which a number of meshes are randomly placed depending on the *Mesh Clutter* density and probability of appearing. The cells are generated one by one starting from the nearest ones. This approach allows to control how close or far the scattered objects are from each other and at the same time reduce the rendering load when the camera moves and farther cells become visible.


| Mesh | Mesh, the copies of which will be scattered. |
|---|---|
| Size X Size Y | The size of the *Mesh Clutter* bounding box along X and Y axis. Within this area objects will be scattered with specified density. - The size is measured in units. |
| Step for cells | Cell size in units. The resulting number of cells in the *Mesh Clutter* is defined in the following way: **[size](#size)** of the *Mesh Clutter* (both along *X* and *Y*) is divided by the step. - The *smaller* the step, the higher the number of cells is. |
| Density | Density specifies how many objects there are per square unit. - By the step of **1** unit, the density cannot be decreased lower than **1** (less than 1 object per square unit). - If the density value is too high, objects can be penetrating each other. |
| Visibility distance | Across the visibility distance the number of objects is strictly specified by the *[Density](#density)* parameter. It means that all objects that should be present are found in place. - If set to infinity (inf), the *[Fade Distance](#fade_distance)* parameter will be ignored. - The real radius of *Mesh Clutter* visibility directly depends on the object (surface) [maximum visibility distance](../../../principles/world_management/index.md#visible) and also its [fade out distance](../../../principles/world_management/index.md#fading). However, even in case it disappears at a closer distance, further increase of the visibility distance will affect performance, because cell generation-related calculations are still performed. - The visibility distance is actually measured up to the cell: when the camera moves on the specified distance form it, the cell is generated. Without the [fade distance](#fade_distance) or object [maximum visibility distance](../../../principles/world_management/index.md#visible), objects can be rendered per visible square. |
| Fade Distance | Across the fade distance the number of objects gradually decreases, as they disappear randomly one by one. Fade distance is measured starting from the *[Visibility Distance](#visible_distance)*. If fade distance is set, there is no clear line where the meshes abruptly disappear. Instead, a few of them will be left smoothly blend into the background without any visual noise. > **Notice:** For the best result, it is also recommended to combine this effect with [objects fade-out](../../../principles/world_management/index.md#fading). |
| Seed | The seed value for pseudo random number generator allows to create different patterns of automatic positioning. The seed is either be set manually or an engine provides a random value for a seed (**Randomize** option). |


## Randomizing Clutter Objects


To randomize the appearance of meshes scattered by *Mesh Clutter*, two types of values are used:


- **Mean value** (i.e., [Scale](#scale), [Offset](#offset), [Rotation](#rotation)) defines the average value. This is the basic value that will be randomly made higher or lower.
- **Spread value** defines the range for possible variation of the parameter. The higher the value, the more diverse the final result will be. Spread value is *optional*: if set to 0, it will not influence the simulation process and only the mean value will be used for all objects.


After these values are specified, each parameter is calculated according to the following formula: *Result = **Mean** + *Random* * **Spread***,
 where *Random* is a random value in range from -1 to 1. For example, if a mean value of the parameter equals 3 and a spread value equals 1, the final result will be any in range from 2 to 4.


| Min and Max Scale | The scale mean value of scattered objects depends on the minimum and maximum scale mean values and the [image mask](#mask) values: the mask values are used for linear interpolation between the minimum and maximum scale values. - The [mean](#mean) scale value cannot be negative. \| Min scale \| Sets the scale mean value for objects scattered in the areas with low density (according to the [image mask](#mask)). The higher the value, the bigger the objects will be in such areas. > **Notice:** When image mask is not set, this parameter isn't taken into account as the default mask stores only the [maximum mask values](#maximum_mask_value) (there are no areas with low density). \| \|---\|---\| \| Max scale \| Sets the scale mean value for objects scattered in the areas with high density (according to the [image mask](#mask)). The higher the value, the bigger the objects will be in such areas. \| For example, if the following image mask is used: ![](scale_image_mask.png) The *Mesh Clutter* objects will be scaled as follows: \| [![](min_max_scale_0_sm.png)](min_max_scale_0.png) \| [![](min_max_scale_1_sm.png)](min_max_scale_1.png) \| \|---\|---\| \| *Min scale = 1; Max scale = 3* \| *Min scale = 3; Max scale = 1* \| | Min scale | Sets the scale mean value for objects scattered in the areas with low density (according to the [image mask](#mask)). The higher the value, the bigger the objects will be in such areas. > **Notice:** When image mask is not set, this parameter isn't taken into account as the default mask stores only the [maximum mask values](#maximum_mask_value) (there are no areas with low density). | Max scale | Sets the scale mean value for objects scattered in the areas with high density (according to the [image mask](#mask)). The higher the value, the bigger the objects will be in such areas. | [![](min_max_scale_0_sm.png)](min_max_scale_0.png) | [![](min_max_scale_1_sm.png)](min_max_scale_1.png) | *Min scale = 1; Max scale = 3* | *Min scale = 3; Max scale = 1* |
|---|---|---|---|---|---|---|---|---|---|
| Min scale | Sets the scale mean value for objects scattered in the areas with low density (according to the [image mask](#mask)). The higher the value, the bigger the objects will be in such areas. > **Notice:** When image mask is not set, this parameter isn't taken into account as the default mask stores only the [maximum mask values](#maximum_mask_value) (there are no areas with low density). |  |  |  |  |  |  |  |  |
| Max scale | Sets the scale mean value for objects scattered in the areas with high density (according to the [image mask](#mask)). The higher the value, the bigger the objects will be in such areas. |  |  |  |  |  |  |  |  |
| [![](min_max_scale_0_sm.png)](min_max_scale_0.png) | [![](min_max_scale_1_sm.png)](min_max_scale_1.png) |  |  |  |  |  |  |  |  |
| *Min scale = 1; Max scale = 3* | *Min scale = 3; Max scale = 1* |  |  |  |  |  |  |  |  |
| Offset | Height offset parameter controls whether all objects are positioned at one height or some are found higher or lower. For example, with offset stones can be dug deep into the ground so that only a small top part is visible, or placed higher and look bigger. - The offset is measured in units. |  |  |  |  |  |  |  |  |
| Rotation X Rotation Y Rotation Z | These parameters allow to randomly orient the scattered objects. - The rotation is set in angles. - If a spread value is set to **180**, objects will be rotated by 360 degrees. |  |  |  |  |  |  |  |  |


## Masking Areas with Objects


Besides scattering the meshes evenly across the whole area, a mask for their positioning can be used. It controls where the meshes should be placed.


| Image Mask | Mask determines areas across which the objects are randomly scattered and areas where there will be no objects from the list. For example, on the terrain a mask allows to scatter stones across the rocky areas, while leaving the grassy ones free from rocks. > **Notice:** When the image mask is not set, the default mask with maximum mask values will be used. The maximum mask value is 255. - The mask is one-channel texture (*R8*). If there are more channels in the provided mask, they will be ignored. - *Zero* color value specify the areas without *Mesh Clutter* objects. - The *higher* (brighter) the color value is, the more objects there are in this area and the denser they are positioned. The size of objects is also affected: *brighter* color values make objects bigger, while *darker* ones reduce their size. - Color value of 255 means the density is as specified by the [corresponding parameter](#density). - Masking is done for all objects that are contained in the *Mesh Clutter* list. > **Notice:** To paint the image mask directly in the scene, use [*Mask Editor*](../../../editor2/mask_editor/index.md). |
|---|---|
| Threshold for mask | To control the strength of masking, a mask threshold is used. It checks the masked density for an area and if a threshold value is *higher* than the color value of the mask, objects are scattered across it. If the masked density is not enough, the places is left bare. - With the minimum value of 0, the mask is applied as it is. - With *higher* threshold value, the objects will be scattered only in areas marked by the mask as dense. Instead of sparse distribution, objects scattered here and there, they are likely to be rendered in dense isolated groups. - With the maximum value of 1, there will be no objects scattered at all. |
| Terrain Mask | [Mask](../../../objects/objects/terrain/landscape_terrain/index.md#layers_masks) of the *[Landscape Terrain](../../../objects/objects/terrain/landscape_terrain/index.md)* to be used to define the area where the *Mesh Clutter* object is to be placed. |
| Mesh Mask | A mesh-based mask can be used to place the objects. Vector masking makes it possible to create roads, rivers, etc. with extremely high precision regardless of the mask texture resolution. A mesh for masking should be a simple planar mesh.  ![](mesh_mask.jpg) *Mesh used as a mask* ![](mesh_masked.jpg) *Mesh-based masking* |
| Inverse | The *Inverse* flag toggles if the objects are placed inside or outside the mesh contour.  ![](mesh_mask_inverse.jpg) *Inverse masking* |
| Cutout Intersection | Cutout bit mask. This mask is used to cut out clutter meshes in the areas of intersection with objects and decals (e.g. can be used to remove vegetation under houses or from the surface of roads projected using decals). Clutter meshes will be cut out by objects and decals that have their intersection masks matching this one (one bit at least). |
| Cutout Inverse | Toggles the value that indicates whether the clutter meshes should be rendered inside or outside the areas determined by the [cutout intersection mask](#cutout_intersection). |


## Orienting along the Relief


*Mesh Clutter* can also scatter objects along the relief. For that, an underlying surface should be made a **parent** of the *Mesh Clutter* node. (If there are some nodes in the hierarchy between a terrain or mesh node and *Mesh Clutter*, intersections will still be checked.)


A parent for intersection can only be a [terrain](../../../objects/objects/terrain/index.md) or a **mesh** object. The mesh should be terrain-like, i.e. it should have only one surface vertically, along the Z coordinate.


> **Notice:** *Mesh Clutter* performs only one vertical intersection testing with parent **mesh** geometry. If there are surfaces underneath the upper surface, they will be ignored. For example, to scatter reference nodes across the whole sphere, two hemisphere meshes need to be used.


| Intersection | After the *Intersection* box is checked, objects will be scattered across the surface of the parent object. - It does not matter if the *Mesh Clutter* is bigger than the parent object in size � the scattering area will be still be limited to parent object surfaces. |
|---|---|
| Orientation | This option allows setting a parent surface normal vector as the initial orientation for scattered objects. It means, if the surface in some place is vertical, the *Up* direction for objects scattered over it will be actually pointing to the side. - They can be still randomly [rotated](#rotation) but relatively to the orientation of the parent normal. - This parameter is enabled only if the *[Intersection](#intersection)* option is checked. |
| Angle | Just like in the case with [grass](../../../objects/objects/grass/settings.md#angle), the scattering can take into account how steep the slope is. - By the minimum value of 0, it makes no difference how flat or how tilted the surface over which the *Mesh Clutter* objects are scattered. - The *bigger* the value is, the flatter the place should be for objects to be scattered over it. So, higher values make less steep surfaces bare. - By the maximum value of 1, the objects can be scattered only over perfectly horizontal surface. - This parameter is enabled only if the *[Intersection](#intersection)* option is checked. |


## Creating Mesh Clusters from Mesh Clutters


If you require more freedom in adjusting an existing *Mesh Clutter*, you can convert it to a *[mesh cluster](../../../objects/objects/mesh_cluster/index.md)* using the relevant [context-menu option](../../../objects/objects/mesh_cluster/index.md#cluster_from_clutter).


![](../mesh_cluster/cluster_from_clutter.png)
