# Landscape Layer Map


![](landscape_layers.png)


*Landscape Layer Map* object represents a rectangular *[Landscape Terrain](../../../../objects/objects/terrain/landscape_terrain/index.md)* layer and stores the data used for rendering in an [`.lmap`](../../../../editor2/assets_workflow/asset_types.md#lmap) asset:


- **Height** map used to generate the geometry of *Landscape Terrain*,
- **Albedo** texture representing color data,
- **20 single-channel mask** textures.


You can create a new *Landscape Layer Map* either from scratch, [sculpting it](../../../../editor2/brush_editor/index.md) with an extendable set of brushes available out-of-the-box, or using imported data (images or tilesets), be it an arbitrary terrain generated in terrain generator software (e.g., *World Machine*), or real digital elevation maps and satellite imagery data.


> **Notice:** *Landscape Layer Map* is designed as a shared data pool, the graphic data of which can be used to add [details](../../../../objects/objects/terrain/landscape_terrain/index.md#details) to the *Landscape Terrain* surface, used in [logic](../../../../api/library/objects/landscape_terrain/class.landscapefetch_cpp.md#getMask_int_float) (e.g. as a land cover classification map) and by other objects as well, such as [Grass](../../../../objects/objects/grass/index.md#terrain_mask), for example.


You can place layer maps anywhere in the scene by moving, scaling and rotating the node (rotation is available around the Z axis only). By blending different *Landscape Layer Maps* you can modify the terrain even at run time.


Depending on the size and resolution of your landscape, the size of the data can be quite large. You can use lossless and lossy [compression](#lmap_compression) options to reduce the size of the `.lmap` file.


### See Also


- The *[LandscapeLayerMap](../../../../api/library/objects/landscape_terrain/class.landscapelayermap_cpp.md)* class to manage parameters of the *Landscape Layer Map* via API
- The *[LandscapeMapFileCreator](../../../../api/library/objects/landscape_terrain/class.landscapemapfilecreator_cpp.md)* class to generate `.lmap` files via API
- The *[LandscapeMapFileSettings](../../../../api/library/objects/landscape_terrain/class.landscapemapfilesettings_cpp.md)* class to load, modify, and apply *Landscape Layer Map* settings stored in a `.lmap` file via API
- The *[Editing *Landscape Terrain*](../../../../editor2/brush_editor/index.md)* article to learn about Brush Editor


## Creating a Landscape Layer Map


Create a new *Landscape Layer Map* via either of the following ways:


- **By creating a node**

  1. In the *Create* menu, select *Landscape -> Landscape Layer Map* and place the new *Landscape Layer Map* node in the scene. ![](create_layer_map.png)
  2. By default, the map has the white, flat and read-only `landscape_layer_map_base.lmap` asset set in the **Landscape** parameter. Click on the word *create* or ![Create](detail_button_create.png) to create a new landscape layer asset. ![](layer_map_create_asset_button.png)
- **By creating an asset**

  1. In the *Asset Browser* right-click for the context menu, select *Create Landscape Layer Map* and specify a name for the new `lmap` asset. ![](layer_map_create_asset_bro.png)
  2. Drag the asset to the Editor viewport and place a new *Landscape Layer Map* in the scene.


> **Notice:** If the current world contains no *[Landscape Terrain](../../../../objects/objects/terrain/landscape_terrain/index.md)* object, which is required for terrain rendering, a new one will be created automatically and set as the parent node for the new *Landscape Layer Map*.


### Specifying Graphic Data


- **Generating from files:**

  1. Set the [**Data Filling**](#data_filling) option to *From Tileset*.
  2. Depending on the desired way to access to the resources, choose the value of the **[Data Sources](#data_sources)** parameter:

    - **Assets**. Use available imported textures, which is a pretty good option for small and moderate terrains.
    - **External Files**. Provide full paths to the resources (e.g. a network drive). A better option for large terrains with extremely dense graphic data.
  3. Specify the resources: albedo and height textures (or texture tilesets) and up to 20 mask textures. In the case of using tilesets, specify only first tiles and appropriate naming patterns.
  4. Adjust other import settings. For instance, you can redefine the [**Resolution**](#resolution) of the *Landscape Layer Map* textures.
  5. Click **Reimport** to load the provided resources.
  6. Modify the layer using [Brush Editor](../../../../editor2/brush_editor/index.md).
- **Sculpting from scratch:**

  1. Set the **[Data Filling](#data_filling)** option to *Manual*.
  2. Choose the [**Resolution**](#resolution) of the *LandscapeLayerMap* textures and click **Reimport** to apply changes.
  3. Click **Brush Edit** and open [Brush Editor](../../../../editor2/brush_editor/index.md) to draw over the layer map surface and thus sculpt the layer from scratch.


> **Notice:** Keep in mind that reimporting will clear all modifications made via the Brush Editor tool earlier!


Watch a quick video guide below on creating and editing a *Landscape Terrain* and Layer Maps:


## Size and Density of Graphic Data


The spatial size of *Landscape Layer Maps* is limited only by [precision of coordinates](../../../../code/double_precision/index.md). However, the resolution of graphic data used has the direct influence on the size of an `*.lmap` asset on the hard drive.


The *density* of a *Landscape Layer Map* data is calculated as its [**Spatial Size**](#size) divided by the [**Resolution**](#resolution) of graphic data and expressed in *meters/pixel* (mpx). Knowing the target size and density of your *Landscape Terrain* layer, you can estimate the resolution of input textures required for achieving the desired quality as follows:

 ResolutionX = SizeX / Density ResolutionY = SizeY / Density
> **Notice:** The final density of the terrain graphic data is limited by the [render parameters](../../../../objects/objects/terrain/landscape_terrain/settings.md#render).


For example, if you need to create a square terrain 100 � 100 km and with 3 mpx density, you will need to prepare 32768 � 32768 px textures. You can slice huge textures to tilesets with proper [naming](#naming_type), to operate on regular size textures (e.g., 8�8 textures each of 4096�4096 pixels).


Regardless of the bit depth of input textures, uncompressed graphic data of any *Landscape Layer Map* is saved using the following formats:


- Two **R32F** textures are used to store the **[Height](#height_texture)** and **[Height Opacity](#heightmap_opacity)** data (32 bits per pixel for each one).
- A single **RGBA8** texture keeps the **[Albedo](#albedo_texture)** data including opacity (four 8-bit-per-pixel channels).
- Five **RGBA8** textures are used to store **[20 Masks](#mask_texture)** and the same number of textures is used for **[Masks Opacity](#mask_opacity)** data (four 8-bit-per-pixel channels for each one).


Thus, if all components are used each pixel of graphic data takes more than 50 bytes on the hard drive, without service data taken into account. Putting it all together, this is how the size of an `*.lmap` asset depends on the resolution of the data used and components enabled approximately:


| **Resolution, px*** | Approximate size | Height | Albedo | Each 4 Masks |  |  |
|---|---|---|---|---|---|---|
| Color | Opacity | Color | Opacity |  |  |  |
| **1024�1024** | 74 Mb | 5.7 Mb | 5.7 Mb | 5.7 Mb | 5.7 Mb | 5.7 Mb |
| **2048�2048** | 295 Mb | 22.7 Mb | 22.7 Mb | 22.7 Mb | 22.7 Mb | 22.7 Mb |
| **4096�4096** | 1.1 Gb | 91 Mb | 91 Mb | 91 Mb | 91 Mb | 91 Mb |
| **8192�8192** | 4.6 Gb | 364 Mb | 364 Mb | 364 Mb | 364 Mb | 364 Mb |
| **16384�16384** | 18.3 Gb | 1.41 Gb | 1.41 Gb | 1.41 Gb | 1.41 Gb | 1.41 Gb |
| **32768�32768** | 74 Gb | 5.7 Gb | 5.7 Gb | 5.7 Gb | 5.7 Gb | 5.7 Gb |
| **65536�65536** | 295 Gb | 22.7 Gb | 22.7 Gb | 22.7 Gb | 22.7 Gb | 22.7 Gb |


**The highest resolution is taken from the input textures.*


When enabling/disabling any component in the **[Import Settings](#import_parameters)** and reimporting data, the size of the file increases or decreases correspondingly. **20 Masks** are grouped into 5 textures each of four channels (*Masks 0-3*, .., *Masks 16-19*), therefore, enabling at least one mask in a group of four will be treated as if all four masks in the group were enabled in terms of the asset size.


Although, the format of *Landscape Layer Map* assets implies asynchronous streaming of data of only necessary tiles, the perfomance might be an issue on workstations utilizing hard drives with poor throughput capacity. In this case, consider splitting a huge *Landscape Layer Map* into several smaller ones and engaging [compression](#lmap_compression). Make note that using performant SSDs is preferable.


> **Notice:** Refinement of the *Landscape Terrain* graphic data using [details](../../../../objects/objects/terrain/landscape_terrain/details.md) enables you to achieve higher density without affecting the size of *Landscape Layer Maps*.


### Compression


Compression options serve for reduction of the size of the `*.lmap` file, which may also speed up asynchronous streaming of tiles. In some cases, compression ratio may exceed 100:1.


Supported compression methods:


- **Our Method** � recommended. UNIGINE compression method optimized for compressing 2D and 3D textures. It provides better results than **LZ4** and **Zlib** without quality reduction.
- **Zlib** � for high compression ratio (can provide up to 2 times higher compression ratio, but takes up to 20 times longer).
- **LZ4** � temporary option, planned to be removed in the upcoming releases.


*Lossless* and *Lossy* compression options are available. When it is needed to apply any changes, the graphic data needs to be decompressed first. Therefore, depending on applicability, these options have different advantages:


- **Lossless** compression ensures absence of quality deterioration and decompresses graphic data to its original state.
- **Lossy** compression provides a higher compression ratio but some information may be lost.


> **Warning:** When you repeatedly decompress/compress the data using Lossy algorithm, the quality will deteriorate every time the data is compressed.


It is recommended to develop projects against Lossless compression algorithms (or with compression disabled) and apply a Lossy compression option when making the final build.


## Landscape Layer Map Parameters


### Landscape Asset Parameters


![](layer_map_common_parameters.png)


| Size | Width and Length, in units (meters). Click **Edit Size** to toggle the size editing mode. |
|---|---|
| Attenuation Distance | Distance of the transparency attenuation, starting from the edge of the map. |
| Current Data Density | *Landscape Layer Map* density calculated as the ratio of the [Size](#size) to the [Resolution](#resolution), in meters/pixel. > **Notice:** The ratio is calculated for both dimensions separately: the *spatial Width* is divided by the *texture Width*, the same is done for the *Length* and the *texture Height*, and the maximum ratio value is considered the Current Data Density in meters/pixel. |
| Landscape | [.lmap](../../../../editor2/assets_workflow/asset_types.md#lmap) asset to store the landscape data. By default, it is the blank read-only `landscape_layer_map_base.lmap` asset, to edit the layer map you can create a new asset by using the ![](detail_button_create.png) *Create* button or specify an existing one. **Brush Edit** opens the [Brush Editor](../../../../editor2/brush_editor/index.md). > **Notice:** Several *Landscape Layer Maps* can refer to the same `.lmap` asset without extra memory required. |
| Height Scale | Scale multiplier along the Z axis. |
| Order | The layer rendering order used in [layers blending](../../../../objects/objects/terrain/landscape_terrain/index.md#layers_blending) (higher numbers on top). |
| Collision | Collision with the map. |
| Intersection | Intersection with the map. |
| Intersection Bicubic Filter | Enables bicubic filtering for intersection detection. |
| Culling | Streaming is based on using previously loaded geometry to define what is going to be streamed next. This option enables uploading preliminary low-level data of all maps to CPU to be used for initializing the streaming. If disabled, only low-level data of the base map is uploaded on CPU. |


### Import Settings


Import Settings are the settings of the [`.lmap`](../../../../editor2/assets_workflow/asset_types.md#lmap) asset associated with the *Landscape Layer Map* node.


![](import_settings_new.png)


There is a set of buttons to work with import settings:


![](layer_map_import_buttons.png)


| Restore Defaults | Reset all settings to the default values. |
|---|---|
| Apply | Save and apply changes to the [import parameters](#import_parameters) without reloading graphic resources. Click *Apply* after selecting a compression method option. |
| Reimport | Reload all graphic resources with respect to the specified [import parameters](#import_parameters). Click *Reimport* after making any changes to the import settings to apply them. |
| Cancel | Discard changes made to the [import parameters](#import_parameters). |


Import settings:


| Compression | Compression options: - **Off** � compression is disabled (maximum file size). - **Lossless** � lossless compression **Our Method** is enabled, all lossy compressions are disabled. - **Lossy** � lossless compression **Our Method** is enabled, all lossy compressions are enabled for all data (*Lossy Compression* checkboxes are checked). > **Warning:** Use of Lossy compression will lead to quality deterioration every time the data is compressed. - **Custom** � *Compression Method* combo box appears below, *Lossy Compression* checkbox appears for *Albedo* and *Masks*. |
|---|---|
| Compression Method | Compression method options: - **Our Method** � recommended. UNIGINE compression method optimized for compressing 2D and 3D textures. It provides better results than **LZ4** and **Zlib** without deteriorating the quality. - **Zlib** � for high compression ratio (can provide up to 2 times higher compression ratio, but takes up to 20 times longer). - **LZ4** � temporary option, planned to be removed in the upcoming releases. |
| Data Filling | Origin of terrain data: - **Manual** � this type of data is selected for work with brushes. > **Notice:** The only setting available for this option is **Resolution**. - **From Tileset** � this type of data is used to add any available data sources. |
| Data Sources | Where data is taken from: - **Assets** � available asset files. This option is good for small terrains. - **External files** � absolute path to the file is indicated (for example, network disk). A recommended option in case of creating a huge terrain using high-density graphic data. > **Notice:** The engine doesn't track the changes made to external files. If there are some changes, you can update graphic data via the [*Reimport*](#reimport) button. |
| Resolution | Resolution of maps limited only by available video memory. The following values are available: - **Manual** � set by the user. Graphic data from textures is remapped to fit the resolution. - **Auto** � automatically detected from the specified textures, the resolution of the biggest texture is used. If a tileset is specified the resulting resolution of all tiles combined will be considered. |
| Flip Y | Flip tiles along the Y axis. |
| Naming Type | The source tileset layout type. The following values are available: - **Row Column** � the row-column based tileset. When set, each tile of the source tileset is determined by the row and column numbers (e.g. `tileset_x0_y2.png`). - **Indexed** � the index-based tileset. When set, each tile of the source tileset is determined by the index (e.g. `tileset_0.png`). The number of columns of the source tileset is specified in the *Number of Columns* field. |
| Pattern Matching | - **Auto** � automatically select the naming pattern. - **Manual** � manually specify the naming pattern. |
| Pattern | A string naming pattern (e.g. *_x%X_y%Y* for the *Row Column* naming type or *_%X* for the *Indexed* type). |
| Number of Columns | The number of columns in the tileset. |
| Horizontal Order | Horizontal loading direction of the source tileset. - Left -> Right - Right -> Left |
| Vertical Order | Vertical loading direction of the source tileset. - Top -> Down - Down -> Top |


### Heightmap


> **Notice:** When **Data Filling** is *Manual*, the only settings available are *Opacity Lossy compression* and *Blending Mode*.


![](heightmap.png)


| Heightmap data | - *None* � no data of this type is available at all. - *Only Heightmap* � load the specified heightmap as is. In this case, data of this layer will always overlap data of underlying layers. - *Heightmap with Opacity* � load the specified heightmap with an additional opacity mask applied. The mode is useful for blending height data with data of underlying layers. |
|---|---|
| Heightmap | A single-channel texture to be treated as the Heightmap. To use a tileset, specify the first tile here. Height values can be interpreted the following ways: - *Normalized* � normalized height values are mapped to the range specified by the Min and Max Height values. - *Unnormalized* � the height values are used as is. It is recommended to use 16bit or 32bit sources for height as lower bit depth may not provide sufficient quality: ![](terrain_height_8bit.png) ![](terrain_height_16bit.png) |
| Height | Min/Max � the values used to transform the value [0,1] stored in the heightmap to meters. |
| Attenuation Distance | Distance of the transparency attenuation, starting from the edge of the map. |
| Height opacity | Sets the height opacity map and channel where data is stored. |
| Opacity Lossy Compression | Enables lossy compression. |
| Blending mode | - *[Alpha-Blend](../../../../principles/render/blending/index.md#id_2)* � the colors of the heightmap of this layer map and the underlying one are blended. - *[Additive](../../../../principles/render/blending/index.md#id_8)* � data of the layer map is added atop. |


### Albedo


> **Notice:** When **Data Filling** is *Manual*, the only settings available are *Lossy Compression* and *Albedo Blending*.


![](albedo.png)


| Lossy Compression | Enables lossy compression. |
|---|---|
| Albedo Data | - *None* � no data of this type is available at all. - *Only Albedo* � load the specified albedo data as is. In this case, data of this layer will always overlap data of underlying layers. - *Albedo with Opacity* � load the specified albedo map with an additional opacity mask applied. The mode is useful for blending albedo data with data of underlying layers. |
| Albedo Color | Albedo color image. |
| Attenuation Distance | Distance of the transparency attenuation, starting from the edge of the map. |
| Albedo opacity | Sets the albedo opacity map and channel where data is stored. |
| Albedo Blending | - *[Alpha-Blend](../../../../principles/render/blending/index.md#id_2)* � the colors of this layer map and the underlying one are blended. - *[Additive](../../../../principles/render/blending/index.md#id_8)* � data of the layer map is added atop. - *[Overlay](../../../../principles/render/blending/index.md#id_1)* � added data replaces the data below it. - *[Multiplicative](../../../../principles/render/blending/index.md#id_9)* � the albedo colors are multiplied. |


### Masks


> **Notice:** When **Data Filling** is *Manual*, the only settings available are *Lossy Compression*, *Name* and *Blending*.


![](masks.png)


| Lossy Compression | Enables lossy compression. |
|---|---|
| Name | The mask name, which is synchronized with the current active [ObjectLandscapeTerrain](../../../../objects/objects/terrain/landscape_terrain/index.md#details). On change, no reimport required. > **Notice:** Names of masks are stored by *Landscape Terrain* objects, i.e. names shown in the parameters of a *Landscape Layer Map* will change in correspondence with the current enabled *Landscape Terrain*. |
| Data | - *None* � no data of this type is available at all. - *Only Mask* � load the specified texture as is. In this case, data of this layer will always overlap data of underlying layers. - *Mask with Opacity* � load the specified mask with an additional opacity mask applied. The mode is useful for blending the mask with data of underlying layers. |
| Color | The image and its channel to be applied as mask to the *LandscapeLayerMap*. > **Notice:** Instead of specifying a single-color image for the mask, you can set the [**Default Value**](../../../../objects/objects/terrain/landscape_terrain/index.md#mask_default_value) for it and avoid excessive data loading. |
| Attenuation Distance | Distance of the transparency attenuation, starting from the edge of the map. |
| Opacity | Sets the opacity map and channel where data is stored. |
| Blending | Mode of blending this detail layer with other data layers: - *[Alpha-Blend](../../../../principles/render/blending/index.md#id_2)* � the corresponding masks of this layer map and the underlying one are blended. - *[Additive](../../../../principles/render/blending/index.md#id_8)* � data of the layer map is added atop. - *[Overlay](../../../../principles/render/blending/index.md#id_1)* � added data replaces the data below it. - *[Multiplicative](../../../../principles/render/blending/index.md#id_9)* � the colors of the masks are multiplied. |


> **Notice:** Enter the *Masks Debug* mode by using the **[Landscape Masks](../../../../editor2/using_visual_helpers/index.md#landscape_masks)** helper in the Editor or via the `render_show_landscape_mask N` console command, where *N* is the index of a mask from 1 to 20.
