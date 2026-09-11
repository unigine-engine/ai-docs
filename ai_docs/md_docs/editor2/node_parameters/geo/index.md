# Geo Coordinates


> **Notice:** These parameters are available in UnigineEditor only when the project is configured to use the **[Geodetics](../../../code/plugins/geodetics/index_cpp.md)** plugin and this plugin is [loaded](../../../code/plugins/geodetics/index_cpp.md#launch) on the start-up.


When working with models of the real world in your application with a georeferenced terrain, it is natural to position nodes using their geo-coordinates (*latitude, longitude, altitude*) instead of *X*, *Y*, and *Z* coordinates.


Geo-coordinates can be specified for any node that meets **either** of the following requirements:


- It is positioned in the world with a *georeferenced terrain* generated using the *[Sandworm](../../../editor2/sandworm/index.md)* tool.
- It is added as a child to the *[GeodeticPivot](../../../objects/geodetics/geodeticpivot/index.md)* node.


## Geo Parameters


This section describes parameters allowing you to specify the geo-coordinates of a node via UnigineEditor, along with obtain the origin of the world in geodetic coordinates.


![](node_geo_coordinates.png)


| Database Origin | Origin of the world in geodetic coordinates (not editable). |
|---|---|
| Geo (Lat, Lon, Alt) | Latitude, longitude, and altitude coordinates of the node. |


The set of available parameters varies depending on the node/nodes selected in the world:


- If you select the **georeferenced terrain** node, only the *Database origin* parameter will be available. ![](geo_coords_0.png)
- If you select any **other node or multiple nodes**, the *Database origin* and *Geo* parameters will be available. > **Notice:** In this case, you can edit the values of the *Geo* parameter. ![](geo_coords_1.png)
- When selecting **both the georeferenced terrain and a node/multiple nodes**, the *Database origin* and *Geo* parameters will be available. > **Notice:** The *Geo* values aren't editable in this case. ![](geo_coords_2.png)


When the node is added as a child to the *[Geodetic Pivot](../../../objects/geodetics/geodeticpivot/index.md)* node, the **[Make Curved](../../../objects/geodetics/geodeticpivot/index.md#working)** button is available as well.
