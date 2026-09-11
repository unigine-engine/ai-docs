# Quality


Output quality affects the final resolution of the terrain (and consequently the disk space required). The set of quality settings depends on the [Terrain Type](../../../../editor2/sandworm/interface/index.md#terrain_type).


## Object Landscape Terrain


![](olt_quality.png)


### Export Quality


The percentage value from 1 to 100. The percentage relates to the compression of the source data quality for the output. 100% quality means zero compression. Reducing the quality value increases the compression: at 50%, the output resolution is half the source resolution along each side. For example, if the source elevation data is 16k and *Export Quality* is 50%, the exported terrain has an 8k heightmap.


This setting is applied to raster data (imagery, elevation, and masks). Vector data are not affected.


### Compression


Compression serves to reduce the size of the `*.lmap` file, which may also speed up asynchronous streaming of tiles. In some cases, compression ratio may exceed **100:1**.


Enabling compression means that all *Landscape Layer Map* objects in the generated terrain will be compressed.


To enable or disable compression for an individual layer (or layers), you can use the parameters of the selected *[Landscape Layer Map](../../../../objects/objects/terrain/landscape_terrain/landscape_layer_map.md#lmap_compression)*.


By default, compression is disabled. The following compression options are available:


- **Lossless** � ensures absence of quality deterioration and decompresses graphic data to its original state.
- **Lossy** � provides a higher compression ratio but some information may be lost.
- **Custom** � compression rules can be customized according to your requirements. The following options are available in this mode: ![Custom Compression Parameters](compression.png) Supported compression methods: In addition, you can enable lossy compression for individual components of *Landscape Layer Maps*:

  - **Our Method** � recommended. UNIGINE compression method optimized for compressing 2D and 3D textures. It provides better results than **LZ4** and **Zlib** without quality reduction.
  - **Zlib** � for high compression ratio (can provide up to 2 times higher compression ratio, but takes up to 20 times longer).
  - **LZ4** � temporary option, planned to be removed in the upcoming releases.

  - *Heightmap* data
  - *Opacity* data
  - *Albedo* data
  - *Mask* data


## Object Terrain Global


The *Sandworm* tool defines the number of LODs, their visibility distances, and densities automatically. You can change these settings individually for elevation, imagery, and details, if necessary.


![](tg_quality_settings.png)


To modify LOD settings for the required data layer, disable the **Automatic** mode by unchecking the corresponding option.


In the manual mode, you can modify the *Density* and *Visibility Distance* values by double-clicking on the corresponding cell and entering the required value.


Use the **+** (plus) button to add a LOD, or **-** (minus) to remove one.


![](quality_lods.gif)


> **Notice:** In the manual mode, the LOD density should be specified more accurately, as this value determines the size of the [tileset of the generated LOD](../../../../objects/objects/terrain/terrain_global/index.md#tiling): the higher the LOD density, the bigger the LOD tileset (the density is multiplied by 128 � the size of a single tile). Specifying high values may lead to visual artifacts at the edges of the terrain.
