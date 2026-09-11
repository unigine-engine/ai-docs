# Adding Grass


The article provides the tips and tricks how to create animated [grass](../../../../objects/objects/grass/index.md), swaying and moving as if with the wind. Your grass will also realistically vary in color across the field, so that it does not look unnatural like a freshly-painted lawn. Moreover, you will keep the frame rate high when rendering all these polygons. No matter how big your grass field should be (it can cover the whole terrain), grass appears only around the camera. And here is a first tip: grass looks better upon a hilly terrain. As for planes, low and non-dense grass would be a reasonable choice.


## Required Textures


The textures that are required to set up grass (within this tutorial) are the following:


> **Notice:** The textures used in this tutorial are taken from the *[Art Samples](../../../../content/samples/index.md)* demo. The demos can be added via *[UNIGINE SDK Browser](../../../../sdk/index.md#samples)*. However, you can use your own textures if any.


- [Diffuse textures](../../../../content/materials/library/grass_base/index.md#texture_diffuse). Within this tutorial, we will use 2 diffuse textures: one for *regular* grass and one for grass of *[various](../../../../objects/objects/grass/index.md#slots)* types. The first texture has 1 x 4 slots and the second texture � 4 x 4 slots. As we are going to use the [image mask](../../../../objects/objects/grass/index.md#mask) for specifying the grass density distribution, the diffuse texture can contain less than 4 columns. | [![](grass_regular_diffuse_sm.png)](grass_regular_diffuse.png) | [![](grass_variation_diffuse_sm.png)](grass_variation_diffuse.png) | |---|---| | *Diffuse Texture for Regular Grass* | *Diffuse Texture for Grass of Various Types* |
- [Spatial noise texture](../../../../content/materials/library/grass_base/index.md#textures_additional) (RGB). It will cover the whole terrain and allows you to color grass differently in all locations. > **Notice:** The texture does not have the same size as the terrain, but should meet the following requirements: > > > - Dimensions of the texture should be equal to some power of two (for example, 1024 � 1024, 2048 � 2048 and so on). > - Dimensions of the texture should be proportional to the terrain size. For example, if you have the 4096 � 4096 terrain, the texture should not be 256 � 512. > - Dimensions of the texture should be chosen so that to get the result of appropriate quality after mapping pixels to the terrain. For example, if you have the 4096 � 4096 terrain and the 1024 � 1024 texture, 1 pixel of this texture will be mapped to cover 4 units of the terrain. If such quality is enough, you can use this texture. Otherwise, you should create a new one of an appropriate size. Within this tutorial, for the 4097 � 4097 terrain, 2048 � 2048 texture will be used (1 pixel will be mapped to cover 2 units). ![](grass_spatial_noise.jpg)
- [Image mask](../../../../objects/objects/grass/index.md#mask) that determines spreading of grass across the terrain. Each channel of the mask (R, G, B and A) controls if the grass from the 1st, 2nd, 3rd and 4th columns (respectively) is rendered or not. The grass will grow only across areas with a channel color value. Within this tutorial, we will use 2 image masks taken from the *Art Samples* demo: | ![](regular_grass_mask.png) | ![](variation_grass_mask.png) | |---|---| | *Image Mask for Regular Grass* | *Image Mask for Grass of Various Types* |

  - R8 texture for the regular grass, as its diffuse texture contains only 1 vertical column. The regular grass will be rendered where the red color is.
  - RGBA8 texture for the grass of various types, as its diffuse texture contains 4 columns. The grass of various types will be rendered where the white color is.
- [Translucent texture](../../../../content/materials/library/grass_base/index.md#textures_translucent) that stores information on grass material translucency. It is represented by the R8 texture atlas, and the number of rows and columns is determined by the number of grass chunks in the diffuse texture. Within this tutorial, we will use the translucent texture for the regular grass, so it will contain 4 vertical slots. This texture can be used instead of tweaking the *Translucent* parameter of the material: the texture specifies areas of the grass blades that permit light to pass through, and the parameter allows scaling of such translucence effect. ![](translucent_map.png)


## Step 1. Prepare World


Before adding and setting up grass, you should prepare the world. If you have a set up world with the terrain, the sun and the atmosphere, you can use it. If you don't have one, you can slightly modify the `vegetation/forest.world` in the *Art Samples* demo (can be added via *[UNIGINE SDK Browser](../../../../sdk/index.md)*): delete all child nodes of the *Landscape* node in the *[World Hierarchy](../../../../editor2/organizing_nodes/index.md)*.


Within this tutorial the modified `forest.world` will be used.


## Step 2. Add Grass


Within this tutorial, we are going to add 2 types of grass: the *regular* grass and the grass of *various* types.


1. In the Menu bar, choose *Create -> Grass -> Base* and drop the grass somewhere in the world. ![](../add_grass.png) ![](1_sized_sm.jpg) *Grass object added to world*
2. In the *[World Hierarchy](../../../../editor2/organizing_nodes/index.md)* window, [clone](../../../../editor2/organizing_nodes/index.md#clone_node) the added *Grass* object. Rename the objects as follows: ![](1_added_grass.png)
3. Select the added *Grass* objects in the *[World Hierarchy](../../../../editor2/organizing_nodes/index.md)* window. In the *Node* tab of the *[Parameters](../../../../editor2/node_parameters/index.md)* window, go to the *Surfaces* section and define the area of visibility for the future grass field. All grass blades cannot be rendered at once, especially, if the field is huge. Instead, they are going to be rendered in a small area around the camera. As a result, you will see that the grass polygons appear and fade out within the set distance (94 units). ![](1_max_fade.png)

  - Set the *[Maximum Visible](../../../../principles/world_management/index.md#max_visible)* distance to 4 units. Within this distance from the camera all grass blades are visible.
  - Set the *[Maximum Fade](../../../../principles/world_management/index.md#max_fade)* distance to 90 units. Over this distance the grass will gradually fade out according to the alpha channel value of its diffuse texture.
4. In the *Grass* section of the *Node* tab, set the real size of the grass field: select both grass objects and set *[Size X](../../../../objects/objects/grass/index.md#size)* (along the X axis) and *[Size Y](../../../../objects/objects/grass/index.md#size)* (along the Y axis) to repeat the size of the 4097 � 4097 terrain. ![](1_size.png)
5. Add the grass objects as ***child*** nodes to the terrain, so the grass can grow upon the terrain repeating its relief: select the grass nodes and [drag](../../../../editor2/organizing_nodes/index.md#rearrange_node) them to the terrain node with the left mouse button pressed. ![](1_child.png)
6. Enable the *[Intersection](../../../../objects/objects/grass/settings.md#intersection)* option to allow intersection with a parent node. ![](1_intersection.png) Now the grass grows upon the terrain (repeats its relief), but the field is still not positioned properly: ![](1_intersected.jpg)
7. In the *Node* tab of the *Parameters* window, reset the position of the grass objects to 0 relative to its parent in the *Common* section. ![](1_coordinates.png) Position of the grass object becomes synchronized with the terrain: ![](1_intersected.jpg) ![](1_coordinated_sm.jpg)
8. Currently, coordinates of the grass quads of both objects are coincide. To avoid grass quads flickering, position grass quads of the *grass_regular* object differently: click **Randomize** (*Node* tab -> *Grass* section) to generate a random seed. ![](1_random_seed.png)


## Step 3. Set Up Grass Material


Now you should create materials for the grass objects before tweaking their spread any further.


1. In the *World Hierarchy* window, select the *regular_grass* and *variation_grass* nodes and go to the *Node* tab of the *Parameters* window.
2. Go to the *Material* section of the *Node* tab: currently, the base *[grass_base](../../../../content/materials/library/grass_base/index.md)* material is assigned to the grass nodes. Click *Inherit* or ![](2_inherit_material.png) to create a new child material. The new material will be automatically assigned to both grass nodes. ![](2_new_material.png)
3. Rename the new material *grass_regular* in the *Name* field. ![](2_renamed_material.png)
4. In the World Hierarchy window, select the *variation_grass* node and go to the *Node* tab of the *Parameters* window. In the *Material* section, click ![](2_inherit_material.png) to inherit a new material. > **Notice:** In this case, a new material will inherit all settings of the *grass_regular* material (e.g. slope, stem noise and so on). Anyway, you still can inherit a material for the 2nd grass object from the base *grass_base* material and set specific settings for it. The material will be assigned automatically to the selected *variation_grass* node. Rename the new material *grass_variation* in the *Name* field. ![](2_renamed_material_0.png)
5. Adjust the materials of the grass objects: for each material, go to the *Textures* tab and drag the [diffuse texture](#diffuse_textures) to the corresponding field. > **Notice:** You may want to manually edit the alpha channel of the mipmaps, because on automatically generated mipmaps thin blades may disappear incorrectly or unpleasantly. | ![](2_regular_diffuse.png) | ![](2_variation_diffuse.png) | |---|---| | *Diffuse Texture forregular_grass* | *Diffuse Texture forvariation_grass* |
6. Go to the *Grass* section of the *Node* tab. For both *Grass* objects, set the proper number of horizontal rows in the diffuse textures in the *[Num Textures](../../../../objects/objects/grass/index.md#slots)* field. For example, we have 4 rows for both grass objects, so the *Num Textures* must be set to 4. > **Notice:** As you can see, the *regular_grass* node isn't rendered properly because there is no *[image mask](../../../../objects/objects/grass/index.md#mask)*. The diffuse texture of the regular grass contains only 1 column, so the 1-channelled image mask (R8) should be set.
7. Drag the correct *[R8 image mask](#image_mask)* from the Asset Browser to the corresponding field in the *Grass* section of the *Node* tab to fix rendering of the *regular_grass* node. We will set up all related parameters later. ![](2_grass_regular_incorrect.png) ![](2_num_textures_regular_fixed.png)
8. Go to the *States* tab of the *Material* section (*Node* tab, *Parameters* window). Check the *[Noise](../../../../content/materials/library/grass_base/index.md#option_color_noise)* option for the *grass_regular* material. It will allow you to color the blades of the regular grass differently across the whole field. The *Noise* option will also be set for the *grass_variation* material. ![](2_noise_option.png)
9. For the *grass_variation* material, go to the *States* tab of the *Material* section and uncheck the *[Noise](../../../../content/materials/library/grass_base/index.md#option_color_noise)* option. It will allow the grass of various types to differ from the regular grass.
10. For the *grass_regular* material, go to the *Textures* tab and drag the [spatial noise texture](#noise_texture) from the Asset Browser to the *[Noise](../../../../content/materials/library/grass_base/index.md#texture_noise)* field. ![](2_load_noise.png)
11. Go to the *Parameters* tab of the *grass_regular* material. To the right of the Noise *[Transform](../../../../content/materials/library/grass_base/index.md#transform)* field, click ![](2_edit_transform.png) to edit the values (or modify the expression right in this field). ![](2_noise_transform.png)
12. Set the scale of texture coordinates by *X* and *Y* axes to 1: in this case, the spatial noise texture will cover the entire terrain. ![](2_noise_transform_by.png) You can see patches of light green and yellow grass: ![](2_noise_transformed.jpg)
13. The colors are too vivid to match the terrain colors. Drop the *[Scale](../../../../content/materials/library/grass_base/index.md#scale)* to 0.38 to dim the noise color. ![](2_noise_scale.png) ![](2_noise_scaled.jpg)
14. The blades are quite thin, so make them a little bit more transparent to light when it shines from behind: increase the *[Translucent](../../../../content/materials/library/grass_base/index.md#parameter_shading_back)* parameter up to 0.7 for the *grass_regular* material. For the *grass_variation* material it will be applied automatically. ![](2_translucency.png) The grass will become more transparent and lighter: ![](2_translucent_0.png) ![](2_translucent_1.png)
15. Go to the *States* tab and enable the *Translucent* option for the regular grass. This will activate the *Translucent Map* in the *Textures* tab that allows specifying translucent areas of the grass blades. ![](2_translucent_state.png)
16. In the *Textures* tab, drag the [translucent texture](#translucence_texture) from the Asset Browser to the *Translucent Map* field. ![](2_translucent_map.png) According to the texture, the translucence effect applied to the grass blades will be gradient.
17. Disable the *Translucent* option for the *grass_variation* material.
18. Increase the *[Alpha Intensity](../../../../content/materials/library/grass_base/index.md#parameter_alpha_intensity)* to 1.5 to scale the Alpha channel of the diffuse texture of the regular grass. In the result, the grass field will look denser. ![](2_diffuse_scale.png) ![](2_diffuse_shading_default.jpg) ![](2_diffuse_shading_custom.jpg)
19. For now, transparency and diffuse coloring values are the same for the *grass_regular* and *grass_variation* materials. Change these settings for the *grass_variation*: set the *[Translucent](../../../../content/materials/library/grass_base/index.md#parameter_shading_back)* parameter to 0.5 and the *[Alpha Intensity](../../../../content/materials/library/grass_base/index.md#parameter_alpha_intensity)* to 0.8. ![](2_various_shading_default.jpg) ![](2_various_shading_custom.jpg)


## Step 4. Set Up Grass Density and Spread


1. First, set up the density of the grass. For the regular grass, go to the *Grass* section of the *Node* tab and drop the *[Step](../../../../objects/objects/grass/index.md#step)* to 17. It will make the cells which are used to render the grass field smaller, however, this value is not so large to hit the performance when the cell is created. The *[Subdivision](../../../../objects/objects/grass/index.md#subdivision)* should be set to 1 to avoid additional subdivision of the grass cells: higher values of this parameter are usually used when the grass is used as a low-poly distant LOD of a forest created by using *[World Clutter](../../../../objects/worlds/world_clutter/index.md)* or *[Mesh Clutter](../../../../objects/objects/mesh_clutter/index.md)*. ![](3_step.png) The grass is regenerated. The density also changed, because it is defined for one cell. As we made the cell smaller, the grass turned out to be slightly more dense. ![](3_step_default.jpg) ![](3_step_custom.jpg)
2. Increase the *[Density](../../../../objects/objects/grass/index.md#density)* of the regular grass in a cell to 2.5 to add more grass blades on the field. For the various grass, set this value to 0.5. ![](3_density.png) ![](3_step_custom.jpg) ![](3_dense_sm.jpg)
3. Now tweak the spread of the grass. For the regular grass, we have already [set the image mask](#regular_grass_mask). Now you should set it for the grass of various types: drag the RGBA8 *[image mask](#image_mask)* to the *[Mask Image](../../../../objects/objects/grass/settings.md#mask)* field in the *Grass* section of the *Node* tab. ![](3_load_mask.png) The grass no longer grows on mountains peaks and stony areas: ![](3_mask_default.jpg) ![](3_mask_set.jpg) > **Notice:** To paint the image mask directly in the scene, use *[Mask Editor](../../../../editor2/mask_editor/index.md)*.
4. Set the *[Threshold](../../../../objects/objects/grass/settings.md#threshold)* to 0.3 to increase the mask intensity. > **Notice:** Perform this step for both grass objects. ![](3_threshold.png) This will decrease the area that the grass covers: ![](3_mask_set.jpg) ![](3_threshold_lower_sm.jpg)
5. Usually the grass does not grow on the steep hillsides. Increase the *[Angle](../../../../objects/objects/grass/settings.md#angle)* to 0.85 to make steep areas grassless. > **Notice:** Perform this step for both grass objects. ![](3_angle.png) Now the spread of the grass is more realistic: ![](3_angle_default.jpg) ![](3_angle_custom.jpg)
6. Currently, all types of the grass of various types (in other words, [slots](../../../../objects/objects/grass/index.md#slots) of the [diffuse texture](#textures) of the *grass_variation* node) are spread uniformly across the grass field. However, in nature, one type of grass can predominate over the others or grow in small groups. To achieve this, change the *[Probability](../../../../objects/objects/grass/index.md#probability)* parameter so that one type of the grass will predominate over the other types according to the diffuse texture. ![](3_probability.png) For example, you can set the probability factor to 4 for the 3rd column of the [diffuse texture](#textures): ![](3_probability_default.jpg) ![](3_probability_custom.jpg)


## Step 5. Set Up Grass Shape and Orientation


1. When changing from bare areas to grassy ones, our grass starts to grow as small and thinned out. But on the stones, it does not look too good. Increase the *Min Height* up to 1.2. In areas with low density (according to the mask) the grass will be higher. You can set different height values for each of four columns in the diffuse texture, or leave it the same for all. > **Notice:** Perform this step for both grass objects. For the regular grass, setting the value for the first column is enough. ![](4_min_height.png) ![](4_min_height_default.jpg) ![](4_min_height_custom.jpg)
2. Increase the *Max Height* of the grass blades to 1.7 units. In areas with high density (according to the mask) the grass becomes higher. We'll use the same height for all four columns in the diffuse texture as well. > **Notice:** Perform this step for both grass objects. For the regular grass, setting the value for the first column is enough. ![](4_max_height.png) ![](4_higher_sm.jpg)
3. Unlike trees, the grass is usually grows perpendicular to the terrain. Check the *[Orientation](../../../../objects/objects/grass/settings.md#orient)* in the *Grass* tab of the *Parameters* window to orient the grass objects along the normal of the terrain. Perform it for both regular and variation grass. ![](4_orientation.png) ![](4_orientation_off.jpg) ![](4_orientation_on.jpg)
4. From above the grass seems too flat. In the *[Material](../../../../editor2/materials_settings/index.md)* section of the *Node* tab (the *Parameters* window), go to the *Parameters* tab and increase the *[Slope](../../../../content/materials/library/grass_base/index.md#parameter_slope)* to 0.5 to make it more billboard-like. > **Notice:** The slope will be the same for both the *grass_regular* and *grass_variation* materials. ![](4_slope.png) ![](4_slope_unscaled.jpg) ![](4_slope_scaled_sm.jpg)
5. Grass blades are too thin and sometimes appear in dashed lines. Increase the *[Alpha Intencity](../../../../content/materials/library/grass_base/index.md#parameter_alpha_intensity)* up to 2 to make the blades look thicker and the grass denser. ![](4_alpha.png)


## Step 6. Set Up Grass Animation


In nature, grass isn't static. So, it is necessary to set up grass animation. It can be set via [animation settings](../../../../content/materials/library/grass_base/index.md#parameters_animation) of the grass material, so that all grass polygons are animated uniformly. Or you can animate some specific area of the grass field by using [animation fields](../../../../objects/effects/fields/field_animation/index.md).


Within this tutorial, only the first method will be used. The example on using grass with animation fields can be found [here](../../../../objects/objects/grass/index.md#field_mask).


> **Notice:** Perform this step for the *grass_regular* material. The inherited *grass_variation* material will have the same values.


1. In the *Parameters* tab of the *Material* section (the *Node* tab, *Parameters* window), set the *[Stem noise](../../../../content/materials/library/grass_base/index.md#parameter_stem_noise)* to 0 to make all the grass blades move uniformly. It will help to learn how to adjust the animation. ![](5_stem_to_zero.png) ![](5_stem_noise_0.gif)
2. Decrease the *[Stem offset](../../../../content/materials/library/grass_base/index.md#parameter_stem_offset)* to 0.1 to make the grass sway and stretch horizontally to a lesser degree. ![](5_stem_offset.png)
3. Decrease the *[Stem radius](../../../../content/materials/library/grass_base/index.md#parameter_stem_radius)* to 0.1 so that the grass does not bend down to the ground. ![](5_stem_radius.png)
4. Increase the *[Stem scale](../../../../content/materials/library/grass_base/index.md#parameter_stem_scale)* to 2 to make the grass move two times faster. ![](5_stem_scale.png)
5. Increase the *[Stem noise](../../../../content/materials/library/grass_base/index.md#parameter_stem_noise)* to 2 to make the blades movement more random. ![](5_stem_noise_higher.png)


![](5_animated.gif)


## Grass Optimization


Grass optimization means reducing the number of grass polygons rendered each frame and the number of DIP calls. To optimize the grass that we added and set up above, we have already set the *[Step](../../../../objects/objects/grass/settings.md#step)* value to 17: the *[Size](../../../../objects/objects/grass/settings.md#size_x)* of the grass field is divided by this value exactly, with no remainder by division. This allows avoiding visual artifacts and unexpected visual effects. Also such value stays within the [recommended optimal range](../../../../objects/objects/grass/index.md#optimization).


Increasing the *[Density](../../../../objects/objects/grass/settings.md#density)* setting for large areas (more than 1 square kilometer) can dramatically increase RAM and VRAM usage by generating tens of gigabytes of data in memory and on the GPU. Adjust this value with extreme caution and use other optimization techniques such as limiting the [visibility distance](../../../../principles/world_management/index.md#visible) and using [levels of detail](../../../../objects/objects/grass/index.md#low_poly_grass).


The *[Thinning](../../../../objects/objects/grass/settings.md#thinning)* option is set for the grass objects by default: it allows reducing the number of grass polygons rendered across the grass *[Fade](../../../../principles/world_management/index.md#fading)* distance.


After changing the settings mentioned above, you can compare the previous and the current number of grass triangles: simply check the *[Triangles](../../../../objects/objects/grass/settings.md#triangles)* counter.


![](6_triangles.png)
