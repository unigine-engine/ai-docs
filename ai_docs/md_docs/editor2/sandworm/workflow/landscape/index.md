# Creating Landscape


To generate a basic landscape we need elevation/height and imagery/color data.


### See Also


Check this video from the series of [video tutorials on the terrain generation](../../../../videotutorials/essentials/sandworm.md) using Sandworm:


## Adding a Georeferenced Image


We are going to add georeferenced images from the asset pack.


### Adding Elevation/Height


1. Click **+** for *Elevation/Height*. ![](add_elevation_layer.png) The interface for adding a new source becomes available on the *Parameters* panel.
2. Keep the source type as it is and click the folder icon: ![](open_file_location.png)
3. Select *Assets*, as you have already added the required files as assets to your project at its creation.
4. In the Asset Browser, select `UnigineGeoreferencedTerrainGeneration/elev/elevation25mpx.tif`.
5. Click the *Preview* button and the preview for the added asset will be displayed on the *Map* panel. This step is optional, you can create the layer without generating the preview. ![](preview_elevation.png)
6. Click the *Create Elevation Layer(s)* button and this source will be added to the *Terrain Layers* list.


### Adding Imagery / Color


Now let's add the Imagery sources. The process is mostly the same as for the Elevation source.


1. Click **+** for *Imagery / Color*. ![](add_imagery_layer.png) The interface for adding a new source becomes available on the *Parameters* panel.
2. Keep the source type as it is and click the folder icon: ![](open_file_location_img.png)
3. In the Asset Browser, open the `data/UnigineGeoreferencedTerrainGeneration/img/` folder, select all assets in it (Ctrl+A), and click *OK*. ![](select_img_sources.jpg)
4. Click the *Preview* button and the preview for the added assets will be displayed on the *Map* panel. This step is optional, you can create the layer without generating the preview.
5. Click the *Create Imagery Layer(s)* button and these sources will be added to the *Terrain Layers* list. ![](preview_imagery.jpg)


## Adding a TMS Source


Let's add an extra piece from a TMS source to try it out.


1. Click **+** for *Imagery / Color*.
2. Select *TMS* as the Source Type in the drop-down list.
3. Add a TMS URL to download the data from. To add a URL, click the ![](pencil.png) button: ![](open_url_list.png) The table to manage TMS URLs will open. It's empty by default, so let's add a URL: `https://server.arcgisonline.com/ArcGIS/rest/services/World_Topo_Map/MapServer/tile/{z}/{y}/{x}.png`, type an alias that will be displayed in the drop-down list, and click *Save Changes*. ![](url_list.png) For more details on adding TMS URLs see [here](../../../../editor2/sandworm/sources/index.md#url).
4. Set *Zoom Level* to 13. You can try higher levels, but they mean higher load. The preview generation process may take more time.
5. Set the [boundaries](../../../../editor2/sandworm/interface/index.md#boundaries) for the source, otherwise *Sandworm* doesn't know what data is required. The easiest way is to click the ![](../../interface/set_visible_area.png) button � the area displayed on the *Map* panel will be enclosed in boundaries. You can scroll out and move the points, add more points or delete them.
6. Click the *Preview* button and the preview for the added assets will be displayed on the *Map* panel. This step is optional, you can create the layer without generating the preview. ![](tms_preview.jpg)
7. Click the *Create Imagery Layer* button and this source will be added to the *Terrain Layers* list.


The last added layer is drawn on top in the *Map* panel. You can move it to the background using the context menu available on the right click on the corresponding terrain source or in the *Map* panel, when the [Editing mode](../../../../editor2/sandworm/interface/index.md#preview_panel) is selected.


![](move_to_background.png)


When generating a terrain, data with the higher density is selected from all available sources. Therefore, in our case the imagery of the terrain taken from *ArcGIS* will be taken only for the area where no data from assets is provided.


## Generated Terrain


The [generated](../../../../editor2/sandworm/workflow/generate/index.md) terrain will look as follows:


![](example.jpg)

*Generated Landscape Terrain*


Here we can see both parts: high-density imagery data with elevation data in the foreground, and lower-quality imagery data with no elevation data in the background.


## What Else


- Search for an elevation TMS source, because imagery added without elevation will look flat.
- [Remove](../../../../editor2/sandworm/interface/index.md#context_menu) or [disable](../../../../editor2/sandworm/interface/index.md#disable_layers) sources that you don't need.
- Check the article on the [elevation and imagery](../../../../editor2/sandworm/sources/elevation_imagery/index.md) for a more detailed description of parameters.
