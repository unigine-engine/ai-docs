# Mask Parameters


**Mask** is landcover data based on which natural features of the terrain are generated: details, grass, trees, etc.


Masks are added the same way as [Elevation and Imagery](../../../../editor2/sandworm/workflow/landscape/index.md), both [online and offline data sources](../../../../editor2/sandworm/sources/index.md#data_sources) can be used. The data contained in a mask source can be [filtered](#filters) to fine-tune the use of the mask for a specific purpose.


An example of creating a *Mask* is given [here](../../../../editor2/sandworm/workflow/mask/index.md).


## Filters


Filters select specific data from the data source for each type of the generated landcover object. There are three types of filters:


![](add_filter.png)


| Indexed | ![](indexed_filter.png) Select a particular color index from the list of available ones in the source raster image. You can also specify the color range by indices (from color to color). |
|---|---|
| Single Channel | ![](single_channel_filter.png) Select a channel of the source raster image. |
| Color | ![](color_filter.png) Set a particular color taken from the source raster image and adjust the **Range** for it, thus defining the suitable deviation from the specified color within the range [0, 255]. Click on the color to open the color settings: ![](open_color_selection.png) Select the color from available, use HSV or RGBA values, or click *Pick Screen Color* to select the color from the image in the *Preview* panel: ![](select_color.png) **Range** — threshold value for the color that defines a range of colors to be used for the filter. 0 means that only the selected color is used as mask, increasing the *Range* value makes the filter include the specified number of neighboring colors. |
| Copy filters ![Copy Filters Button](../share_button.png) | Opens the window to copy all filters from the current source to the selected sources: ![Copy Filters Window](../copy_filters.png) If you change anything in filters that you have already copied, and want these changes to be applied to other sources, you need to copy the filters once again. All filters of the selected sources will be replaced with the filters of the current source. |
| Delete all filters ![Delete Filters Button](../../interface/trash_bin.png) | Deletes all added filters. |
| Add ![Add Filter Button](../add_button.png) | Adds one more filter. |
