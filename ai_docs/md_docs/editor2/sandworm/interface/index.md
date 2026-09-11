# Sandworm Interface Overview


This chapter gives an overview of the *Sandworm* tool interface.


### See Also


Check this video from the series of [video tutorials on the terrain generation](../../../videotutorials/essentials/sandworm.md) using Sandworm:


## Opening the Sandworm Tool and creating a project


To open *Sandworm*, select *Tools -> Sandworm* in the main menu.


![](open_sandworm.png)


The following window will open:


![](welcome_dialog_1.png)


If you have already worked with *Sandworm* and created projects, you'll also see a list of links to your recent projects for quick access:


![](welcome_dialog_2.png)


By clicking the *Create New* button, the **Project Configuration** window opens:


![](project_configuration.png)


| Name | *Sandworm* project name |
|---|---|
| Path | Path to store the project |
| Terrain Type | Terrain type to be used for terrain generation. UNIGINE has two built-in terrain objects. Both have a practical limit of up to 10,000 x 10,000 km: - *[Object Landscape Terrain](../../../objects/objects/terrain/landscape_terrain/index.md)* � a more efficient advanced type of terrain, useful for very detailed terrains, doesn't support geo-coordinates for now, supports collaborative editing, supports runtime modification, faster intersection testing, binoculars-friendly. - *[Object Terrain Global](../../../objects/objects/terrain/terrain_global/index.md)* � useful for large-scale multi-inset terrains, supports [curved](../../../objects/geodetics/geodeticpivot/index.md) mode, natively works with geo-coordinates, can be generated from raw GIS data. > **Notice:** The terrain type can't be changed after the project creation. If you want to create the terrain using the other terrain type, you can [create another project based on the current one](#create_based_on_current) and change the terrain type at creation. |
| Export Spatial Reference | Coordinate reference system to be used for export. This setting is available if *Landscape Terrain* is selected as *Terrain Type* and can be changed later in the generation settings, where it is called *[Output Projection](../../../editor2/sandworm/generation/projection/index.md#output_projection)*. Do not confuse it with the *[Coordinate System](../../../editor2/sandworm/generation/projection/index.md#coordinate_system)* setting, which controls axis alignment only. As you click the button, the following window will open: ![](coordinate_systems.png) If you don't know what projection to use, type 3857 in the search window and select the *EPSG:3857* projection � this projection is widely used by such services as Google, OpenStreetMap, Navitel, etc. This projection fits almost all georeferenced data except poles. For more details, see the [setting](../../../editor2/sandworm/generation/projection/index.md#output_projection) description and the relevant [FAQ](../../../editor2/sandworm/faq/index.md#projection) section. |


### Creating a project based on the current one


You can use a *Sandworm* project as a basis for another project: all data available in the existing project will be copied to the new one.


To do that, in the *Sandworm* window click *File -> Create Project Based on Current*.


![](create_based_on_current.png)


The following window will open:


![](create_based_on_current_config.png)


When creating a project using this option, you can change the Terrain Type. In this case, settings that are not suitable for the selected terrain type, won't be added to the new project.


## Sandworm Interface


The *Sandworm* tool interface has four panels: *Sources, Map, Parameters*, and *Generation Settings*. *Parameters* and *Generation Settings* share the same place on the right and are switched with the tabs above them. The *Sources* panel holds two lists: *Terrain Layers* at the top and *Objects* at the bottom.


![](panels.jpg)


### Sources


In the *Sources* panel, you specify the *Elevation* (height) and *Imagery* (albedo) sources for the terrain generation and the *Mask* data sources for details and vegetation generation in the *Terrain Layers* list, as well as the objects placed on the terrain using the source data in the *Objects* list.


To add a new data source or object, click the *+* sign for the corresponding source type:


![](create_layer.png)


An *Elevation*, *Imagery*, or *Mask* layer can hold several data sources. Selecting several sources at once lets you enable or disable them, or change their parameters, in a single action.


The checkbox on the left of the source allows disabling a source, thus excluding it from the generation process.


![Enabling and Disabling Sources](disable_layers.gif)


Right-clicking on an item opens the context menu:


![](sources_context_menu.png)


| Copy | Copies the selected source, mask, or object � one or several at a time. The items are duplicated with all their settings and can be reconfigured without affecting the source item. |
|---|---|
| Focus | Focuses the view in the *Map* panel on the selected source/object. |
| Move to Foreground | Moves the selected source/object (or several items of one type) to the foreground in the *Map* panel. |
| Move to Background | Moves the selected source/object (or several items of one type) to the background in the *Map* panel. |
| Generate Preview | Generates the preview of the selected source. It is designed to generate the preview that has previously been [canceled](#cancel_preview). Available for sources only, not for objects. |
| Remove | Removes the selected source/object (or several items of one type). You can also delete a selected source/object by using the Delete button. |
| Properties | Displays the properties of the selected source: its name, the coordinate reference system the source file uses, the data density in the units of that system (meters per pixel for a metric one, degrees per pixel for a geographic one), and the geographic bounds of the source file. Available for a single selected source only. |


> **Notice:** *Move to Foreground* and *Move to Background* change the drawing order in the *Map* panel only � see [Overlapping Sources](../../../editor2/sandworm/sources/index.md#precedence).


To rename a source/object, double-click its name. Renaming for objects is also available on the *Parameters* panel.


### Map


The *Map* panel visualizes the available information. Here you can navigate and preview the added inputs. The following controls are available:


![](preview_controls.png)


| ![](panning.png) | Panning mode. Allows only panning in the *Map* panel without selecting any source. Panning is also possible when holding the *SPACE* button or the mouse wheel button and dragging the preview. |
|---|---|
| ![](select.png) | Editing mode. Allows editing the source boundaries: add, move, or delete the selected boundary points. Context menu for the layer becomes available in the *Map* panel. |
| ![](zoom_in.png) | Zoom-in button. The map can also be zoomed in by scrolling the mouse wheel up. |
| ![](zoom_out.png) | Zoom-out button. The map can also be zoomed out by scrolling the mouse wheel down. |
| Coordinates | Current coordinates of the mouse cursor. |
| ![](wgs84.png) | Display coordinates as *WGS 84* latitude and longitude. If coordinates are already displayed as latitude and longitude (not in meters), this button is inactive. |
| Coordinate System | The coordinate system selected for the *Map* panel. It can be changed by clicking this button. |


The source data might be heavy, and it can take time to generate a preview. In this case, you can cancel the preview generation using the following button available in the bottom right corner of the *Map* panel during the generation process:


![](layer_loading.gif)


If you later require this preview to be generated, use the *Generate Preview* option in the [context menu](#context_menu) of the *Sources* panel.


### Parameters


The *Parameters* panel contains parameters of the selected source or object.


#### Boundaries


For the imported sources (elevation, imagery, masks, and vectors), you can set the area to be used for the terrain generation by adjusting the boundaries:


![](boundaries.png)


| ![](edit_boundaries.png) | **Modifying boundaries**: click and drag the point on the *Map* panel or change its coordinates on the *[Parameters](../../../editor2/sandworm/interface/index.md#parameters_panel)* panel. **Adding points**: hold ALT and click the left mouse button in the *Map* panel. **Deleting points and boundaries**: right-click on a single point in the *Map* panel and click *Remove* in the context menu. You can also select a point in the *Map* panel and press *Delete* on the keyboard. |
|---|---|
| ![](set_visible_area.png) | **Enclosing the area** visible in the *Map* panel in the boundaries. The data will be uploaded for the area within these boundaries. You can move the points defining the boundaries to adjust the area as necessary. |
| ![](trash_bin.png) | **Removing the boundaries** for the selected source. If the boundaries are not set (or deleted), all data available in the source and within the *[Export Area](../../../editor2/sandworm/generation/export_area/index.md)* will be uploaded. |


By using this toolset, you can define which data should be taken from every source without uploading any unnecessary or corrupted data.


### Generation Settings


The *Generation Settings* panel contains the settings that define the details of the [terrain generation](../../../editor2/sandworm/generation/index.md) process: the format of terrain, its size and form, type of projection, paths for storage and output, and the distributed generation settings.


If any parameters required for the generation have not been set, their names are listed in red at the bottom of the panel. Click a name to scroll to the corresponding generation setting.
