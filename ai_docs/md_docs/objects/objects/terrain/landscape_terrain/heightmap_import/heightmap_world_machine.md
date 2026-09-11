# Importing Height Map from World Machine


[![](world_machine_scheme.png)](world_machine_scheme.png)


## Export Settings


### Dimensions


When exporting a heightmap from **World Machine**, pay attention to the following parameters (available via *World Commands -> Project World Parameters�*):


![](wm_base_properties.png)


- *Width* and *Height* define the physical size in kilometers.
- *Resolution* sets the size of the output heightmap in pixels.
- *Detail scale* provides the info on the resolution of the output heightmap, i.e. how many meters there are in one pixel.


*Elevation* is available in the General Setup tab of the Project Settings window.


![](wm_elevation.png)


### Tiling


For large-scale terrains (more than 8K), export in **tiles** is recommended, this helps to avoid RAM limitations, especially when using 32 bit textures. The minimum recommended tile size is 1024 to avoid visual tiling artifacts. To do that, in the Project Settings on the *Tiled Build Options* tab (available for the Professional Edition), set the *Tile Resolution* and the number of *Tiles per Side*, check the *Final Resolution*:


![](wm_tile_settings.png)


And export the height map by selecting *Tiled Build*:


![](wm_tile_export.png)


### Export Format


In the *Heightfield File Output* settings, select the suitable [export format](../../../../../editor2/assets_workflow/asset_types.md#texture). UNIGINE allows importing 8, 16, and 32-bit heightmaps.


> **Notice:** The **RAW** format is not supported.


## Importing


The exported heightmap is imported to UNIGINE as follows. In the **Landscape Layer Map**:


![](wm_import.png)


- In the *Import Maps* section, select the heightmap file you want to import.

  - For the **normalized** heightmap, indicate the minimum and maximum heights taken from the *Base Elevation* and *Maximum Elevation* values.
  - The **unnormalized** map does not require setting the height values.
- In the *Landscape Asset* section, set the actual size of your terrain in meters, the same as in *Width* and *Height* in *World Machine*.
- Check the *Current Data Density* value. It shows the meter-to-pixel ratio, and should correspond to the *Detail Scale* value.
- In the *Import settings* section, check the *Resolution* values. They define the resolution of the heightmap. They are set automatically in most cases, but can also be adjusted, if required.


If the heightmap is represented by a **[tileset](#tiles)**, set the corresponding [data-filling](../../../../../objects/objects/terrain/landscape_terrain/landscape_layer_map.md#data_filling) pattern.


Click **Reimport**.
