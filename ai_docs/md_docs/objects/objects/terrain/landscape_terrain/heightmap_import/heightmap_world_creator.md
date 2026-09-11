# Importing Height Map from World Creator 2


[![](world_creator_scheme.png)](world_creator_scheme.png)


## Export Settings


### Dimensions


When exporting a heightmap from **World Creator 2**, pay attention to the following parameters in the **Base Properties** panel:


![](wc_base_properties.png)


- *Terrain Width* and *Terrain Length* (in meters) define the physical size of the terrain.
- *Precision* defines the resolution of the output heightmap, i.e. how many meters there are in one pixel.
- *Resolution (in Pixel)* of the heightmap which is generated from the terrain.


Check also the *Min* and *Max* height values of your heightmap in the top left corner. They are required, if you import your heightmap as normalized.


![](wc_min_max_height.png)


### Tiling


For large-scale terrains (more than 8K), export in **tiles** is recommended. This helps to avoid RAM limitations, especially when using 32 bit textures. The minimum recommended tile size is 1024 to avoid visual tiling artifacts. To do that, in the export settings for the heightmap, enable *Split*, define the Tile size (the power of 2), and disable *Include Border*:


![](wc_tile_export.png)


### Export Format


When exporting the terrain, select the suitable [export format](../../../../../editor2/assets_workflow/asset_types.md#texture). UNIGINE allows importing 8, 16, and 32-bit heightmaps.


> **Notice:** The **RAW** format is not supported.


## Importing


The exported heightmap is imported to UNIGINE as follows. In the **Landscape Layer Map**:


![](wc_import.png)


- In the *Import Maps* section, select the heightmap file you want to import.

  - For the **normalized** heightmap, indicate the minimum and maximum heights taken from the *Min* and *Max* values.
  - The **unnormalized** map does not require setting the height values.
- In the *Landscape Asset* section, set the actual size of your terrain in meters, the same as *Terrain Width* and *Length* in *World Creator 2*.
- Check the *Current Data Density* value. It shows the meter-to-pixel ratio, the same as *Precision* in *World Creator 2*.
- In the *Import settings* section, check the *Resolution* values. They define the resolution of the heightmap in pixels. They are set automatically in most cases, but can also be adjusted, if required.


If the heightmap is represented by a **[tileset](#tiles)**, set the corresponding [data-filling](../../../../../objects/objects/terrain/landscape_terrain/landscape_layer_map.md#data_filling) pattern.


Click **Reimport**.
