# Sources and Their Parameters


This article gives an overview of the source types and their common parameters.


## Types of Source Layers


### Terrain Sources


![Terrain Sources](terrain_sources.png)


[Elevation and Imagery](../../../editor2/sandworm/sources/elevation_imagery/index.md) are the basis required for the terrain generation.


[Mask](../../../editor2/sandworm/sources/mask/index.md) is a useful tool to automatically generate vegetation in specific areas of the terrain and create terrain details that can be used to modify the visual representation of the terrain ([Terrain Global](../../../objects/objects/terrain/terrain_global/details/index.md) or [Landscape Terrain](../../../objects/objects/terrain/landscape_terrain/details.md)).


### Objects


![Objects](objects.png)


*Sandworm* allows placing objects on the generated terrain according to the georeferenced data, such as:


- [Trees and grass](../../../editor2/sandworm/sources/vegetation/index.md)
- [Roads](../../../editor2/sandworm/sources/roads/index.md)
- [Landmarks and individual buildings and structures](../../../editor2/sandworm/sources/points/index.md)
- [Fences, pipelines, powerlines, and other objects repeated along a line](../../../editor2/sandworm/sources/splines/index.md)
- [Rivers](../../../editor2/sandworm/sources/rivers/index.md)
- [Urban districts consisting of numerous houses made of various materials](../../../editor2/sandworm/sources/buildings/index.md)


Object names may be set and changed as necessary either in the *Sources* panel or in the *Parameters* panel. This name is also used for the generated objects in the *World Nodes* hierarchy window.


![Editing the object name](object_name.png)


## Adding a Data Source


*Sandworm* works with both offline and online data sources:


![](source_type.png)


