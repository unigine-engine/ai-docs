# Editing Landscape Terrain


The built-in Brush Editor allows you to change the *[Landscape Terrain](../../objects/objects/terrain/landscape_terrain/index.md)* relief on the spot with the help of brushes. In the editing mode, you can draw various terrain features, such as rocky ground and other craggy details. All brushes modify only the selected *[Landscape Layer Map](../../objects/objects/terrain/landscape_terrain/landscape_layer_map.md)*.


To start editing a *Landscape Layer Map*, select *Landscape Paint Mode* on the [toolbar](../../editor2/interface/index.md#tools_panel).


You can also click the **Brush Edit** button in the *Landscape Asset* section of the *Node* tab in the *[Parameters](../../editor2/interface/index.md#parameters)* window.


![](brush_edit.png)


The *Active Tool* window will open:


![](brush_editor_window.png)


In the *Objects* section, there is a list of all *Landscape Layer Map* objects available in the world. To edit the required *Landscape Layer Map*, choose it either in the *Objects* section or in the *World Hierarchy* window.


After the *LandscapeLayerMap* texture asset is created, [editing tools](#tools) become available in the *Parameters* section of *Active Tool*.


If you are going to edit the compressed map, it needs to be decompressed first, which may take some time depending on the size of the map.

> **Warning:** When you repeatedly decompress/compress the data using Lossy algorithm, the quality will deteriorate every time the data is compressed.


To reset all changes made to a *Landscape Layer Map*, [Reimport](../../objects/objects/terrain/landscape_terrain/landscape_layer_map.md#import_parameters) all its data.


> **Notice:** Due to asynchronous nature of the *Landscape Terrain* system, insufficient streaming settings may result in undesired lagging of brushes while editing. Refer to the *[Landscape Terrain](../../objects/objects/terrain/landscape_terrain/settings.md#streaming)* article for more details on the streaming settings.


## Controls


- To draw with a brush, select it, click ***LMB*** and drag the mouse.
- To change the brush size, use ***mouse wheel***.
- To increase the brush size step, use ***Shift + mouse wheel***.
- To decrease the brush size step, use ***Ctrl + mouse wheel***.
- To adjust opacity (step: 0.1), use ***Alt + mouse wheel***.
- To adjust opacity (step: 0.01), use ***Alt + Ctrl + mouse wheel***.
- To switch to the brush tool, press ***B***.
- To switch to the Eraser tool, press ***E***.
- To invert the brush of the current tool, press and hold ***X***.
- To switch to the Smooth tool, press ***V***.
- To pick the height / color / mask intensity (depending on the brush type) at the current point of terrain and set it as a brush value, press ***C***.
- To select a Clutter in the Viewport, press ***Q***.


The information on controls is also available at the bottom of *Active Tool*.


## Select Masks


The list of masks contains all masks available for *Landscape Layer Map*. You can select one or several masks using the *Ctrl* or *Shift* buttons.


> **Notice:** To make editing more convenient, you can isolate the terrain component you are editing by enabling the [**Show Landscape Data**](../../editor2/using_visual_helpers/index.md#landscape_masks) visual helper and switching to the desired terrain component.


## Tools


The following tools are available for modifying the terrain:


| ![](apply.png) | Applies the settings defined for the selected Brush in the *Brush Settings* depending on the selected mask or masks. |
|---|---|
| ![](erase.png) | Erases albedo and height data. |
| ![](blur.png) | Blurs image, height, or mask data based on the *Brush Settings*. |


## Brushes


Brush Editor contains a set of available brushes with various forms that can be modified as necessary by adjusting their *[Brush Settings](#brush_settings)*. You can also add your own brushes by clicking the Plus icon.


![](brush_settings.png)


## Brush Settings


Depending on the selected tool, the following brush settings may be available:


| Size | Size of the brush. To change the value, the mouse wheel can also be scrolled. |
|---|---|
| Spacing | Distance between the brush marks in a stroke, in pixels. |
| Angle | Angle of the brush marks, in degrees. |
| Color Srgb | Convert the brush color to SRGB. |
| Color | Color of the brush. You can pick a screen color, if necessary. |
| Color Intensity | Intensity of the color applied to the terrain. The value in the range from 0 to 1. |
| Masks Override | Override detail masks: - **Enabled** � erase the rest (unselected) detail masks so the current mask becomes visible when drawing. - **Disabled** � don't modify the rest detail masks. |
| Height Blend Mode | Blending mode for the Height brush: - **Alpha Blend** � override the existing height with the current height. - **Additive** � add the current height to the existing value. |
| Height | Height value for the brush. |
| Opacity | Strength of the brush when applying the layer color. *Lower* values create a more translucent brush, and *higher* values create a more opaque brush. Multiple applications of the brush with low opacity to the same place create a more opaque image. |
| Contrast | Hardness of the brush. *Lower* values create a softer brush. |
| Intensity | Intensity for the eraser. |
| Smooth Intensity | Intensity of the blur. |
| Opacity | Image file containing the opacity map to be used for the brush. |
| Clutters Refresh Rate | Delay period for all *Mesh Clutter* updates following the mask changes, in seconds, if the brush is dragged continuously. The mask of *Landscape Terrain* being edited should be also assigned to the clutter as the [terrain mask](../../objects/objects/mesh_clutter/index.md#terrain_mask) to trace these changes. |
