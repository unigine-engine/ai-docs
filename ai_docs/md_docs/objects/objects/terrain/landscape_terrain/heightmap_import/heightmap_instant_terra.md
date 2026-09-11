# Importing Height Map from Instant Terra


[![](instant_terra_scheme.png)](world_creator_scheme.png)


## Export Settings


### Dimensions


When exporting a heightmap from **Instant Terra**, pay attention to the following parameters available in the properties of the first node of the terrain creation graph:


![](it_base_properties.png)


- *Width* and *Height* define the texture size in pixels.
- *Quad size* � physical size in meters set for the quad, i.e. pixel, of the height map texture. Practically, this is a multiplier for the width and height that defines the physical size of the height map. The output size of the map in meters is provided below. For example, the 1024x1024 texture with the quad size of 0.5 will result in a terrain with a physical size of 511.5 x 511.5 meters.


The height values are not identified at export by default, and the texture is imported to UNIGINE as unnormalized. To control the height, create the *Elevation info* node to generate a normalized texture with the min and max height values. Connect these values to the min and max height of the *Export terrain* node. As a result, the export file format switches to 16 bit and the height range values become available.


![](it_min_max_height.png)


### Tiling


For large-scale terrains (more than 8K), export in **tiles** is recommended, this helps to avoid RAM limitations, especially when using 32 bit textures. The minimum recommended tile size is 1024 to avoid visual tiling artifacts. To do that, use the *Multi file export terrain* node:


![](it_tile_export.png)


The recommended file naming pattern is: *filename_X$x_Y$y*.


### Export Format


When exporting the terrain, select the suitable [export format](../../../../../editor2/assets_workflow/asset_types.md#texture). UNIGINE allows importing 8, 16, and 32-bit heightmaps.


> **Notice:** The **RAW** format is not supported.


## Importing


The exported heightmap is imported to UNIGINE as follows. In the **Landscape Layer Map**:


![](it_import.png)


- In the *Import Maps* section, select the heightmap file you want to import.

  - For the **normalized** heightmap, indicate the minimum and maximum heights obtained using the *Elevation info* node.
  - The **unnormalized** map does not require setting the height values.
- In the *Landscape Asset* section, set the actual size of your terrain in meters, the same as in *Size in meters* in *Instant Terra*.
- Check the *Current Data Density* value. It shows the meter-to-pixel ratio, the same as *Quad size* in *Instant Terra*.
- In the *Import settings* section, check the *Resolution* values. They define the resolution of the heightmap and correspond to *Width* and *Height* in *Instant Terra*. They are set automatically in most cases, but can also be adjusted, if required.


If the heightmap is represented by a **[tileset](#tiles)**, set the corresponding [data-filling](../../../../../objects/objects/terrain/landscape_terrain/landscape_layer_map.md#data_filling) pattern.


Click **Reimport**.
