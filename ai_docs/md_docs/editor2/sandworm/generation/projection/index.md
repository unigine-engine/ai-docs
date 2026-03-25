# Projection


In this section you select the projection to be used for the generated terrain and the required alignment of axes in the coordinate system.


![](projection_lt.png)


## Output Projection


The generated terrain is exported to *[Object Landscape Terrain](../../../../objects/objects/terrain/landscape_terrain/index.md)* or *[Object Terrain Global](../../../../objects/objects/terrain/terrain_global/index.md)*, which is actually a **flat** (i.e., not geospherical) area. Therefore, **only projected coordinate systems are available for selection and can be used as export projections**.


To choose a projection, click the corresponding button. The list of coordinate systems that can be used for projected output will open:


![](coordinate_system_list.png)


- The ***Projected Coordinate System*** list contains a wide range of coordinate reference systems for projected output.
- The ***Source Coordinate System*** list displays the coordinate systems used by your source data for convenience.


Select a projection by double click, or just select by clicking once and press the *OK* button.


> **Notice:** For the proper terrain generation, the coordinate system that encompasses all data sources should be selected. If the selected coordinate system does not include any part of the source data, the part of the terrain for such fragment will not be generated.


## Coordinate System


The result of data transformation using the selected projection sometimes may not coincide with the internal UNIGINE axis alignment (**East(x), North(y)**). In such a case, the generated terrain might differ from the preview (i.e., East and West switched). To fix this, set the *Coordinate System* to *Source*.


- ***Source*** — the orientation of the generated terrain is in accordance with the alignment indicated in the projection.
- ***World*** — the generated terrain is aligned as East(x), North(y).


## Built-In (Unigine Projection)


![](projection_tg.png)


**Built-In (Unigine Projection)** is an additional option available for the *[Object Terrain Global](../../../../objects/objects/terrain/terrain_global/index.md)* *[terrain type](../../../../editor2/sandworm/interface/index.md#terrain_type)* only. The terrain is generated using the projection based on *WGS-84* ellipsoid and can be [curved](../../../../editor2/sandworm/generation/curvature/index.md).
