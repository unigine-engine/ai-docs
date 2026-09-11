# Grass Settings


The article describes all settings available in the ***Node*** tab of the *[Parameters](../../../editor2/node_parameters/index.md)* window for the grass node.


## Adding Grass


To add grass to the world, perform the following:


1. On the Menu bar, click *Create -> Grass -> Base*. ![](add_grass.png)
2. Place the grass object somewhere in the world. ![](added_grass.jpg)
3. Set the required grass parameters described [below](#params).


> **Notice:** See also the tutorial on *[Adding Grass](../../../objects/objects/grass/tutorial/index.md)* for a more detailed explanation on adding grass and setting its parameters.


## Grass Parameters


| Num textures | Sets a number of grass clusters (or plants, or flowers) lined up horizontally in the [diffuse texture](../../../content/materials/library/grass_base/index.md#texture_diffuse). Read more about this parameter [here](../../../objects/objects/grass/index.md#slots). > **Notice:** This value cannot exceed 4. |
|---|---|
| Size X | Specifies the length of the grass area along the X axis. |
| Size Y | Specifies the length of the grass area along the Y axis. |
| Step | Sets the size of the cells into which the grass field is divided. - A *larger* step value results in larger cells. However, there is a limit to the number of grass quads that can be generated per cell. Once this limit is reached, increasing the *[Density](#density)* parameter will not increase the number of grass quads. - A *smaller* step value results in smaller cells. Since the density value is applied per cell, reducing the cell size increases the overall grass density across the field. To learn more about the parameter, read the *[Step for Cell Division](../../../objects/objects/grass/index.md#step)* chapter of the *[Grass](../../../objects/objects/grass/index.md)* article. |
| Subdivision | Subdivides each cell into the specified number of parts. This is usually required when grass is used as a [low-poly distant LOD](../../../objects/objects/grass/index.md#low_poly_grass) of a forest created by using *[World Clutter](../../../objects/worlds/world_clutter/index.md)* or *[ObjectMeshClutter](../../../api/library/objects/class.objectmeshclutter_cpp.md)* with a smaller cell size: the *Subdivision* parameter subdivides large grass cells so that they match the smaller clutter cells. This way, positions of randomly scattered objects will coincide with positions of grass-based impostors. The range of available values is from 1 to 32. |
| Density | Determines how many grass quads are to be rendered per square unit taking into account the [step](#step) of division and the number of cells. > **Warning:** Increasing *Density* significantly raises RAM and VRAM usage. Therefore, when using values above **1.0** for large grass areas (more than 1 sq. km) make sure that you apply optimization techniques such as limiting the [visibility distance](../../../principles/world_management/index.md#visible), using [levels of detail](../../../objects/objects/grass/index.md#low_poly_grass) and enabling the grass [Thinning](#thinning) option. Otherwise, setting higher values can quickly result in excessive memory consumption. |


## Randomizing Grass


To randomize the appearance of grass quads, two types of values are used:


- **Mean value** (i.e. *[Aspect](#aspect), [Min/Max Bend](#bend), [Min/Max Height](#height), [Offset](#offset)*) defines the average value. With its help, the designer can set milestones to control the parameter.
- **Spread value** defines the range for a possible variation of the parameter. The higher the value, the more diverse the final result is. Spread value is *optional*: if set to 0, it does not influence the simulation process and only the mean value is uniformly used.


After these values are specified, the following formula is used to calculate the final result for the parameter:

Result = **Mean** + *Random* * **Spread**,  where *Random* is a random value in the range from -1 to 1. This means that the parameter differs for each grass quad on the field to the desired extent (see example with [Min and Max Height](#height) below).
**Spread** value is *optional*: if set to 0, it does not influence the simulation process and only the mean value is used for all objects.


| Variation | On the randomly chosen quads, flips the diffuse texture horizontally, automatically giving two variants available for rendering of varied blades. |  |  |
|---|---|---|---|
| Min Bend | Determines the **mean** grass quad sloping value in areas with the minimum density according to the [image mask](#mask). The *higher* the *Min Height* value, the more bent the grass is in areas with the minimum density. |  |  |
| **Max Bend** | Determines the **mean** grass quad sloping value in areas with the maximum density according to the [image mask](#mask). The *higher* the *Max Height* value, the more bent the grass is in areas with the maximum density. |  |  |
| Min Height | Determines the **mean** value for the height of grass blades quads rendered in areas with the minimum density according to the [image mask](#mask). The *higher* the *Min height* value, the higher the grass is in areas with the minimum density. \| ![](min_height_default.jpg) *Min height = 1; Spread = 0.3The grass height varies from 0.7 to 1.3* \| ![](min_height_custom.jpg) *Min height = 1.2; Spread = 1The grass height varies from 0.2 to 2.2* \| \|---\|---\| | ![](min_height_default.jpg) *Min height = 1; Spread = 0.3The grass height varies from 0.7 to 1.3* | ![](min_height_custom.jpg) *Min height = 1.2; Spread = 1The grass height varies from 0.2 to 2.2* |
| ![](min_height_default.jpg) *Min height = 1; Spread = 0.3The grass height varies from 0.7 to 1.3* | ![](min_height_custom.jpg) *Min height = 1.2; Spread = 1The grass height varies from 0.2 to 2.2* |  |  |
| Max Height | Determines the **mean** value for the height of grass blades quads rendered in areas with the maximum density according to the [image mask](#mask). The *higher* the *Max Height* value, the higher the grass is in areas with the maximum density. \| ![](max_height_default.jpg) *Max height = 3; Spread = 0.3The grass height varies from 2.7 to 3.3* \| ![](max_height_custom.jpg) *Max height = 3; Spread = 1The grass height varies from 2 to 4* \| \|---\|---\| | ![](max_height_default.jpg) *Max height = 3; Spread = 0.3The grass height varies from 2.7 to 3.3* | ![](max_height_custom.jpg) *Max height = 3; Spread = 1The grass height varies from 2 to 4* |
| ![](max_height_default.jpg) *Max height = 3; Spread = 0.3The grass height varies from 2.7 to 3.3* | ![](max_height_custom.jpg) *Max height = 3; Spread = 1The grass height varies from 2 to 4* |  |  |
| Aspect | Sets an aspect to calculate the width of a grass quad: *Width = Max height * Aspect* Aspect is set for each of the diffuse texture columns separately and can be randomly varied if the [spread](#spread) value is set in addition to [mean](#mean) one. |  |  |
| Offset | Specifies the offset in units up the surface normal, thus accurately repeating its relief. It is set by [mean](#mean) value (only positive) and additional [spread](#spread) value (positive or negative), if variation is required. |  |  |
| Rotation | It might be necessary to add more diversity via random rotation of grass quads. This parameter specifies the rotation of grass quads in degrees. It is set by [mean](#mean) value (only positive) and additional [spread](#spread) value (positive or negative), if variation is required. Values are set for each of the diffuse texture columns separately. |  |  |
| Probability | Sets the grass rendering probability per diffuse texture column. |  |  |
| Seed | Sets an integer value used to generate pseudo-random successions of numbers. The parameter is used to randomly position grass blades quads across an area by an image mask. > **Notice:** The same *Seed* value will always generate the same successions of numbers. To get a random seed value, press the **Randomize** button. |  |  |


## Masking Grass Areas


| Mask Image | Mask that determines the [density](#density) distribution of the grass. - The mask is a 4-channel (**RGBA8**) texture: > **Notice:** In case **R8, RG8** or **RGB8** texture is used as a mask, the [diffuse texture](../../../content/materials/library/grass_base/index.md#texture_diffuse) must have only one, two, or three columns. So, if your diffuse texture contains, for example, only one vertical column, the **R8** texture should be used. - **Red** channel specifies the areas of growth for the 1st texture column. If there are several grass clusters in a vertical column, they will be randomly spread across the masked area. - **Green** � for the 2nd texture column. - **Blue** � for the 3rd texture column. - **Alpha** � for the 4th texture column. - *Zero channel* values specify areas where the grass should not grow - *Non-zero channel* values create a grassy area: the *higher* the value, the denser the grass grows. |  |  |
|---|---|---|---|
| Threshold | Controls starting from what density (according to the mask), the grass should grow. This means, that if in some particular place the threshold value is *higher* than the color or alpha value of the mask, it is rendered grassless. - With the minimum value of 0, the grass is planted on the whole area, that is specified as available by the mask. - With *higher* threshold value, the grass will grow only in the areas marked by the mask as dense. The areas of sparse distribution stay bare. - With the maximum value of 1, there will be no grass at all. |  |  |
| Min Value | Image mask minimum value of the color density range. Read more [here](../../../objects/objects/grass/index.md#values). |  |  |
| Max Value | Image mask maximum value of the color density range. Read more [here](../../../objects/objects/grass/index.md#values). |  |  |
| Flip X | Flips an image mask horizontally. |  |  |
| Flip Y | Flips an image mask vertically. For example: \| ![](image_mask_not_flipped.jpg) *Grass growing according to original Image Mask* \| ![](image_mask_flip_y.jpg) *Grass growing according to Image Mask flipped vertically* \| \|---\|---\| After flipping the image mask by the Y axis, the grass has started growing on the stony area. Density and color of grass growing on the presented area have also changed. | ![](image_mask_not_flipped.jpg) *Grass growing according to original Image Mask* | ![](image_mask_flip_y.jpg) *Grass growing according to Image Mask flipped vertically* |
| ![](image_mask_not_flipped.jpg) *Grass growing according to original Image Mask* | ![](image_mask_flip_y.jpg) *Grass growing according to Image Mask flipped vertically* |  |  |
| Mesh Mask | Mesh-based mask that is used to specify areas where grass can grow. A mesh for masking should be a simple planar mesh. ![](mesh_mask.jpg) *Mesh used as a mask* |  |  |
| Terrain Mask | Four [Masks](../../../objects/objects/terrain/landscape_terrain/index.md#layers_masks) of the *[Landscape Terrain](../../../objects/objects/terrain/landscape_terrain/index.md)* each to be used to define the areas of growth for the corresponding [grass texture slot](../../../objects/objects/grass/index.md#slots) (grass type). If there are several grass clusters in a vertical column, they will be randomly spread across the masked area. |  |  |
| Inverse | Toggles the value that indicates if grass grows inside or outside the mesh contour. |  |  |
| Field Mask | - If used together with a *[Field Spacer](../../../objects/effects/fields/field_spacer/index.md)* object, the field mask specifies areas of the grass field that should not be rendered. - If used together with a *[Field Animation](../../../objects/effects/fields/field_animation/index.md)* object, the field mask specifies areas of the grass field that should be animated. > **Notice:** The field mask set for the grass object must match the *[Field Mask](../../../api/library/fields/class.field_cpp.md#getFieldMask_int)* of a *[Field](../../../objects/effects/fields/index.md)* node applied to the grass object. |  |  |
| Cutout Intersection | Cutout bit mask. This mask is used to cut out the grass in the areas of intersection with objects and decals (e.g. can be used to remove grass under houses or from the surface of roads projected using decals). The grass will be cut out by objects and decals that have their intersection masks matching this one (one bit at least). |  |  |
| Cutout Inverse | Toggles the value that indicates whether the grass should be rendered inside or outside the areas determined by the *[Cutout Intersection](#cutout_intersection)* mask. |  |  |


## Orienting Along the Relief


| Intersection | Flag indicating whether grass should follow the relief. |  |  |
|---|---|---|---|
| Orientation | Flag indicating whether grass polygons are oriented along the normal of its parent node (for example, terrain). \| ![](orientation_0.jpg) *Grass polygons oriented along normal of Grass object* \| ![](orientation_1.jpg) *Grass polygons oriented along normal of Terrain* \| \|---\|---\| Read more [here](../../../objects/objects/grass/index.md#orientation). | ![](orientation_0.jpg) *Grass polygons oriented along normal of Grass object* | ![](orientation_1.jpg) *Grass polygons oriented along normal of Terrain* |
| ![](orientation_0.jpg) *Grass polygons oriented along normal of Grass object* | ![](orientation_1.jpg) *Grass polygons oriented along normal of Terrain* |  |  |
| Angle | Sets the ground slope angle. - By the minimum value of 0, grass will grow everywhere on the ground. - The *bigger* the value is, the flatter the place should be for grass to grow. So, as the value is increased, steep slopes turn out to be bare at first, and then low-sloped places also become grassless. - By the maximum value of 1, grass will grow only on the strictly horizontal ground. |  |  |


## Optimizing Grass


| Thinning | Flag indicating whether grass is thinned out with a distance. - If the flag is set, random grass polygons are not rendered across the grass *[Fade](../../../principles/world_management/index.md#fading)* distance. - If the flag is not set, all grass polygons are rendered between the grass *[Visibility](../../../principles/world_management/index.md#visible)* distance and the *[Fade](../../../principles/world_management/index.md#fading)* distance. |
|---|---|
| Triangles | Counter that shows the total number of grass polygons. The shown values can be, for example, compared after changing some parameters in order to improve performance. |
