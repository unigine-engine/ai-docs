# Adding a Mask


A Mask can be useful in two ways:


- [Detail](../../../../objects/objects/terrain/landscape_terrain/index.md#details) specifying where the additional features (such as rocks, sand, etc.) are located on the primary surface.
- Mask to identify where to generate [grass and trees](../../../../editor2/sandworm/workflow/vegetation/index.md).


You are already experienced enough to [add an asset](../../../../editor2/sandworm/workflow/landscape/index.md#add_georef) as a mask on your own. Let's add the asset `UnigineGeoreferencedTerrainGeneration/landcover/landcover_mask.tif` and click *Preview*.


You can already click *Create Mask*, and this mask will be added to *Terrain Layers*. Any further changes you make in this source will be saved automatically.


![](mask_added.jpg)


### See Also


Check this video from the series of [video tutorials on the terrain generation](../../../../videotutorials/essentials/sandworm.md) using Sandworm:


## Specifying Mask Filters


[Filters](../../../../editor2/sandworm/sources/mask/index.md#filters) are used to pick specific data from the mask source. At least one filter is required to make the mask useful.


Let's add a filter: select the filter type.


![](set_filter_type.png)


We are going to use this mask to [generate trees](../../../../editor2/sandworm/workflow/vegetation/index.md). Apparently, this area is marked green in the landcover data. We can set the filter either as *Indexed*, or as *Single Channel* and select the green value. In our case, the result will be identical.


![](../../sources/mask/indexed_filter.png)


Let's add one more source from the assets to this mask and set a color filter.


1. In the same mask (meaning that you don't create a new mask), click the *Add Source(s)* button and select *Assets*.
2. Select the `UnigineGeoreferencedTerrainGeneration/img/sw_1mpx_img_6.tif` file and click *OK*. The preview will be updated. Let's zoom in to this source in the *Map* panel. ![](mask2_added.jpg)
3. Set the filter type to *Color* and click on the white color to open the color settings.
4. Click the *Pick Screen Color* button and click on the dark-green color on the preview. ![](pick_screen_color.jpg) Click *Apply* to apply the picked color and *OK* to close the color settings window.
5. Set *Range* to some value to allow for some color variation along the color palette. ![](color_filter.png)


This is it. Now if we generate trees using this mask they will be dispersed in the areas marked green and additionally in the dark-green areas of the added imagery.


## Generated Mask


The [generated](../../../../editor2/sandworm/workflow/generate/index.md) mask is available as a detail of the *Terrain* object:


![](example1.png)

*Mask in Detail of Landscape Terrain*


![](example2.png)

*Mask in Detail of Terrain Global*


To see how the mask is applied to the terrain, toggle it in *[Helpers](../../../../editor2/using_visual_helpers/index.md#landscape_masks)*.


![](show_mask_data.jpg)


The mask is also available for [generating vegetation](../../../../editor2/sandworm/workflow/vegetation/index.md) in *Sandworm*.


![](example3.png)

*Mask in Vegetation Object*


## What Else


- Check the article on the [mask](../../../../editor2/sandworm/sources/mask/index.md) for a more detailed description of parameters.
- Read about [configuring details](../../../../objects/objects/terrain/landscape_terrain/details.md) of *Object Landscape Terrain*.
- See the [video tutorial](https://youtu.be/UT7duARx-TY?t=507) on configuring details of *Object Terrain Global*.
- Read about indexed colors, for example on [Wikipedia](https://en.wikipedia.org/wiki/Indexed_color).
