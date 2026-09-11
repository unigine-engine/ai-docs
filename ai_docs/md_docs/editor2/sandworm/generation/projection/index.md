# Projection


In this section you select the projection to be used for the generated terrain and the required alignment of axes in the coordinate system. The set of options depends on the *[Terrain Type](../../../../editor2/sandworm/interface/index.md#terrain_type)*.


![](projection_lt.png)

*Projection settings for Landscape Terrain*


![](projection_tg.png)

*Projection settings for Terrain Global*


## Output Projection


The generated terrain is exported to *[Object Landscape Terrain](../../../../objects/objects/terrain/landscape_terrain/index.md)* or *[Object Terrain Global](../../../../objects/objects/terrain/terrain_global/index.md)*, which is actually a **flat** (i.e., not geospherical) area. Therefore, **only projected coordinate systems are available for selection and can be used as export projections**.


To choose a projection, click the corresponding button. The list of coordinate systems that can be used for projected output will open:


![](coordinate_system_list.png)


- The ***Projected Coordinate System*** list contains a wide range of coordinate reference systems for projected output.
- The ***Source Coordinate System*** list displays the coordinate systems used by your source data for convenience.


Select a projection by double click, or just select by clicking once and press the *OK* button.


> **Notice:** For the proper terrain generation, the coordinate system that encompasses all data sources should be selected. If the selected coordinate system does not include any part of the source data, the part of the terrain for such fragment will not be generated.


## Built-in Projections


Instead of a projected coordinate system defined by an EPSG code, the terrain can be generated in a built-in local tangent projection: the origin is taken from the *[Origin](../../../../editor2/sandworm/generation/export_area/index.md#origin)* of the *Export Area*, and the axes are East(x), North(y) in meters. Each *[terrain type](../../../../editor2/sandworm/interface/index.md#terrain_type)* has its own built-in projection.


- ***Cesium-Ready*** � available for *[Object Landscape Terrain](../../../../objects/objects/terrain/landscape_terrain/index.md)*. The transformation from geographic to flat coordinates is performed entirely by GDAL/PROJ (+proj=topocentric or +proj=ortho). Such a terrain carries no projection and no EPSG tag and stores its geodetic origin, so it can be used as a [terrain inset](../../../../code/plugins/cesium/insets.md): a high-detail area rendered on top of the global elevation and imagery streamed from *Cesium ion* by the *[Cesium](../../../../code/plugins/cesium/index_cpp.md)* plugin.
- ***Built-in (Unigine Projection)*** � available for *[Object Terrain Global](../../../../objects/objects/terrain/terrain_global/index.md)*. The projection based on the *WGS-84* ellipsoid.

  - ***Curved*** setting enables the horizon curvature (*WGS-84* ellipsoid datum). Curving of the terrain is performed using the *[Geodetic Pivot](../../../../objects/geodetics/geodeticpivot/index.md)*.


> **Notice:** While a built-in projection is enabled, the [output projection](#output_projection) cannot be chosen. For *Object Terrain Global*, the [*Coordinate System*](#coordinate_system) parameter is unavailable as well.


## Coordinate System


The result of data transformation using the selected projection sometimes may not coincide with the internal UNIGINE axis alignment (**East(x), North(y)**). In such a case, the generated terrain might differ from the preview (i.e., East and West switched). To fix this, set the *Coordinate System* to *Source*.


- ***Source*** � the orientation of the generated terrain is in accordance with the alignment indicated in the projection.
- ***Unigine World*** � the generated terrain is aligned as East(x), North(y).


## Vertical Datum


> **Notice:** The setting is available for *[Object Landscape Terrain](../../../../objects/objects/terrain/landscape_terrain/index.md)* only and while *[Cesium-Ready](#cesium_ready)* is enabled.


Elevation sources do not all measure height from the same reference surface: some give heights above the ellipsoid, others above a geoid model. *Vertical Datum* declares which one the source data uses, so that the geoid-to-ellipsoidal transform is applied on import. The generated heightmap always holds *WGS84* ellipsoidal heights.


- ***Ellipsoidal (WGS84)*** � the heights are already ellipsoidal, nothing is transformed.
- ***EGM96 (EPSG:5773)*** � the heights are given above the EGM96 geoid.
- ***EGM2008 (EPSG:3855)*** � the heights are given above the EGM2008 geoid.
- ***Custom EPSG*** � any other vertical coordinate system, specified by its code in the *Vertical EPSG* field that appears below.
