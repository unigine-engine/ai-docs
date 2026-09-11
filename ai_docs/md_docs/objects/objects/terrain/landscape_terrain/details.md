# Configuring Landscape Terrain Details


Details are intended for refinement of *Landscape Terrain* graphic data by means of tiled textures in order to achieve extreme density and realistic visual representation in close up views.


![](details_off.png) ![](details_on.png)


> **Notice:** If your project requires detection of collisions with the terrain surface, you should keep in mind that Details don't participate in [Intersection and Collision Detection](../../../../objects/objects/terrain/landscape_terrain/index.md#intersections), so it's not recommended to apply intense displacement using details since visual inconsistency may appear.


### See Also


- The *[TerrainDetail](../../../../api/library/objects/landscape_terrain/class.terraindetail_cpp.md)* class to manage *Landscape Terrain* details via API
- The *[TerrainDetailMask](../../../../api/library/objects/landscape_terrain/class.terraindetailmask_cpp.md)* class to manage detail masks of the *Landscape Terrain* Object via API
- The *[landscape_terrain_detail_base](../../../../content/materials/library/landscape_terrain_detail_base/index.md)* material for details


## Details


*ObjectLandscapeTerrain* stores visual settings for **20** detail masks intended for reaching better level of visual quality in close up views. Details represent arbitrary albedo, roughness and height (displacement) data, so you can drastically improve the look of the *Landscape Terrain*. Details are applied according to [masks](../../../../objects/objects/terrain/landscape_terrain/index.md#layers_masks) of *Landscape Layer Map* objects.


Detail settings available in *ObjectLandscapeTerrain* parameters allow defining the detail visual appearance, adding up to **1024** details to a mask and defining the material of each detail.


![](detail_parameters.png)

*Detail parameters are available on the Node tab of theObjectLandscapeTerrainparameters.*


By combining multiple details under a single mask you can diversify the look of the surface a lot.


![](several_details.gif)

*The result of combining three details under a single mask.*


The list of detail masks displays the hierarchy of details for each of 20 detail masks. Using the buttons at the top you can control details and rearrange masks or details depending on what is selected:


- ![](detail_button_create.png) � **create** details for the selected masks.
- ![](detail_button_clone.png) � **clone** the selected details.
- ![](detail_button_moveup.png) � **move up** the selected masks/details.
- ![](detail_button_movedown.png) � **move down** the selected masks/details.
- ![](detail_button_delete.png) � **delete** the selected details.


Drag details using the mouse to set up the hierarchy, Double-click on a detail or a detail mask to rename it.


Detail parameters allow applying additional masking:


| Mask Threshold | Threshold starting from which the mask starts to be rendered. |
|---|---|
| Mask Contrast | Contrast of the mask. For each mask you can set a Dither amount enabling you to reduce graphical artefacts in case of increased *Mask Contrast* value set per-detail. This Dither amount is multiplied by the [global dithering amount](../../../../editor2/settings/render_settings/landscape/index.md#detail_mask_dither). |
| Mask by Albedo | Select an albedo color of *Landscape Layer Masks* in the world to be used as a mask. In this case, all areas on the terrain having selected color will be covered by the detail. > **Notice:** Control opacity by using the Alpha channel of the **Mask by Albedo** color. |
| Mask by Height | This group of parameters is used for mask modulation. For the areas specified by the mask, you can set up the range of heights in which the detail is visible. - **Min Visibility** � minimum height value starting from which the detail mask begins to fade in until it becomes completely visible. The default value is -inf. - **Max Visibility** � maximum height value starting from which the detail mask begins to fade out until it becomes completely invisible. The default value is inf. - **Min Fade** � over this height range below the minimum height value the detail mask will fade in until it is completely visible. The default value is 0. - **Max Fade** � over this height range above the maximum height value the detail mask will fade out until it is completely invisible. The default value is 0. |
| Mask by Texel Size | This group of parameters just like the previous one is used for mask modulation. For the areas specified by the mask, you can set up the range of texel sizes in which the detail is visible. - **Min Visibility** � minimum texel size value starting from which the detail mask begins to fade in until it becomes completely visible. The default value is -inf. - **Max Visibility** � maximum texel size value starting from which the detail mask begins to fade out until it becomes completely invisible. The default value is inf. - **Min Fade** � over this range below the minimum texel size value the detail mask will fade in until it is completely visible. The default value is 0. - **Max Fade** � over this range above the maximum texel size value the detail mask will fade out until it is completely invisible. The default value is 0. |


The **Detail Material** section contains settings of the *[landscape_terrain_detail_base](../../../../content/materials/library/landscape_terrain_detail_base/index.md)* material defining visual features of the current detail.


Internally each *[Landscape Layer Map](../../../../api/library/objects/landscape_terrain/class.landscapelayermap_cpp.md)* stores its **20** masks in 5 RGBA8 mask textures. The following parameters display the info on the corresponding mask texture and can be used to [access the mask via API](../../../../api/library/objects/landscape_terrain/class.landscapeimages_cpp.md#getMask_int_ImagePtr):


![](detail_parameters_mask_info.png)


| Mask Texture | The index of the mask texture used. |
|---|---|
| Channel | The channel of the mask texture used. |
