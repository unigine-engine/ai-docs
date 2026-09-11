# Grass


**Grass** is rendered as a set of 2D textures (blades), each representing a small grass tuft. Grass diversity is achieved by the probabilistic factor that influences the grass blades height, offset, color, etc., which grants convincing illusion of natural variation with fine details, while not monopolizing the GPU. Grass can be animated, which makes it realistically sway in the wind.


[![](grass_field_sm.jpg)](grass_field.jpg)


### See Also


- The *[Adding Grass](../../../objects/objects/grass/tutorial/index.md)* tutorial
- The article on *[Grass Settings](../../../objects/objects/grass/settings.md)*
- The *[grass_base](../../../content/materials/library/grass_base/index.md)* material to adjust the grass appearance
- The *[ObjectGrass](../../../api/library/objects/class.objectgrass_cpp.md)* class to edit grass via API


## Adding Grass


To add grass to the world, perform the following:


1. On the Menu bar, click *Create -> Grass -> Base*. ![](add_grass.png)
2. Place the object somewhere in the world. ![](added_grass.jpg)


The default grass field would appear with the *[grass_base](../../../content/materials/library/grass_base/index.md)* material assigned.


## Rendering Grass


Rendering of grass mostly depends on two textures:


- **[Diffuse](../../../content/materials/library/grass_base/index.md#texture_diffuse)** texture defines the grass shape and color.
- **[Mask](#mask)** texture determines grass mapping and density distribution on the terrain.


For convenience, the diffuse texture is subdivided into chunks. Each chunk is rendered depending on the used mask values. To utilize maximum variations of grass species, chunks are placed in the texture as follows:


- The horizontal row can have up to 4 chunks. Each chunk corresponds to the red, green, blue, and alpha channels of the mask. ![](chunk.png)
- The number of chunks in the vertical column can be from 1 to 4. Chunks in the column represent variations of grass for the corresponding mask channel. Usually, each channel corresponds to the particular species of grass (thiner, thicker, tangled, etc.). If there are several grass clusters in a vertical column, they are randomly spread across the masked area. For the texture to be split into the correct number of chunks, the number of chunks that you've used per column should be specified in the *[Num Textures](#slots)* field. For example, for the diffuse texture below, *Num Textures = 4* should be specified. ![](variation.png)


| Texture | Type | Setting |
|---|---|---|
| Diffuse | RGBA: - RGB values store the grass color information. - A value stores transparency information and defines which parts of the grass chunks will be rendered colored and which ones will be cut by alpha testing. | Set in the *Textures* tab of the *[grass_base](../../../content/materials/library/grass_base/index.md)* material. |
| Mask | RGBA8: each channel controls distribution of the chunks in the vertical column of the grass diffuse texture. - Red channel specifies the areas of growth for the 1st texture column. - Green � for the 2nd texture column. - Blue � for the 3rd texture column. - Alpha � for the 4th texture column. > **Notice:** In case R8, RG8, or RGB8 texture is used as a mask, the [diffuse texture](../../../content/materials/library/grass_base/index.md#texture_diffuse) must have only one, two, or three columns. So, if your diffuse texture contains, for example, only 1 vertical column, the R8 texture should be used. 0 mask channel values (no color) create areas where grass should not grow. Non-zero channel values create a grassy area: the higher the value, the denser grass grows. If the mask texture is not set, the default white texture is used. It doesn't have a predefined amount of channels: the type of this texture depends on the value set in the *Num Textures* field. So, if *Num Textures = 2*, the default mask texture will be RG8. | Set in the *ObjectGrass -> Node* tab -> *Grass* section - > *Mask Image* field. |


For example, we have the following diffuse and mask textures:


| ![](grass_variation_diffuse_sm.png) *Diffuse texture* | ![](mask.png) *RBG and A channels of the mask* |
|---|---|


We see that in the first column, chunks of the green shades correspond to the red channel of the mask, which is 9 red rhombuses; in the second column, chunks of the real grass variation correspond to the green channel of the mask, which is the square green mask frame; in the third column, chunks of the red shades correspond to the blue channel of the mask, which is the blue rhombuses frames; and in the fourth column, chunks of the yellow shades correspond to the alpha channel of the mask, which is the rest black areas (note that these parts won't re rendered, as there no alpha color data).


The result will be as follows:


![](result.png)


## Randomizing Grass


To randomize appearance of grass blades, two types of values are used:


- **Mean Value** (set in the main field of the parameter: *[Min/Max Bend](#bend), [Min/Max Height](#height), [Aspect](#aspect), [Offset](#offset)*) defines the average value of distribution. Four fields correspond to the red, green, blue, and alpha channels of the diffuse texture correspondingly. Using this value, the designer can set milestones to control the parameter.
- **Spread Value** defines the range for possible variation of the parameter. Four fields correspond to the red, green, blue, and alpha channels of the diffuse texture correspondingly. The higher the value, the more diverse the final result is. > **Notice:** The spread value is optional: if set to 0, it does not affect the simulation process. In such a case, only the mean value is uniformly used.


An example of using the *Spread Value* is provided for the *[Min/Max Height](#height)* parameter. It is applied similarly to the *[Min/Max Bend](#bend), [Aspect](#aspect)*, and *[Offset](#offset)* parameters.


![](mean_spread.png)

*Mean and spread values of the grass randomization parameters*


### Probability


The probability of appearance of the grass chunk belonging to a specific mask channel (horizontal row) depends on the *Probability* parameter. The variations of the specie (vertical column) are rendered randomly.


![](probability.png)

*Probability of appearance of the grass slots belonging to the red, green, blue, and alpha channels of the mask correspondingly*


Let's check several variations of the *Probability* parameter for the following diffuse texture:


![](diffuse_1.png)


The default RGBA8 white texture is used as a mask (as there are 4 chunks in the diffuse texture, we set *Num Textures* to 4). The mask value is *white = 1*, therefore, the whole grass area is filled.


In the pictures below, different variations of the *Probability* parameter are shown:


| ![](probability_0.png) *Probability = 1 1 1 1* | ![](probability_1.png) *Probability = 0.1 0 0 1* |
|---|---|


| ![](probability_3.png) *Probability = 0 1 0 1* | ![](probability_2.png) *Probability = 0.1 0.3 0.7 1* |
|---|---|


### Min/Max Bend


Bending means sloping of a grass quad forward or backward at a certain angle.


![](bend_0.png) ![](bend_1.png)


**Min Bend** is the [mean](#mean) grass quad sloping value in areas with the lowest density according to the [mask](#mask). **Max Bend** is the [mean](#mean) grass quad sloping value in areas with the highest density according to the [mask](#mask). Both *Min/Max Bend* and their [spread](#spread) values are set for each diffuse texture column separately.


### Min/Max Height


**Min Height** is the [mean](#mean) grass height value in areas with the lowest density according to the [mask](#mask). **Max Height** is the [mean](#mean) grass height value in areas with the highest density according to the [mask](#mask). Both *Min/Max Height* and their [spread](#spread) values are set for each diffuse texture column separately.


Let's compare the following examples:


| If we set the *Min Height* value equal to 1 with the *Spread* value of 0.3, the height interval for the grass in the areas with the lowest density is from 0.7 (i.e., 1�-�0.3) to 1.3 (i.e., 1�+�0.3), meaning that each grass quad has its own height selected randomly from this interval. | With the Min Height value equal to 1.2 and the Spread value of 1, the height interval for the grass in the areas with the lowest density is from 0.2 (i.e., 1.2�-�1) to 2.2 (i.e., 1.2�+�1), meaning that each grass quad has its own height selected randomly from this interval. |
|---|---|
| ![](min_height_default.jpg) *Min Height = 1; Spread = 0.3* | ![](min_height_custom.jpg) *Min Height = 1.2; Spread = 1* |


It works the same way for *Max Height*.


| For the *Max Height* value equal to 3 and the Spread value equal to 0.3, the height interval for the grass in the areas with the highest density is from 2.7 (i.e., 3�-�0.3) to 3.3 (i.e., 3�+�0.3), meaning that each grass quad has its own height selected randomly from this interval. | For the *Max Height* value equal to 3 and the Spread value equal to 1, the height interval for the grass in the areas with the highest density is from 2 (i.e., 3�-�1) to 4 (i.e., 3�+�1), meaning that each grass quad has its own height selected randomly from this interval. |
|---|---|
| ![](max_height_default.jpg) *Max Height = 3; Spread = 0.3* | ![](max_height_custom.jpg) *Max Height = 3; Spread = 1* |


### Aspect


To render the intended grass quad, in addition to the height, it should also have the width set. To preserve the proportions of the quad, width is not specified directly, but rather using the aspect parameter. So the final **width** is calculated by multiplying *[Max Height](../../../objects/objects/grass/settings.md#height)* by *Aspect*.


*Aspect* is set for each diffuse texture column separately. Like the *[Height](#height)* parameter, *Aspect* can be randomly varied if the *[Spread](../../../objects/objects/grass/settings.md#random)* value is set in addition to the *[Mean](../../../objects/objects/grass/settings.md#random)* value. For example, setting spread to 0 yields the following result:


- If the mean value is set to 1, grass is rendered in square proportions, with the height equal to the width.
- If the mean value is set to 2, the width of the grass quad is twice its height.


| ![](aspect_1.jpg) *Aspect = 1; Spread = 0* | ![](aspect_2.jpg) *Aspect = 2; Spread = 0* |
|---|---|


### Offset


Sometimes to avoid visual artifacts, it is necessary to slightly raise grass quads above the ground. This parameter specifies the offset in units up the surface normal, thus accurately repeating its relief. It is set by the *[mean](../../../objects/objects/grass/settings.md#random)* value (only positive) and additional *[spread](../../../objects/objects/grass/settings.md#random)* value (positive or negative), if variation is required.


### Rotation


Rotation of grass quads adds more diversity. This parameter specifies the rotation of grass quads in degrees in random directions . It is set by the *[mean](../../../objects/objects/grass/settings.md#random)* value (only positive) and additional *[spread](../../../objects/objects/grass/settings.md#random)* value (positive or negative), if variation is required. Values are set for each diffuse texture column separately.


### Texture Slots


On one single field, it may be necessary to simulate grass that had grown in good and bad conditions, shooting young grass blades and withered straw. The grass [diffuse texture](../../../content/materials/library/grass_base/index.md#texture_diffuse) can have 4�x�n slots, each containing a separate grass cluster, plant, or flower. The number of *horizontal rows* in the texture can be from 1 to 4. However, the number of *vertical columns* may vary depending on the way the grass distribution is specified:


- If the [image mask](#mask) is used to specify grass density distribution, the number of diffuse texture columns *can be less* than 4. > **Notice:** The number of diffuse texture columns in this case is determined by the number of channels in the [mask texture](#mask) (e.g., diffuse texture must have 1 column if an **R8** mask is used).
- If a [mesh mask](#mesh_mask) is used to specify grass distribution, the number of diffuse texture columns *must be equal* to 4.
- If both masks are used (the image mask sets grass density distribution and the mesh mask is used to [exclude](#mesh_mask) some areas, such as roads, the number of diffuse texture columns also *must be equal* to 4.


The *[Num Textures](../../../objects/objects/grass/settings.md#num_textures)* parameter sets a number of horizontal rows with grass clusters, plants, or flowers available in the diffuse texture, and this value cannot exceed 4. After specifying the number, each grass cluster is rendered as a separate quad on the field.


| ![](grass_regular_diffuse_sm.jpg) | ![](grass_variation_diffuse_sm.jpg) |
|---|---|
| *4 Texture Slots; Num Textures = 1* | *8 Texture Slots; Num Textures = 2* |


### Variation


To add more diversity to grass and avoid total uniformity of all blades on the field (especially required, if grass is represented as billboards), the variation option can be enabled. On randomly chosen quads, it flips the texture horizontally, automatically giving two variants of rendering the same quad.


![](grass_variation.jpg)

*Two possible variations for grass (automatic horizontal flipping)*


## Grass Quads Orientation


To make grass quads repeat the relief, the following parameters are set up:


- *[Orientation](../../../objects/objects/grass/settings.md#orientation)*. A grass quad can be oriented either along its own normal vector, or along the normal vector of its parent node (usually a terrain). However, on steep hills, grass oriented along the terrain normal can look unnatural (as the grass growth direction is up), so you will need to choose an appropriate value for the *[Angle](../../../objects/objects/grass/settings.md#angle)* parameter. In the right picture below, the *Angle* parameter is set incorrectly and the grass grows almost perpendicular to the slope: | ![](orientation_0.jpg) *Grass polygons oriented along normal of Grass Object* | ![](orientation_1.jpg) *Grass polygons oriented along normal of Terrain Object* | |---|---|
- *[Angle](../../../objects/objects/grass/settings.md#angle)*. This parameter affects to grass distribution that varies depending on the ground slope angle. This parameter simulates the natural tendency of the grass to strike root in more flat places.
- *[Intersection](../../../objects/objects/grass/settings.md#intersection)*. By reproducing the hilly landscape, it is essential that the grass follows the relief it grows on. For the grass to be rendered upon the ground, the following is necessary:

  1. Make the grass a **child** of the terrain or any arbitrary mesh (static or dynamic one). If there are some nodes in the hierarchy between a terrain or mesh node and grass, intersections will still be checked.
  2. Enable the *Intersection* option.


## Size of the Grass Field


The grass can shoot as a few separate blades, or form a field of verdure stretching to the horizon. The size of the field determines the extent of rectangular area, which is covered with grass.


- *[Size X](../../../objects/objects/grass/settings.md#size_x)* specifies the length of the grass area along the X axis.
- *[Size Y](../../../objects/objects/grass/settings.md#size_y)* specifies the length of the grass area along the Y axis.


## Step for Cell Division


Visually attractive grass, however, may reduce performance if rendered as a whole. To allow rendering at interactive frame rates, the field is split into *cells* that form a ***grid***. Each cell is estimated, whether it contributes to the grass field or stays grassless. Grassless cells are disregarded, while for the cells with grass all required computations are done. Depending on the [density](#density), blades are planted in the cell with random coordinates imitating the natural vegetation sprouting. The cells are rendered one by one, starting from the camera and further forward.


To get the resulting number of cells, *[Size](#size)* of the field (both along *[X](../../../objects/objects/grass/settings.md#size_x)* and *[Y](../../../objects/objects/grass/settings.md#size_y)* axes) is *split* using the *[Step](../../../objects/objects/grass/settings.md#step)* value.


> **Notice:** - *Size* of the field should be divided by *Step* exactly. Otherwise, if there is a remainder of a division, it may result in visual artifacts and unexpected visual effects.
> - Each cell requires 1 DIP call, so the higher the number of cells (i.e. the smaller the step), the lower the performance is. However, to create one large grass cell takes longer time. When the camera moves fast enough, small cells are created one by one very fast and smoothly, but large ones can noticeably pop into sight and cause a small rendering lag. Usually the *Step* value is set between 10 and 25 (for normal grass; if grass is used as a distant LOD of *[World Clutter](../../../objects/worlds/world_clutter/index.md)* or *[Mesh Clutter](../../../objects/objects/mesh_clutter/index.md), Step* may be different).


Controlling the step for dividing field into cells allows you to change the field size without affecting the set density for planting grass blades. On the other hand, if we change the step and consequently the number of cells without altering the density value, the number of grass quads rendered will be different.


If the *Step* value is too small and the maximum visibility distance is large, rendering of cells takes some time and the number of DIP calls increases significantly. On the other hand, a very high *Step* value causes performance spikes due to the increased number of objects per cell.


### Cell Subdivision


Each cell can also be subdivided into smaller parts by specifying the *[Subdivision](../../../objects/objects/grass/settings.md#subdivision)* value. Subdivision is usually required when the grass is used as a [low-poly distant LOD](#low_poly_grass) of a forest created by using *[World Clutter](../../../objects/worlds/world_clutter/index.md)* or *[ObjectMeshClutter](../../../api/library/objects/class.objectmeshclutter_cpp.md)* with a smaller cell size: the *Subdivision* parameter subdivides large grass cells so that they match smaller cells of a clutter. This way, positions of randomly scattered objects will coincide with positions of grass-based impostors. The range of available values is from 1 to 32.


## Masks for the Grass Field


### Image Mask for the Grass Field


To simulate a convincingly looking pasture that naturally blends with the rest of the virtual environment, the grass field can take an arbitrary outline gradually shaping and growing on the ground. Furthermore, the grass can grow chaotically and irregularly forming clumps of green and grassless patches, just like in the nature. To implement this effect, the mask is mapped on the terrain to determine the [density](#density) distribution.


The mask is an **RGBA8** texture. Each channel of this texture controls distribution of grass per *vertical column* of the [grass diffuse texture](../../../content/materials/library/grass_base/index.md#texture_diffuse) (there can be up to 4 columns in the diffuse texture).


- **Red** channel specifies the areas of growth for the 1st texture column. If there are several grass clusters in a vertical column, they are randomly spread across the masked area.
- **Green** � for the 2nd texture column.
- **Blue** - for the 3rd texture column.
- **Alpha** - for the 4th texture column.


> **Notice:** In case **R8, RG8**, or **RGB8** texture is used as a mask, the diffuse texture must have only one, two, or three columns respectively. So, if your diffuse texture contains, for example, only 1 vertical column, the **R8** texture should be used.


For every channel separately, areas where the grass should not grow have 0 channel value (no color or alpha data). Non-zero channel value creates a grassy area: the higher the value, the denser the grass grows.


The image mask is characterized with the following parameters:


- *[Threshold](../../../objects/objects/grass/settings.md#threshold)* that controls starting from what density (according to the mask), the grass should grow.
- *[Min value](../../../objects/objects/grass/settings.md#min_value)* and *[Max value](../../../objects/objects/grass/settings.md#max_value)* that set the color density range.
- *[Flip X](../../../objects/objects/grass/settings.md#flip_x)* and *[Flip Y](../../../objects/objects/grass/settings.md#flip_y)* that flip the texture horizontally and vertically (respectively).


> **Notice:** To paint the image mask directly in the scene, use *[Mask Editor](../../../editor2/mask_editor/index.md)*.


#### Minimum and Maximum Mask Values


As a solution for advanced objects seeding and memory consumption optimization, a mask can be applied to the object partially. It means that different multiple objects can share the same mask, but use different levels.


By default, each channel of the image mask specifies the areas and the density of growth in the [0;255] color density range. However, by using *Min value* and *Max value*, you can modify a certain color density range, and the part of the mask that contains the specified density range will be used to seed the grass.


For example, there is the following **R8** image mask:


![](image_mask.png)


Several grass objects that represent grass of different heights can share this mask as follows:


- In range from 100 to 200, density of the short grass can be stored. The part of the image mask, in which the specified range of color gradation is stored, will be applied for the short grass object.
- In range from 160 to 230, density of the grass of the medium height can be stored.
- In range from 190 to 255 density of the tall grass can be stored.


### Terrain Mask


The same way as by an arbitrary image mask, the grass density distribution can be defined by [ObjectLandscapeTerrain masks](../../../objects/objects/terrain/landscape_terrain/index.md#layers_masks). If a *Landscape Terrain* object is present in the world and has some masks provided, the names of the masks are available in the **Mask Terrain** parameter, so you can specify a certain landscape mask for each [grass texture slot](#slots) (grass type).


![](terrain_mask_param.png)

*Mask Terrain parameter*


![](terrain_mask.jpg)

*Grass distribution based on a landscape mask.Landscape Maskshelper is enabled*


### Mesh Mask


Vector masking allows creating roads, rivers, etc., with extremely high precision as it is independent of the mask texture resolution. A mesh-based mask can be set for grass to specify areas where grass should or should not grow.


> **Notice:** A mesh for masking should be a simple planar mesh.


![](mesh_mask.jpg)

*Mesh used as a mask*


![](mesh_masked.jpg)

*Mesh-based masking*


> **Notice:** When using a mesh mask to specify the grass distribution, the number of [diffuse texture](../../../content/materials/library/grass_base/index.md#texture_diffuse) columns *must be equal* to 4. Otherwise, the diffuse texture will be applied incorrectly.


A mesh mask can be inverted by toggling the *[Inverse](../../../objects/objects/grass/settings.md#inverse)* flag.


![](mesh_mask_inverse.jpg)

*Inverse masking*


### Field Mask


Any area of a grass field can be animated by using *[Field Animation](../../../objects/effects/fields/field_animation/index.md)*. *[Field Spacer](../../../objects/effects/fields/field_spacer/index.md)* is used to specify areas of grass that should not be rendered. Such areas of grass are specified by the *[Field Mask](../../../objects/objects/grass/settings.md#field_mask)* (*[Parameters](../../../editor2/node_parameters/index.md)* window -> *Grass* section).


> **Notice:** The *Field Mask* set for the grass object must match the *[Field Mask](../../../principles/bit_masking/index.md#field_mask)* of a *[Field](../../../objects/effects/fields/index.md)* node applied to the grass.


![](field_mask.png)


See the example on animating grass with the animation field [here](../../../objects/effects/fields/field_animation/index.md#example).


## Density of Growth and Grass Randomization


To achieve sufficient grass field density, adjust the *[Density](../../../objects/objects/grass/settings.md#density)* parameter. It defines how many grass quads are rendered per square unit.


- The *higher* the value, the more grass quads are rendered and the closer they are positioned. Note that the final result also depends on the *[Step](../../../objects/objects/grass/settings.md#step)* parameter, which defines how the field is divided into cells.


> **Warning:** Increasing *[Density](../../../objects/objects/grass/settings.md#density)* significantly raises RAM and VRAM usage. Therefore, when using values above **1.0** for large grass areas (more than 1 sq. km) make sure that you apply optimization techniques such as limiting the [visibility distance](../../../principles/world_management/index.md#visible), using [levels of detail](../../../objects/objects/grass/index.md#low_poly_grass) and enabling the grass [Thinning](../../../objects/objects/grass/settings.md#thinning) option. Otherwise, setting higher values can quickly result in excessive memory consumption.


To randomly position grass quads across an area using the image mask, set up the *[Seed](../../../objects/objects/grass/settings.md#seed)* value, which is an integer value used to generate pseudo-random successions of numbers (in other words, a *random seed*). To get a random seed value, press the *Randomize* button.


> **Notice:** The same *Seed* value always generates the same successions of numbers.


Setting up the *Seed* value is necessary when there is more than one grass object in the world. It enables to position grass quads differently so that 2 quads don't have the same coordinates.


To achieve the predominance of one type of the grass over the other types, you can use the *[Probability](../../../objects/objects/grass/settings.md#probability)* parameter. This parameter sets the grass rendering probability per diffuse texture column: you can specify a probability factor for each column of the diffuse texture separately.


For example, if you set the probability factor to 5 for the 1st column of the [diffuse texture](#diffuse_texture), the grass blades quads stored in slots of this column will appear more often.


| ![](probability_1.jpg) *Probability = 1* | ![](probability_5.jpg) *Probability for the 1st column = 5* |
|---|---|


## Grass Optimization


As it was mentioned [above](#step), rendering all grass cells at once (and therefore thousands of grass polygons) drastically drops performance.


The grass field can be thinned out with a distance: you can check the *[Thinning](../../../objects/objects/grass/settings.md#thinning)* box in order not to render random grass polygons across the grass *[Fade](../../../principles/world_management/index.md#fading)* distance.


> **Notice:** When changing the settings described above, you can compare the previous and the current number of grass triangles: simply check the *[Triangles](../../../objects/objects/grass/settings.md#triangles)* counter.


Choosing the optimal *[Step](#step)* for cells division is also important when optimizing grass. For normal grass (that is used properly), the optimal step is in range [10, 25].


### Using Grass as Low-Poly LOD


When using a grass object as a low-poly LOD (for example, to create a distant LOD for a forest), the clutter and the grass cells must match. So, you need to make sure that the following parameters match:


- *[Seed](../../../objects/objects/grass/settings.md#seed)* of both objects so that they are positioned the same way.
- *[Size X](../../../objects/objects/grass/settings.md#size_x)* and *[Size Y](../../../objects/objects/grass/settings.md#size_y)* of both objects.
- *Clutter Step* matches the ratio of *Step/[Subdivision](../../../objects/objects/grass/settings.md#subdivision)* values of the grass.
- *[Orientation](../../../objects/objects/grass/settings.md#orientation)* flag is enabled/disabled for both objects.
- *[Intersection](../../../objects/objects/grass/settings.md#intersection)* flag is enabled/disabled for both objects.
- *[Flip X](../../../objects/objects/grass/settings.md#flip_x)* and *[Flip Y](../../../objects/objects/grass/settings.md#flip_y)* are enabled/disabled for both objects (in case the image mask is used).
- *[Inverse](../../../objects/objects/grass/settings.md#inverse)* is enabled/disabled for both objects (in case the mesh mask is used).
- *[Min Value](../../../objects/objects/grass/settings.md#min_value)* and *[Max Value](../../../objects/objects/grass/settings.md#max_value)* of both objects (in case the image mask is used).
- *[Angle](../../../objects/objects/grass/settings.md#angle), [Threshold](../../../objects/objects/grass/settings.md#threshold), [Density](../../../objects/objects/grass/settings.md#density)*, and *[Probability](../../../objects/objects/grass/settings.md#probability)* of both objects.
