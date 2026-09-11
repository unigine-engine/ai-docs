# Questions and Answers


This article aims to help with questions that arise when you use the *Sandworm* terrain generation tool.


There is a number of **general tips** that may be useful for overall understanding:


- Open the Editor console (*Windows -> Console*). If something goes wrong, a console message might be useful in explaining the situation. ![Console errors](console_errors.png) *Example of console errors*
- If you suspect that the heightmap has some issues, you can enable the debug mode to check: *[Rendering Debug](../../../editor2/using_visual_helpers/index.md) -> Opacity World Normal*.
- Don�t worry about the number of [triangles](../../../objects/objects/terrain/landscape_terrain/index.md#tiling) in *ObjectLandscapeTerrain*. This object was designed in a way that millions of polygons wouldn�t affect the framerate that much.
- [Clear cache](../../../editor2/sandworm/generation/output_dir_files/index.md#clear_cache) before you start terrain generation: click the ![](../interface/trash_bin.png) button near the cache address line in the bottom left corner of the *Sandworm* window.


<details>
<summary>What is the difference between ObjectTerrainGlobal and ObjectLandscapeTerrain? | Click to close</summary>

**What is the difference between ObjectTerrainGlobal and ObjectLandscapeTerrain?**


Currently, UNIGINE has two objects that are used for terrain: *[ObjectTerrainGlobal](../../../objects/objects/terrain/terrain_global/index.md)*, which has long been in use, and comparatively recently introduced *[ObjectLandscapeTerrain](../../../objects/objects/terrain/landscape_terrain/index.md)*, which has many improvements.


These two terrain objects can be generated using the *Sandworm* Tool.


The *[Sandworm](../../../editor2/sandworm/index.md)* Tool as well as *ObjectLandscapeTerrain* were developed to solve the problems, which have accumulated over the years, and extend the functionality.

</details>


<details>
<summary>Where can I take the geodata? | Click to close</summary>

**Where can I take the geodata?**


As a rule, access to private TMS servers is not free, however, there are free data sources supported by donations. If you are not in the mood of searching, you can check the list [here](https://wiki.openstreetmap.org/wiki/Tile_servers). Keep in mind that every server has its own features and check the information in description.


**Heights**


For example, you can try the [mapbox](https://www.mapbox.com/) service. Register there in order to obtain your own token and access, for more details see [this page](https://docs.mapbox.com/help/troubleshooting/access-elevation-data/).


Free access limits the number of requests per minute, but that doesn�t affect the overall workflow and is enough for general overview.


As soon as you register, you�ll receive a token which is a string of various symbols. Add this token to the following URL after the equality sign (=): **https://api.mapbox.com/v4/mapbox.terrain-rgb/{z}/{x}/{y}.pngraw?access_token=YOUR_ACCESS_TOKEN**, and use this URL in *Sandworm* to obtain the data for the corresponding level.


> **Notice:** To avoid jaggies (stair-step artifact), export the heightmap into a 32-bit texture.


**Imagery**


Here's an example of an imagery TMS server you can use for general overview:


- **http://a.tile.openstreetmap.org/{z}/{x}/{y}.png** � OSM topographic data with a legend


**Vector**


As a free source of vector data for a basic overview, you can check [https://www.openstreetmap.org](https://www.openstreetmap.org) and use [https://extract.bbbike.org/](https://extract.bbbike.org/) as an aggregator for it.


The mentioned links and sources are provided as a quick start for an overview. You can use them and the *Sandworm* documentation if you don�t have any georeferenced data at hand. Exporting data from third-party tools is a huge topic for research in itself, and would take much more time than getting along with our tool.

</details>


<details>
<summary>Which projection should I select to have the minimum surface distortion? | Click to close</summary>

**Which projection should I select to have the minimum surface distortion?**


Unfortunately an all-fitting universal projection doesn�t exist, because every projection is a flat representation of a curved area, and the farther a point is from the center (origin) of the projection, the higher the data corruption is. You can find more on [Wikipedia](https://en.wikipedia.org/wiki/Map_projection) or search for other explanations on projections. The output projection should be chosen based on source data at hand or the project requirements.


You can use [https://epsg.org/](https://epsg.org/search/map) to find the best-fitting projection with minimum inaccuracy for the selected area.


**How to use [https://epsg.org/](https://epsg.org/search/map):**


1. Go to *EPSG Dataset -> Map Search*: ![](epsg_menu.png) > **Notice:** If the website doesn't display any map, consider disabling adblock or using a VPN.
2. Set the area boundaries and click *Search*. You�ll receive a table � sort it by type (click on the *TYPE* heading) and select one of the data sources that is marked as ***Projected***. ![](epsg_projection.gif)


Again, for a start, you can use **EPSG:3857** � this is a projection widely used by such services as *Google, OpenStreetMap, Navitel*, etc.

</details>


<details>
<summary>A heightmap/imagery tile is not placed as required. How to locate it properly on the map? | Click to close</summary>

**A heightmap/imagery tile is not placed as required. How to locate it properly on the map?**


If your data is not georeferenced, it won�t be located on the map (check the editor console, there also shall be a message).

</details>


<details>
<summary>Are tiles loading or not? | Click to close</summary>

**Are tiles loading or not?**


The more detailed the tiles are, the more time is required to load them. The *Generating Preview* pop-up will give you a hint � it is displayed in the bottom right corner of *Sandworm* while the data is downloaded. In addition, in the Editor console there�ll be a message looking like *"ImportCacheTile 465.162000 ms"* when a tile is loaded.


We recommend attempting with low *Zoom Level* values first. This will give you an overall understanding about the data you add, then you can increase the *[Zoom Level](../../../editor2/sandworm/sources/index.md#zoom)* value and click *[Update Elevation Layer](../../../editor2/sandworm/sources/elevation_imagery/index.md#update_layer)*. The higher the *Zoom Level* value is, the more detailed is the data (and the more time it takes to download from a server). If the data is too heavy, you�ll see a notification.

</details>


<details>
<summary>Sometimes neighboring tiles are of different colors. Is there any workaround for that? | Click to close</summary>

**Sometimes neighboring tiles are of different colors. Is there any workaround for that?**


This can happen when you take data from TMS servers. Better data usually costs money.


You can try to change *[Zoom Level](../../../editor2/sandworm/sources/index.md#zoom)* for a certain area. One more solution is to make insets using other TMS sources: for example, you generate the whole area with *Zoom Level* = 10, and for the problem area � create another layer, use another source for it, and set *Zoom Level* = 14 (the given zoom values are just an example, try your own values).

</details>


<details>
<summary>The result of generation is wrong. / Only a part of the area has been generated. | Click to close</summary>

**The result of generation is wrong. / Only a part of the area has been generated.**


Check that the output projection is set correctly.


If the data is outside the selected output projection, it won�t be used for the terrain generation � only the part that is inside will be generated. The corresponding message will be also shown in the Editor console.


A quick check: regenerate the project with no *Export Area* � select *Export Area* and click the trash-bin icon to remove its boundaries. *Sandworm* will generate only the areas for which the data is available.


Preview generation is also helpful in defining if you have data for the area that is missing. If you canceled the preview generation, restart it by right-clicking on a layer and selecting *Generate Preview*.

</details>


<details>
<summary>Only a part of the generated terrain is visible in the viewport. | Click to close</summary>

**Only a part of the generated terrain is visible in the viewport.**


Change the camera visibility distance: in the Editor window, click the gear icon for the selected camera and increase the *Far* value. You can set the maximum, which is 900000.


Adjust the visibility distance for *ObjectLandscapeTerrain*. It is set in the Editor settings: *Windows -> Settings -> Landscape -> Visibility Distance*. You can set it to inf.


![Setting visibility distance for Landscape Terrain](visibility_distance.jpg)

</details>


<details>
<summary>When I click Run, I see the black screen after the world is loaded, although there are cameras in the scene. | Click to close</summary>

**When I click Run, I see the black screen after the world is loaded, although there are cameras in the scene.**


The scene contains a camera by default, which has the *[Main Player](../../../objects/players/index.md#main_player)* parameter enabled. This parameter defines the image from which camera is displayed when the world is run. Enable this parameter for the camera that you want to control at runtime, for example *Sandworm* camera � it is spawned right above the terrain, and disable all other cameras.

</details>


<details>
<summary>Is there a built-in day and night cycle system (with the starry sky) that depends on the current latitude and longitude? | Click to close</summary>

**Is there a built-in day and night cycle system (with the starry sky) that depends on the current latitude and longitude?**


We have the IG plugin for this task. This plugin is enabled by default in the IG Template, you can read more [here](../../../ig/weather/settings.md) and [here](../../../api/library/plugins/weather/class.skymap_cpp.md).

</details>


<details>
<summary>How to position an object using its geo coordinates? | Click to close</summary>

**How to position an object using its geo coordinates?**


For ***ObjectTerrainGlobal***, you can use *[Geodetic Pivot](../../../objects/geodetics/geodeticpivot/index.md)* in the Editor � every object added as its child can be positioned on the terrain using geographical coordinates set in latitude/longitude.


As for ***ObjectLandscapeTerrain***, the positioning tool is still in development, meanwhile you can transform coordinates using third-party sources, such as [https://products.aspose.app/gis/transformation](https://products.aspose.app/gis/transformation).


Here is a description of the workflow:


- Transform the object and the origin coordinates to the world coordinates (mind the input and output projections). ![Source coordinates of the object](object_coordinates.jpg) *Source coordinates of the object (screen capture from Google Maps)* ![Source coordinates of the origin](origin_coordinates.png) *Source coordinates of the origin (Export Area parameter in Sandworm)* ![Transforming coordinates using aspose.app](transform_coordinates_aspose.png) *Transforming coordinates using aspose.app*
- Take the origin position from the object position: **Object.X � Origin.X; Object.Y � Origin.Y**. ![Calculating the world coordinates](coordinates_calculation.png) *Calculating the world coordinates*
- Use the outcome as the X and Y coordinates of the object in the world. ![Object positioned in the world](positioned_object.jpg) *Object positioned in the world*


Developers can also use *[Geodetics Plugin](../../../code/plugins/geodetics/index_cpp.md)* and position objects via code.


IG has the *[worldToGeodetic()](../../../api/library/geodetics/geodetics_plugin/class.converter_cpp.md#worldToGeodetic_Vec3_dvec3)* method and *[Unigine::Plugins::Geodetics::Transformer](../../../api/library/geodetics/geodetics_plugin/class.transformer_cpp.md)* class to position objects.

</details>


<details>
<summary>Terrain is not generated. / Editor suddenly closes. | Click to close</summary>

**Terrain is not generated. / Editor suddenly closes.**


Generating a terrain is a very resource-consuming operation. For vast and detailed landscapes, you might need a lot of RAM available.


We recommend having 64 Gb RAM (at least 32 Gb).


Disabling the [Microprofile](../../../tools/profiling/microprofile/index_cpp.md) tool can also save up to 6 Gb RAM. This may be done either by running the Editor with the [external argument](../../../sdk/projects/index_cpp.md#customize_edit) `"-microprofile_enabled 0"`, or disabling it in the Editor [console](../../../code/console/index.md#microprofile_enabled).


If you have crashes while generating a terrain, gradual adding layers one by one and generating can help finding a problem with the data. Or at least remove the vector data layer, because it may be very consuming.

</details>
