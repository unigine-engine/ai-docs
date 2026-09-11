# Unigine::Plugins::Geodetics::Converter Class (CS)


This class is used to transform geodetic coordinates (**latitude, longitude and altitude**) to the 3D world position and vice versa. It supports multiple geodetic modes: a **GeodeticPivot**-based mode for pivot-anchored scenes, and plugin-based modes using **EPSG** codes or **WKT2** projection strings via the GDAL library. The converter also handles terrain-aware transformations (flat or curved terrain), Euler angle conversions between local geodetic and world space, and coordinate system conversions between geodetic and geocentric (ECEF) representations.

> **Notice:** Geodetics transformations are available **only** if the [Geodetics Plugin](../../../../code/plugins/geodetics/index_cs.md) is loaded.


## Converter Class

### Enums

## GEODETIC_MODE

Geodetic mode that determines how world-to-geodetic and geodetic-to-world transformations are performed.
| Name | Description |
|---|---|
| **NOT_AVAILABLE** = 0 | Geodetic coordinate transformations are not available. No valid projection or *[GeodeticPivot](../../../../api/library/geodetics/class.geodeticpivot_cs.md)* was found during initialization. |
| **GEODETIC_PIVOT** = 1 | Transformations are performed using a *[GeodeticPivot](../../../../api/library/geodetics/class.geodeticpivot_cs.md)* node found in the world. Supports both flat and curved terrain modes. |
| **PROJECTED** = 2 | Transformations are performed through the projected coordinate system of the world, defined by an EPSG code or a WKT2 string (see the **[ProjectionMode](../../../...md#getProjectionMode_int)**). |
| **ANCHOR** = 3 | Transformations are performed through the *[Anchor](../../../../api/library/geodetics/geodetics_plugin/class.anchor_cs.md)* binding the world space to the geocentric (ECEF) coordinate system; the world can be re-anchored at any geodetic position. |

## TERRAIN_MODE

Type of terrain object present in the world, used to determine how terrain-related parameters are resolved during initialization.
| Name | Description |
|---|---|
| **NO_TERRAIN** = 0 | No terrain object was found in the world. |
| **LANDSCAPE_TERRAIN** = 1 | An **[ObjectLandscapeTerrain](../../../../objects/objects/terrain/landscape_terrain/index.md)** (landscape terrain) is present in the world and is used as the terrain reference. |
| **TERRAIN_GLOBAL** = 2 | An **[ObjectTerrainGlobal](../../../../objects/objects/terrain/terrain_global/index.md)** (global terrain) is present in the world and is used as the terrain reference. |

## PROJECTION_MODE

Projection mode that determines how the projected coordinate system of the world is specified.
| Name | Description |
|---|---|
| **NONE** = 0 | No projected coordinate system is set (default). |
| **EPSG** = 1 | The projected coordinate system of the world is defined by an EPSG code (see the **[EPSGProjection](../../../...md#getEPSGProjection_int)** property). |
| **WKT2** = 2 | The projected coordinate system of the world is defined by a WKT2 string (see the **[WKT2Projection](../../../...md#getWKT2Projection_String)** property). |

### Properties

## bool AutoWorldInit

The flag indicating whether the converter automatically calls **[Initialize()](../../../...md#initialize_int)** when the world is loaded and **[Clear()](../../../...md#clear_void)** when the world is shut down. When enabled, the converter subscribes to world *init/shutdown* events and manages its own lifecycle automatically.
## 🔒︎ bool IsInitialized

The flag indicating whether the converter has been successfully initialized with a valid geodetic mode.
## 🔒︎ bool IsTerrainCurved

The flag indicating whether the terrain is treated as curved (spherical/ellipsoidal) rather than flat. Applies only in **[GEODETIC_MODE.GEODETIC_PIVOT](../../../...md#GEODETIC_MODE_GEODETIC_PIVOT)** mode.
## 🔒︎ dvec3 Origin

The world origin in geodetic coordinates (latitude, longitude, altitude). In *[GeodeticPivot](../../../../api/library/geodetics/class.geodeticpivot_cs.md)* mode this is the pivot's origin; in plugin modes it is the origin read from the terrain node's *sandworm_origin* variable.
## 🔒︎ Converter.TERRAIN_MODE TerrainMode

The terrain mode, indicating which type of terrain object (if any) was detected during initialization. See **[TERRAIN_MODE](../../../...md#TERRAIN_MODE_NO_TERRAIN)** for possible values.
## 🔒︎ ObjectLandscapeTerrain LandscapeTerrain

The active **[ObjectLandscapeTerrain](../../../../objects/objects/terrain/landscape_terrain/index.md)** instance found in the world during initialization, or null if no landscape terrain is present.
## 🔒︎ ObjectTerrainGlobal TerrainGlobal

The **[ObjectTerrainGlobal](../../../../objects/objects/terrain/terrain_global/index.md)** instance found in the world during initialization, or null if no global terrain is present.
## 🔒︎ Converter.GEODETIC_MODE GeodeticMode

The geodetic mode selected during initialization. See **[TERRAIN_MODE](../../../...md#TERRAIN_MODE_NO_TERRAIN)** for possible values.
## 🔒︎ int EPSGProjection

The EPSG code of the current projection, as read from the terrain node's *sandworm_epsg* variable. Returns **-1** if no EPSG projection is set.
## 🔒︎ string WKT2Projection

The WKT2 projection string of the current projection, as read from the terrain node's *sandworm_projection* variable. Returns an empty string if no WKT2 projection is set.
## bool ForceRotateCoordinatesToENU

The flag controlling whether coordinates are forcibly rotated to East-North-Up (ENU) axis alignment during geodetic transformations in plugin modes. When enabled, X maps to East and Y maps to North. This flag is automatically set from the terrain node's *coordinate_system* variable during initialization.
## 🔒︎ GeodeticPivot GeodeticPivot

The *[GeodeticPivot](../../../../api/library/geodetics/class.geodeticpivot_cs.md)* node found in the world during initialization, or null if no *[GeodeticPivot](../../../../api/library/geodetics/class.geodeticpivot_cs.md)* is present.
> **Notice:** Only relevant in **[GEODETIC_MODE.GEODETIC_PIVOT](../../../...md#GEODETIC_MODE_GEODETIC_PIVOT)** mode.

## GeodeticPivot.UP_AXIS GeodeticPivotMode

The up-axis mode used when computing the zero basis via the *[GeodeticPivot](../../../../api/library/geodetics/class.geodeticpivot_cs.md)*. Controls whether the up direction is the **geodetic normal** (ellipsoid surface normal) or the **geocentric normal** (direction toward the Earth's center).
> **Notice:** Only relevant in **[GEODETIC_MODE.GEODETIC_PIVOT](../../../...md#GEODETIC_MODE_GEODETIC_PIVOT)** mode.

## 🔒︎ Converter.PROJECTION_MODE ProjectionMode

The projection mode defining how the projected coordinate system of the world is specified, one of the *PROJECTION_MODE_** values.
## 🔒︎ Event EventInitialized

The event triggered when the converter finishes initialization (see **[Initialize()](../../../...md#initialize_int)**). The event also fires when initialization completes without a usable geodetic data source, so check **[IsInitialized](../../../...md#isInitialized_int)** in the callback.
### Members

---

## bool Initialize ( )

Scans the current world for a *[GeodeticPivot](../../../../api/library/geodetics/class.geodeticpivot_cs.md)* node and terrain objects (**[ObjectTerrainGlobal](../../../../objects/objects/terrain/terrain_global/index.md)** or **[ObjectLandscapeTerrain](../../../../objects/objects/terrain/landscape_terrain/index.md)**) to determine the appropriate geodetic mode. If a *[GeodeticPivot](../../../../api/library/geodetics/class.geodeticpivot_cs.md)* is found it is used directly; otherwise the terrain's *sandworm_epsg* or *sandworm_projection* variables are used to set up the GDAL-based projection. Must be called after the world has been loaded if **[AutoWorldInit](../../../...md#isAutoWorldInit_int)** is disabled.
### Return value

true if a valid geodetic mode was established; false if no usable geodetic configuration was found.
## void Clear ( )

Resets all converter state to defaults: sets the geodetic mode to **[GEODETIC_MODE.NOT_AVAILABLE](../../../...md#GEODETIC_MODE_NOT_AVAILABLE)**, clears the projection, origin, terrain references, and the *[GeodeticPivot](../../../../api/library/geodetics/class.geodeticpivot_cs.md)* pointer. After calling this method, **[IsInitialized](../../../...md#isInitialized_int)** returns false.
## dvec3 WorldToGeodetic ( vec3 world_position )

Transforms a 3D world position to geodetic coordinates (latitude, longitude, altitude). In **[GEODETIC_MODE.GEODETIC_PIVOT](../../../...md#GEODETIC_MODE_GEODETIC_PIVOT)** mode, uses flat or curved pivot mapping depending on **[IsTerrainCurved](../../../...md#isTerrainCurved_int)**. In plugin modes, delegates to the Geodetics plugin *[transformer](../../../../api/library/geodetics/geodetics_plugin/class.transformer_cs.md)*.
### Arguments

- *vec3* **world_position** - Position in 3D world space.

### Return value

Geodetic coordinates as (latitude, longitude, altitude). If the converter is not initialized, the input position is returned cast to a **dvec3**.
## vec3 GeodeticToWorld ( dvec3 geodetic_position )

Transforms geodetic coordinates (latitude, longitude, altitude) to a 3D world position. In **[GEODETIC_MODE.GEODETIC_PIVOT](../../../...md#GEODETIC_MODE_GEODETIC_PIVOT)** mode, uses flat or curved pivot mapping depending on **[IsTerrainCurved](../../../...md#isTerrainCurved_int)**. In plugin modes, delegates to the Geodetics plugin *[transformer](../../../../api/library/geodetics/geodetics_plugin/class.transformer_cs.md)* and extracts the translation component of the resulting transform matrix.
### Arguments

- *dvec3* **geodetic_position** - Geodetic coordinates as (latitude, longitude, altitude).

### Return value

Position in 3D world space. If the converter is not initialized, the input coordinate is returned cast to a **Vec3**.
## quat EulerToRotation ( vec3 euler )

Converts Euler angles in world space (pitch, roll, heading in degrees, ZYX order) to a quaternion rotation in world space. This is a coordinate-system-independent conversion and does not account for the local geodetic orientation at any particular location.
### Arguments

- *vec3* **euler** - Euler angles in degrees as (pitch, roll, heading), applied in ZYX order.

### Return value

Quaternion representing the rotation in world space.
## vec3 RotationToEuler ( quat rotation )

Converts a quaternion rotation in world space to Euler angles (pitch, roll, heading in degrees, ZYX order). This is a coordinate-system-independent conversion and does not account for the local geodetic orientation at any particular location.
### Arguments

- *quat* **rotation** - Quaternion representing the rotation in world space.

### Return value

Euler angles in degrees as (pitch, roll, heading) decomposed in ZYX order.
## quat GeodeticEulerToRotation ( dvec3 geodetic_position , vec3 euler )

Converts Euler angles defined in the local geodetic (ENU-aligned) frame at the given geodetic position to a quaternion rotation in world space. The local frame orientation is determined by *[GetZeroRotation()](../../../...md#getZeroRotation_dvec3_quat)* at that location. This is useful for placing objects whose heading, pitch, and roll are defined relative to the local horizon.
### Arguments

- *dvec3* **geodetic_position** - Geodetic coordinates (latitude, longitude, altitude) that define the local reference frame.
- *vec3* **euler** - Euler angles in degrees as (pitch, roll, heading) in the local geodetic frame, applied in ZYX order.

### Return value

Quaternion representing the rotation in world space.
## vec3 RotationToGeodeticEuler ( dvec3 geodetic_position , quat rotation )

Converts a quaternion rotation in world space to Euler angles defined in the local geodetic (ENU-aligned) frame at the given geodetic position. This is the inverse of *[GeodeticEulerToRotation()](../../../...md#geodeticEulerToRotation_dvec3_vec3_quat)*.
### Arguments

- *dvec3* **geodetic_position** - Geodetic coordinates (latitude, longitude, altitude) that define the local reference frame.
- *quat* **rotation** - Quaternion representing the rotation in world space.

### Return value

Euler angles in degrees as (pitch, roll, heading) in the local geodetic frame, decomposed in ZYX order.
## quat GetZeroRotation ( dvec3 geodetic_position )

Returns the quaternion rotation of the local geodetic reference frame at the given geodetic position. This is the rotation component extracted from *[GetZeroBasis()](../../../...md#getZeroBasis_dvec3_Mat4)*. An object with this rotation will have its forward axis pointing North and its up axis pointing away from the Earth's surface.
### Arguments

- *dvec3* **geodetic_position** - Geodetic coordinates (latitude, longitude, altitude) at which to compute the local frame orientation.

### Return value

Quaternion representing the local geodetic frame orientation in world space (zero heading, zero pitch, zero roll at that location).
## mat4 GetZeroBasis ( dvec3 geodetic_position )

Returns the full transform matrix of the local geodetic reference frame at the given geodetic position. The matrix encodes both the world-space position and the local orientation: X axis points East, Y axis points North, Z axis points Up (away from the Earth's surface). In flat-terrain *[GeodeticPivot](../../../../api/library/geodetics/class.geodeticpivot_cs.md)* mode, the Z component of the forward axis is zeroed to keep it horizontal.
### Arguments

- *dvec3* **geodetic_position** - Geodetic coordinates (latitude, longitude, altitude) at which to compute the local frame basis.

### Return value

Transform matrix with position set to the world-space location and axes aligned to the local geodetic frame (East, North, Up).
## vec3 GetZeroUpDirection ( dvec3 geodetic_position )

Returns the up direction of the local geodetic reference frame at the given geodetic position in world space. This is the Z axis of the matrix returned by *[GetZeroBasis()](../../../...md#getZeroBasis_dvec3_Mat4)*, i.e. the direction pointing away from the Earth's surface at that location.
### Arguments

- *dvec3* **geodetic_position** - Geodetic coordinates (latitude, longitude, altitude) at which to compute the local up direction.

### Return value

Normalized vector pointing away from the Earth's surface at the given geodetic location, expressed in world space.
## vec3 WorldToProjection ( vec3 world_position )

Converts a world-space position to a projection-space position by adding the projection origin offset. This offset is the position of the world origin expressed in the projected coordinate system (e.g. UTM meters). Not applicable in **[GEODETIC_MODE.GEODETIC_PIVOT](../../../...md#GEODETIC_MODE_GEODETIC_PIVOT)** or **[GEODETIC_MODE.NOT_AVAILABLE](../../../...md#GEODETIC_MODE_NOT_AVAILABLE)** modes � the input is returned unchanged in those cases.
### Arguments

- *vec3* **world_position** - Position in 3D world space.

### Return value

Position in the projected coordinate system space (e.g. UTM meters). Equal to the input in GeodeticPivot or unavailable modes.
## vec3 ProjectionToWorld ( vec3 projection_position )

Converts a projection-space position to a world-space position by subtracting the projection origin offset. This is the inverse of **worldToProjection()**. Not applicable in **[GEODETIC_MODE.GEODETIC_PIVOT](../../../...md#GEODETIC_MODE_GEODETIC_PIVOT)** or **[GEODETIC_MODE.NOT_AVAILABLE](../../../...md#GEODETIC_MODE_NOT_AVAILABLE)** modes � the input is returned unchanged in those cases.
### Arguments

- *vec3* **projection_position** - Position in the projected coordinate system space (e.g. UTM meters).

### Return value

Position in 3D world space. Equal to the input in GeodeticPivot or unavailable modes.
## dvec3 GeodeticToGeocentric ( dvec3 geodetic_position , double major_axis = 6378137.0 , double minor_axis = 6356752.314245 )

Converts geodetic coordinates (latitude, longitude, altitude) to geocentric (ECEF � Earth-Centered, Earth-Fixed) Cartesian coordinates using the closed-form ellipsoid equations. The default axis values correspond to the WGS84 ellipsoid.
### Arguments

- *dvec3* **geodetic_position** - Geodetic coordinates as (latitude in degrees, longitude in degrees, altitude in meters).
- *double* **major_axis** - Semi-major axis of the reference ellipsoid in meters. Defaults to the WGS84 value of 6378137.0 m.
- *double* **minor_axis** - Semi-minor axis of the reference ellipsoid in meters. Defaults to the WGS84 value of 6356752.314245 m.

### Return value

ECEF Cartesian coordinates in meters as (X, Y, Z).
## dvec3 GeocentricToGeodetic ( dvec3 geocentric_position , double major_axis = 6378137.0 , double minor_axis = 6356752.314245 )

Converts geocentric (ECEF � Earth-Centered, Earth-Fixed) Cartesian coordinates to geodetic coordinates (latitude, longitude, altitude) using the closed-form solution for the reference ellipsoid. The default axis values correspond to the WGS84 ellipsoid.
### Arguments

- *dvec3* **geocentric_position** - ECEF Cartesian coordinates in meters as (X, Y, Z).
- *double* **major_axis** - Semi-major axis of the reference ellipsoid in meters. Defaults to the WGS84 value of 6378137.0 m.
- *double* **minor_axis** - Semi-minor axis of the reference ellipsoid in meters. Defaults to the WGS84 value of 6356752.314245 m.

### Return value

Geodetic coordinates as (latitude in degrees, longitude in degrees, altitude in meters).
## vec3 GeocentricEulerToGeodeticEuler ( dvec3 geodetic_position , vec3 geocentric_euler )

Converts an orientation expressed as geocentric Euler angles (Psi/Theta/Phi � yaw/pitch/roll in the ECEF body frame) to geodetic Euler angles (heading, pitch, roll relative to the local North-East-Down frame) at the given geodetic position. Useful for converting orientations received from systems that operate in the ECEF frame (e.g. DIS/HLA simulations) into locally intuitive heading/pitch/roll values.
### Arguments

- *dvec3* **geodetic_position** - Geodetic coordinates (latitude, longitude, altitude) that define the local NED reference frame used for the conversion.
- *vec3* **geocentric_euler** - Orientation in the geocentric (ECEF) body frame as (Psi, Theta, Phi) in radians � yaw about Z, then pitch about Y, then roll about X.

### Return value

Euler angles in the local geodetic (NED) frame as (pitch, roll, heading) in radians.
## vec3 GeodeticEulerToGeocentricEuler ( dvec3 geodetic_position , vec3 geodetic_euler )

Converts an orientation expressed as geodetic Euler angles (heading, pitch, roll relative to the local North-East-Down frame) to geocentric Euler angles (Psi/Theta/Phi in the ECEF body frame) at the given geodetic position. This is the inverse of **geocentricEulerToGeodeticEuler()** and is useful for converting locally defined orientations into the ECEF body frame for interoperability with simulation standards such as DIS/HLA.
### Arguments

- *dvec3* **geodetic_position** - Geodetic coordinates (latitude, longitude, altitude) that define the local NED reference frame used for the conversion.
- *vec3* **geodetic_euler** - Euler angles in the local geodetic (NED) frame as (pitch, roll, heading) in degrees � heading about the local Down axis, pitch about the local East axis, roll about the local North axis.

### Return value

Orientation in the geocentric (ECEF) body frame as (Psi, Theta, Phi) in radians � yaw about Z, then pitch about Y, then roll about X.
## Anchor GetAnchor ( )

Returns the anchor binding the engine's world space to the geocentric (ECEF) coordinate system (see the *[Anchor](../../../../api/library/geodetics/geodetics_plugin/class.anchor_cs.md)* class).
### Return value

Anchor of the converter.
