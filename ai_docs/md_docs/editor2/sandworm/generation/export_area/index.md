# Export Area


*Export Area* is an arbitrary area that defines which part of the terrain is going to be generated. This area is visualized as blue boundaries on the preview map.


![](export_area.jpg)


### Setting Export Area


To define *Export Area*, set the [boundaries](../../../../editor2/sandworm/interface/index.md#boundaries).


You can set points manually or enclose the area visible in the *Map* view and move the points, if necessary, using the following tools:


![](../../sources/boundaries_tools.png)


| ![Edit Boundaries Button](../../interface/edit_boundaries.png) | **Modifying boundaries**: click and drag the point on the preview map or change its coordinates on the *[Parameters](../../../../editor2/sandworm/interface/index.md#parameters_panel)* panel. **Adding points**: hold ALT and click the left mouse button in the *Map* window. **Deleting points and boundaries**: right-click on a single point in the *Map* window and click *Remove* in the context menu. You can also select a point in the *Map* window and press *Delete* on the keyboard. |
|---|---|
| ![Enclose Visible Area Button](../../interface/set_visible_area.png) | **Enclosing the area** visible in the *Map* window in the boundaries. The data will be uploaded for the area within these boundaries. You can move the points defining the boundaries to adjust the area as necessary. |
| ![Delete Boundaries Button](../../interface/trash_bin.png) | **Removing the boundaries** for the selected source. If the boundaries are not set (or deleted), all data available in the source and within *Export Area* will be uploaded. |


> **Notice:** If *Export Area* is not set, the terrain is generated based on all added data, i.e. the boundaries of this terrain would be equal to the boundaries of all added sources, and the origin is set to the center as relative to all added sources. You can modify the boundaries of each source individually in the same way as *Export Area*.


You can relocate *Export Area* — right-click somewhere on the map and select *Place Export Area Here* in the context menu. *Export Area* will be moved there, and the clicked point will become the center of the polygon inside the boundaries.


### Parameters


![](export_area_parameters.png)


| Area Size | Displays the size of the selected area in square kilometers. |
|---|---|
| Calculate Origin Automatically | If enabled, the origin is calculated automatically based on the data provided. If *Export Area* is changed and the terrain is regenerated, the origin would be updated automatically. |
| Origin | If [**Calculate Origin Automatically**](#calculate_origin) is disabled, the origin latitude and longitude can be edited here, and they will not be recalculated automatically if the Export Area is changed and the terrain is regenerated. |
| Block Export Area to Changes | If enabled, the selected *Export Area* cannot be modified. This option is useful, if you want to move around the map without occasionally shifting or modifying *Export Area*. |
