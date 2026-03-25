# Sources and Their Parameters


This articles overviews the types of sources and their common parameters.


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
- [Landmarks, specific buildings and structures, fences, pipelines, and other lengthy structures](../../../editor2/sandworm/sources/points/index.md)
- [Urban disctricts consisting of numerous houses made of various materials](../../../editor2/sandworm/sources/buildings/index.md)


Object names may be set and changed as necessary either in the *Sources* or in the *Parameters* window. This name is also used for the generated objects in the *World Nodes* hierarchy window.


![Editing the object name](object_name.png)


## Adding a Data Source


*Sandworm* works with both offline and online data sources:


![](source_type.png)


- **[Georeferenced Image](#georeferenced_image)** — for adding offline data stored on the PC
- **[TMS](#tms)** — for using online data by adding the link


> **Notice:** If you don't want to generate an added source, you can either delete or disable it in the *Sources* list.


### Georeferenced Image Source


*Georeferenced Images* are the data files already available on a PC:


![](georef_parameters.png)


- **Assets** — files that are added to the [file system](../../../principles/filesystem/index_cpp.md) and represent a part of the project. Depending on the size of assets, they can be stored in the `/data` directory or added as a *[mount](../../../principles/filesystem/index_cpp.md#mount_points)*. This approach is recommended for teamwork. > **Notice:** We recommend importing image files as *Unchanged*, in order to avoid creating the unnecessary runtime files.
- **External Files** — files stored on the PC that are not a part of the file system. This type of data source may be helpful if the file extension is unknown to the file system. However, keep in mind that if you share this project, the path to the external file has to be updated accordingly.


**File location** — path to the file or group of files to be added. Multiple selection allows adding a number of files simultaneously and adds them as separate layers.


### TMS Source


The *TMS* source type is designed for using *Tile Map Services* for terrain generation. This option is available for both raster and vector data types.


To download the data for this source type, you need to set the [boundaries](../../../editor2/sandworm/sources/index.md#boundaries).


![](tms_parameters.png)


| TMS URL | A URL of the online data source. You can use any of the suggested sources or add your own. The scope of data is defined by the [boundaries](../../../editor2/sandworm/sources/index.md#boundaries). **Adding Custom URLs** To add a URL, select the *Add URL* line in the drop-down window or click the ![](edit.png) image on the right: ![](add_url.png) The following window will open to manage URLs: ![](manage_urls.png) **Requirements to TMS URLs:** A link to a Tile Map Service inserted as the URL should have x, y, and z embraced into curly brackets ({}). For example: - The link to the OpenStreetMap tile map service (http://a.tile.openstreetmap.org/z/x/y.png) should be used as follows: ***http://a.tile.openstreetmap.org/{z}/{x}/{y}.png*** - The link to *ArcGIS Online* data (https://server.arcgisonline.com/ArcGIS/rest/services/World_Topo_Map/MapServer/tile/z/y/x.png) should be used as follows: ***https://server.arcgisonline.com/ArcGIS/rest/services/World_Topo_Map/MapServer/tile/{z}/{y}/{x}.png*** For sources that require tokens, the link should be arranged in the following way: *https://api.mapbox.com/v4/mapbox.terrain-rgb/{z}/{x}/{y}.pngraw?access_token=**your_token*** > **Notice:** The sources that require login and password input are currently not supported. |
|---|---|
| Zoom Level | Zoom level specifies the scale of the source data to be downloaded. Data providers have their own zoom levels defined; therefore, this value depends on the source. For example, *OSM* has the following [zoom levels](https://wiki.openstreetmap.org/wiki/Zoom_levels). Higher zoom levels provide a more detailed data but affect the generation speed and create a higher load. |


## Setting Boundaries


Boundaries define the scope of the source source data that is used for generation. By default, all data of a source are used for generation. That means if you don't set the boundaries for a *Georeferenced Image*, all data available in it will be used for generation.


A TMS source won't be created without setting the boundaries.


Boundaries are marked green with points as the corners:


![](boundaries.jpg)


You can set points manually or enclose the area visible in the *Map* view and move the points, if necessary, using the following tools:


![](boundaries_tools.png)


| ![Edit Boundaries Button](../interface/edit_boundaries.png) | **Modifying boundaries**: click and drag the point on the preview map or change its coordinates on the *[Parameters](../../../editor2/sandworm/interface/index.md#parameters_panel)* panel. **Adding points**: hold ALT and click the left mouse button in the *Map* window. **Deleting points and boundaries**: right-click on a single point in the *Map* window and click *Remove* in the context menu. You can also select a point in the *Map* window and press *Delete* on the keyboard. |
|---|---|
| ![Enclose Visible Area Button](../interface/set_visible_area.png) | **Enclosing the area** visible in the *Map* window in the boundaries. The data will be uploaded for the area within these boundaries. You can move the points defining the boundaries to adjust the area as necessary. |
| ![Delete Boundaries Button](../interface/trash_bin.png) | **Removing the boundaries** for the selected source. If the boundaries are not set (or deleted), all data available in the source and within the *[Export Area](../../../editor2/sandworm/generation/export_area/index.md)* will be uploaded. |


## Preview


The *Preview* button generates the data preview in the *Map* window.


Updating the preview is required when you change the source borders.


## Filtering Vector Data


**Filtering of mask data is described [here](../../../editor2/sandworm/sources/mask/index.md).**


Filters are used to pick specific data from a vector source and create the required types of objects only. By default, no filters are set and all data available in the source are used to generate the specified object.


> **Notice:** Currently, only `*.shp` and `*.geojson` are supported as assets. Therefore, if you have other types of files, you can try to add them as *External Files*.


Add a vector source to set filters. As you select an already created object to modify its filters, ensure that you have selected a source in the sources list:


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
| Copy filters ![Copy Filters Button](share_button.png) | Opens the window to copy all filters from the current source to the selected sources: ![Copy Filters Window](copy_filters.png) If you change anything in filters that you have already copied, and want these changes to be applied to other sources, you need to copy the filters once again. All filters of the selected sources will be replaced with the filters of the current source. |
| Delete all filters ![Delete Filters Button](../interface/trash_bin.png) | Deletes all added filters. |
