# Unigine::Plugins::Geodetics::Transformer Class (CS)


This class provides low-level geodetic coordinate transformations between geodetic coordinates (**latitude, longitude, and altitude**) and 3D world-space positions and orientations. It relies on the **GDAL** library for coordinate system handling and supports two ways of defining the projection:


- By **EPSG code** � a numeric identifier from the EPSG geodetic registry (e.g. 32637 for UTM zone 37N).
- By **WKT2 string** � a full OpenGIS Well-Known Text description of the projected coordinate system.


Once a projection is set, the Transformer computes an internal **projection-space origin** by transforming the supplied geodetic world origin into projection coordinates. All subsequent world-to-geodetic and geodetic-to-world conversions apply this offset so that the 3D world origin maps to the specified real-world geodetic location.


The *[GeodeticToWorld()](../../../...md#geodeticToWorld_dvec3_bool_dmat4)* method returns a full **dmat4** transform matrix whose axes are aligned to the local **East-North-Up (ENU)** frame at the given location: the X axis points East, the Y axis points North, and the Z axis points Up. The orientation is computed by numerically differentiating the projection at the queried point, yielding accurate local frame axes even for non-conformal projections. When only the position is needed, *[GeodeticToWorldPosition()](../../../...md#geodeticToWorldPosition_dvec3_bool_dvec3)* provides a lighter alternative that skips the orientation computation.


For higher-level coordinate conversion that also handles *[GeodeticPivot](../../../../api/library/geodetics/class.geodeticpivot_cs.md)* nodes, automatic terrain detection, Euler angle conversions between world space and the local geodetic frame, and geocentric (ECEF) coordinate conversions, use the associated [Converter](../../../../api/library/geodetics/geodetics_plugin/class.converter_cs.md) class, accessible via *[GetConverter()](../../../...md#getConverter_Converter)*.


> **Notice:** Geodetics transformations are available **only** if the [Geodetics Plugin](../../../../code/plugins/geodetics/index_cs.md) is loaded.


## Transformer Class

### Properties

## 🔒︎ dvec3 OriginProjectionSpace

The world origin expressed in the projected coordinate system space (e.g. UTM meters). This value is computed once when a projection is set via **[SetProjectionEpsg](../../../...md#setProjectionEpsg_int_dvec3_cstr_bool_int)** or **[SetProjectionWkt](../../../...md#setProjectionWkt_cstr_dvec3_cstr_bool_int)** by transforming the supplied geodetic origin into projection space. It is used as the offset applied during all world-to-projection and projection-to-world conversions.
### Members

---

## Transformer Get ( )

Returns a pointer to the existing geodetics instance.
### Return value

Pointer to the existing geodetics transformer instance. If GeodeticsPlugin is not launched, null is returned.
## int SetProjectionWkt ( string projection_cs_wkt_string , dvec3 world_origin_geodetic_position , string geodetic_cs_string = WGS84 , bool geodetic_cs_is_well_known = true )

Sets a projection by WKT description, which is used as the world coordinate projection, and defines a geodetic coordinate system. Also computes and stores the projection-space origin by transforming the supplied geodetic origin coordinates. On failure, all internal projection state is cleared.
### Arguments

- *string* **projection_cs_wkt_string** - Description of the projection in the OpenGIS WKT format.
- *dvec3* **world_origin_geodetic_position** - World origin in geodetic coordinates (lat,lon,alt).
- *string* **geodetic_cs_string** - Description of a geodetic coordinate system.
- *bool* **geodetic_cs_is_well_known** - true or false. If set to **1**, a well-known coordinate system description is used as the **geodetic_cs_string** argument. The following well-known text values are supported: If set to false, a detailed WKT description is used.

  - WGS84 � same as *EPSG:4326*, but has no dependence on EPSG data files.
  - WGS72 � same as *EPSG:4322*, but has no dependence on EPSG data files.
  - NAD27 � same as *EPSG:4267*, but has no dependence on EPSG data files.
  - NAD83 � same as *EPSG:4269*, but has no dependence on EPSG data files.
  - EPSG:n � *n* is a GCS code from the horizontal coordinate system table.

### Return value

**1** on success; otherwise, **0**.
## int SetProjectionEpsg ( int projection_cs_epsg_code , dvec3 world_origin_geodetic_position , string geodetic_cs_string = WGS84 , bool geodetic_cs_is_well_known = true )

Sets a projection by EPSG code, which is used as the world coordinate projection, and defines a geodetic coordinate system. Also computes and stores the projection-space origin by transforming the supplied geodetic origin coordinates. Must be called from the main thread. On failure, all internal projection state is cleared.
### Arguments

- *int* **projection_cs_epsg_code** - EPSG code of the projection.
- *dvec3* **world_origin_geodetic_position** - World origin in geodetic coordinates (lat,lon,alt).
- *string* **geodetic_cs_string** - Description of a geodetic coordinate system.
- *bool* **geodetic_cs_is_well_known** - true or false. If set to **1**, a well-known coordinate system description is used as the **geodetic_cs_string** argument. The following well-known text values are supported: If set to false, a detailed WKT description is used.

  - WGS84 � same as *EPSG:4326*, but has no dependence on EPSG data files.
  - WGS72 � same as *EPSG:4322*, but has no dependence on EPSG data files.
  - NAD27 � same as *EPSG:4267*, but has no dependence on EPSG data files.
  - NAD83 � same as *EPSG:4269*, but has no dependence on EPSG data files.
  - EPSG:n � *n* is a GCS code from the horizontal coordinate system table.

### Return value

**1** on success; otherwise, **0**.
## dmat4 GeodeticToWorld ( dvec3 geodetic_position , bool rotate_to_en = false )

Transforms geodetic coordinates of the selected coordinate system to the 3D world coordinates: position and rotation (the Y axis is directed to the North, the X axis � to the East, and the Z axis � upwards). The orientation is computed by numerically differentiating the projection at the given location to derive accurate local North and East vectors. Returns an identity matrix if no projection has been set.
### Arguments

- *dvec3* **geodetic_position** - Geodetic coordinates (lat,lon,alt).
- *bool* **rotate_to_en** - true to rotate data as follows: East => X, North => Y (ENU and similar systems); false if the data source uses another alignment (for example NED).

### Return value

World position and orientation.
## dvec3 GeodeticToWorldPosition ( dvec3 geodetic_position , bool rotate_to_en = false )

Transforms geodetic coordinates of the selected coordinate system to the 3D world coordinates (position only, without orientation). More efficient than **geodeticToWorld()** when only the position is needed. Returns a zero vector if no projection has been set.
### Arguments

- *dvec3* **geodetic_position** - Geodetic coordinates (lat,lon,alt).
- *bool* **rotate_to_en** - true to rotate data as follows: East => X, North => Y (ENU and similar systems); false if the data source uses another alignment (for example NED).

### Return value

World position.
## dvec3 WorldToGeodetic ( dvec3 world_position , bool rotate_to_en = false )

Transforms the 3D world coordinates to geodetic coordinates of the selected coordinate system. The world position is first shifted by the projection-space origin offset, then transformed through the inverse (projection-to-geodetic) coordinate transformation. Returns a zero vector if no projection has been set.
### Arguments

- *dvec3* **world_position** - World position.
- *bool* **rotate_to_en** - true to rotate data as follows: East => X, North => Y (ENU and similar systems); false if the data source uses another alignment (for example NED).

### Return value

Geodetic coordinates (lat,lon,alt).
## Converter GetConverter ( )

Returns the **[Converter](../../../../api/library/geodetics/geodetics_plugin/class.converter_cs.md)** instance associated with this *Transformer*. The *Converter* provides higher-level geodetic-to-world transformations that also handle *[GeodeticPivot](../../../../api/library/geodetics/class.geodeticpivot_cs.md)* nodes, terrain detection, Euler angle conversions, and geocentric coordinate conversions.
### Return value

Associated **[Converter](../../../../api/library/geodetics/geodetics_plugin/class.converter_cs.md)** instance.
