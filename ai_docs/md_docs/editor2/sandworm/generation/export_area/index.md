# Export Area


*Export Area* is an arbitrary area that defines which part of the terrain is going to be generated. This area is visualized as blue boundaries on the *Map* panel.


![](export_area.jpg)


## Setting Export Area


To define *Export Area*, set the [boundaries](../../../../editor2/sandworm/interface/index.md#boundaries).


You can set points manually or enclose the area visible in the *Map* panel and move the points, if necessary, using the same [boundary tools](../../../../editor2/sandworm/interface/index.md#boundaries) as for the sources. Removing *Export Area* works differently:


![](../../sources/boundaries_tools.png)


| ![Delete Boundaries Button](../../interface/trash_bin.png) | **Removing *Export Area***: deletes all points defining it. With no *Export Area* set, the terrain is generated from all added data, i.e. the boundaries of this terrain would be equal to the boundaries of all added sources, and the origin is placed at the center of the combined extent of all added sources. You can modify the boundaries of each source individually in the same way as *Export Area*. |
|---|---|


You can relocate *Export Area* � right-click somewhere on the map and select *Place Export Area Here* in the context menu. *Export Area* will be moved there, and the clicked point will become the center of the polygon inside the boundaries.


## Parameters


![](export_area_parameters.png)


| Area Size | Displays the size of the selected area in square kilometers. |
|---|---|
| Calculate Origin Automatically | If enabled, the origin is calculated automatically based on the data provided. If *Export Area* is changed and the terrain is regenerated, the origin would be updated automatically. |
| Origin | If [**Calculate Origin Automatically**](#calculate_origin) is disabled, the origin latitude and longitude can be edited here, and they will not be recalculated automatically if the Export Area is changed and the terrain is regenerated. |
| Block Export Area to Changes | If enabled, the selected *Export Area* cannot be modified. This option is useful, if you want to move around the map without occasionally shifting or modifying *Export Area*. |