- **[Georeferenced Image](#georeferenced_image)** � for adding offline data stored on the PC
- **[TMS](#tms)** � for using online data by adding the link


> **Notice:** If you don't want to generate an added source, you can either delete or disable it in the *Terrain Layers* or *Objects* list of the *Sources* panel.


### Georeferenced Image Source


*Georeferenced Images* are the data files already available on a PC:


![](georef_parameters.png)


- **Assets** � files that are added to the [file system](../../../principles/filesystem/index_cpp.md) and represent a part of the project. Depending on the size of assets, they can be stored in the `/data` directory or added as a *[mount](../../../principles/filesystem/index_cpp.md#mount_points)*. This approach is recommended for teamwork. Vector data is taken as an asset in `*.shp`, `*.geojson`, and `*.sxf`; raster data - in any format the Editor imports as a texture. Anything else has to be added as an [External File](#data_sources) - see the [list of supported formats](../../../editor2/sandworm/index.md#data_formats). > **Notice:** We recommend importing image files as *Unchanged*, in order to avoid creating the unnecessary runtime files.
- **External Files** � files stored on the PC that are not a part of the file system. This type of data source may be helpful if the file extension is unknown to the file system. However, keep in mind that if you share this project, the path to the external file has to be updated accordingly. See the [list of supported formats](../../../editor2/sandworm/index.md#data_formats).


**File location** � path to the file or group of files to be added. Multiple selection allows adding a number of files simultaneously and adds them as separate layers.


### TMS Source


The *TMS* source type is designed for using *Tile Map Services* for terrain generation. This option is available for both raster and vector data types.


To download the data for this source type, you need to set the [boundaries](../../../editor2/sandworm/sources/index.md#boundaries).


![](tms_parameters.png)


| TMS URL | A URL of the online data source. You can use any of the suggested sources or add your own. The scope of data is defined by the [boundaries](../../../editor2/sandworm/sources/index.md#boundaries). **Adding Custom URLs** To add a URL, select the *Add URL* line in the drop-down window or click the ![](edit.png) image on the right: ![](add_url.png) The following window will open to manage URLs: ![](manage_urls.png) **Requirements to TMS URLs:** A link to a Tile Map Service inserted as the URL should start with http:// or https:// and have x, y, and z embraced into curly brackets ({}). For example: - The link to the OpenStreetMap tile map service (http://a.tile.openstreetmap.org/z/x/y.png) should be used as follows: ***http://a.tile.openstreetmap.org/{z}/{x}/{y}.png*** - The link to *ArcGIS Online* data (https://server.arcgisonline.com/ArcGIS/rest/services/World_Topo_Map/MapServer/tile/z/y/x.png) should be used as follows: ***https://server.arcgisonline.com/ArcGIS/rest/services/World_Topo_Map/MapServer/tile/{z}/{y}/{x}.png*** For sources that require tokens, the link should be arranged in the following way: *https://api.mapbox.com/v4/mapbox.terrain-rgb/{z}/{x}/{y}.pngraw?access_token=**your_token*** > **Notice:** The sources that require login and password input are currently not supported. |
|---|---|
| Zoom Level | *Zoom Level* specifies the scale of the source data to be downloaded. Data providers have their own zoom levels defined; therefore, this value depends on the source. For example, *OSM* has the following [zoom levels](https://wiki.openstreetmap.org/wiki/Zoom_levels). Higher zoom levels provide a more detailed data but affect the generation speed and create a higher load. The available values are 0 to 23, 5 by default. |
| Projection | Projection of the tile source (EPSG code): EPSG:3857 (Web Mercator) or EPSG:3395 (World Mercator). Choosing the wrong one misplaces every downloaded tile. |
| NoData Value (*Elevation* only) | The pixel value to be interpreted as [NoData](../../../editor2/sandworm/generation/nodata/index.md). A *TMS* source carries no metadata at all, so this field is the only way to declare a NoData value for it. Tick the checkbox next to the field to enable it: while the checkbox is clear, no value is declared. The field takes values from -1e9 to 1e9 with 4 decimal places; on choosing the value, see [NoData Value for Elevation Sources](../../../editor2/sandworm/sources/elevation_imagery/index.md#nodata). For a layer that already exists, click *Update Elevation Layer* to apply the change. |


## Overlapping Sources


Sources may overlap. Where several sources cover the same area, the sources are composited from the coarsest to the finest, so the one with the higher data density � more pixels per unit of terrain � ends up on top and its opaque pixels win. This is what makes [high-resolution insets](../../../editor2/sandworm/index.md#insets) work: a small detailed source added over a large coarse one replaces its data exactly where the detailed source has data of its own.


> **Notice:** The *Move to Foreground* and *Move to Background* commands of the [context menu](../../../editor2/sandworm/interface/index.md#context_menu) change the drawing order in the *Map* panel only. They do not affect which source is used for generation.


## Setting Boundaries


Boundaries define the scope of the source data used for generation. They are optional for a *Georeferenced Image*: if you set none, all data available in the file is used.


They are mandatory for a *TMS* source � it cannot be created until the boundaries are set, because they tell *Sandworm* which tiles to download.


Boundaries are marked green with points as the corners:


![](boundaries.jpg)


You can set points manually or enclose the area visible in the *Map* panel and move the points, if necessary, using the [boundary tools](../../../editor2/sandworm/interface/index.md#boundaries) of the *Parameters* panel:


![](boundaries_tools.png)


## Preview


The *Preview* button generates the data preview in the *Map* panel.


Regenerate the preview after adding or replacing a data source, and after changing the source boundaries.


> **Notice:** The preview generation process may take much time for heavy source files, therefore you can [cancel it](../../../editor2/sandworm/interface/index.md#cancel_preview), and [generate later](../../../editor2/sandworm/interface/index.md#context_menu), if required.


## Filtering Vector Data


> **Notice:** Filter settings specific to masks are described in [Mask Parameters](../../../editor2/sandworm/sources/mask/index.md).


Filters are used to pick specific data from a vector source and create the required types of objects only. By default, no filters are set and all data available in the source are used to generate the specified object.


> **Notice:** Currently, only `*.shp`, `*.geojson`, and `*.sxf` are supported as assets. Therefore, if you have other types of files, you can try to add them as *External Files*. See the [list of supported formats](../../../editor2/sandworm/index.md#data_formats).


Add a vector source to set filters. As you select an already created object to modify its filters, ensure that you have selected a source in the source list of the *Parameters* panel:


![](selected_vector_source.png)


Sources in this list can also be disabled and deleted. If you delete the only source, the object also will be deleted.


The **Filter** is a set of rules created using the **Attributes**.


![](filters.png)


| Binary operation ![Binary Operators](binary_op.png) | Binary operators AND and OR that allow combining several filters. |
|---|---|
| Attribute name | Name of the attribute available in the attribute table. |
| Attribute condition ![Attribute Conditions](attr_condition.png) | The available conditions are: =, !=, >, <, ANY. ANY generates all the objects that have any value assigned for the selected Attribute. > **Warning:** When using > and <, make sure that the selected Attribute value type is a number. String comparison may cause issues. |
| Attribute value | Value of the attribute available in the attribute table. |
| Attribute Table ![Open Table Button](table_sign.png) | Opens the attribute table, which allows setting the Attribute Name and Attribute Value in one click. Clicking on a value fills in the corresponding fields. Double click fills in the fields and closes the table. ![Attributes Table](attributes_table.png) |
| Remove filter ![Remove Filter Button](remove.png) | Removes the corresponding filter from the list. |
| Add ![Add Filter Button](add_button.png) | Adds one more filter. |
| Apply Filters for Preview | Applies the filters to the preview, so that only the data passing them is shown. When disabled, the preview shows all vector objects and masks of the source unfiltered, and is not regenerated when a filter changes. This is a single tool-wide setting, enabled by default: switching it for one source switches it for every source, object, and mask � in the current project and in any project you open afterwards. |
| Copy filters ![Copy Filters Button](share_button.png) | Opens the window to copy all filters from the current source to the selected sources. Filters can only be copied between the sources of one object or one mask: ![Copy Filters Window](copy_filters.png) If you change anything in filters that you have already copied, and want these changes to be applied to other sources, you need to copy the filters once again. All filters of the selected sources will be replaced with the filters of the current source. |
| Delete all filters ![Delete Filters Button](../interface/trash_bin.png) | Deletes all added filters. |
