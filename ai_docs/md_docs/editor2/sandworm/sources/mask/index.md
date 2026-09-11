# Mask Parameters


**Mask** is landcover data based on which natural features of the terrain are generated: details, grass, trees, etc.


Masks are added the same way as [Elevation and Imagery](../../../../editor2/sandworm/sources/elevation_imagery/index.md) � see the [walkthrough](../../../../editor2/sandworm/workflow/landscape/index.md#add_georef) for a step-by-step example. Both [online and offline data sources](../../../../editor2/sandworm/sources/index.md#data_sources) can be used. See the [list of supported formats](../../../../editor2/sandworm/index.md#data_formats). The data contained in a mask source can be [filtered](#filters) to fine-tune the use of the mask for a specific purpose.


An example of creating a *Mask* is given [here](../../../../editor2/sandworm/workflow/mask/index.md).


## Filters


Filters select specific data from the data source for each type of the generated landcover object. There are three types of filters:


![](add_filter.png)


| Indexed | ![](indexed_filter.png) Select a particular color index from the list of available ones in the source raster image. You can also specify the color range by indices (from color to color). |
|---|---|
| Single Channel | ![](single_channel_filter.png) Select a channel of the source raster image. |
| Color | ![](color_filter.png) Set a particular color taken from the source raster image and adjust the **Range** for it, thus defining the suitable deviation from the specified color within the range [0, 255]. Click on the color to open the color settings: ![](open_color_selection.png) Select the color from available, use HSV or RGBA values, or click *Pick Screen Color* to select the color from the image in the *Map* panel: ![](select_color.png) **Range** � threshold value for the color that defines a range of colors to be used for the filter. 0 means that only the selected color is used as mask, increasing the *Range* value makes the filter include the specified number of neighboring colors. |


The settings that are common to all filters are described in [Sources and Their Parameters](../../../../editor2/sandworm/sources/index.md#filters).
