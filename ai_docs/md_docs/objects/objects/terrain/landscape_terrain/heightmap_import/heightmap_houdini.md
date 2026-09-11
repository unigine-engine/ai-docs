# Importing Height Map from Houdini


[![](houdini_scheme.png)](houdini_scheme.png)


## Export Settings


### Dimensions


When exporting a heightmap from **Houdini**, pay attention to the following settings.


In the **HeightField** node:


![](houdini_base_properties.png)


- Recommended Division Mode is *By Axis*. It allows easily setting the traditional size of the texture (power of two) to be exported.
- *Grid Samples* � texture size in pixels.
- *Size* defines the terrain size in meters.


In the **HeightField Output** node:


![](houdini_output.png)


- Output type: Packed Raster
- Format: RGB (to make possible further editing in Photoshop, if required)
- Type: 16b or 32b Floating Point depending on your terrain
- Output Range:

  - For **unnormalized** heightmap � No Remapping
  - For **normalized** heightmap � Manual Remap, and define the range using the [expressions](https://www.sidefx.com/docs/houdini/expressions/bbox.html) bbox (�./�, D_YMIN) and bbox (�./�, D_YMAX) to calculate the Min and Max height automatically, or take this data from the node info: ![](houdini_height_info_icon.png)


### Tiling


For large-scale terrains (more than 8K), export in **tiles** is recommended, this helps to avoid RAM limitations, especially when using 32 bit textures. The minimum recommended tile size is 1024 to avoid visual tiling artifacts. To do that, in the export settings for the heightmap, enable *Divide into tiled maps*, set the preferable *Tile Size* and select *XY tile* as the *File Naming* method:


![](houdini_tile_export.png)


### Export Format


When exporting the terrain, select the suitable [export format](../../../../../editor2/assets_workflow/asset_types.md#texture). UNIGINE allows importing 8, 16, and 32-bit heightmaps.


> **Notice:** The **RAW** format is not supported.


## Importing


The exported heightmap is imported to UNIGINE as follows. In the **Landscape Layer Map**:


![](houdini_import.png)


- In the *Import Maps* section, select the heightmap file you want to import.

  - For the **normalized** heightmap, indicate the minimum and maximum height values.
  - The **unnormalized** map does not require setting the height values.
- In the *Landscape Asset* section, set the actual size of your terrain in meters, the same as in *Size* in Houdini.
- In the *Import settings* section, check the *Resolution* values. They define the resolution of the heightmap. They are set automatically in most cases, but can also be adjusted, if required.


If the heightmap is represented by a **[tileset](#tiles)**, set the corresponding [data-filling](../../../../../objects/objects/terrain/landscape_terrain/landscape_layer_map.md#data_filling) pattern.


Click **Reimport**.
