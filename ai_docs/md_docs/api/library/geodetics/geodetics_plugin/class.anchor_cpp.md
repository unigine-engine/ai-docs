# Unigine::Plugins::Geodetics::Anchor Class (CPP)

**Header:** #include <plugins/Unigine/Geodetics/UnigineGeodetics.h>


The Anchor binds the engine's world space to the geocentric (ECEF) coordinate system. It stores the pair of transformations between world and geocentric coordinates and lets you re-anchor the world at any geodetic position. Re-anchoring keeps world coordinates small near the current area of interest, preserving floating-point precision in large georeferenced scenes.


To re-anchor the world, set the anchor position via the **[getGeoPosition()](../../../...md#getGeoPosition_dvec3)** property: the plugin builds an East-North-Up tangent frame on the WGS84 ellipsoid at the specified geodetic position, and this frame becomes the new world frame. The transformations that were in effect before the last re-anchoring remain available via the **[getOldGeocentricToWorld()](../../../...md#getOldGeocentricToWorld_dmat4)** and **[getOldWorldToGeocentric()](../../../...md#getOldWorldToGeocentric_dmat4)** properties, so the data you keep in world coordinates can be converted to the new frame. Calling **[reset()](../../../...md#reset_void)** drops the anchor, making world space coincide with the geocentric coordinate system.


The anchor is a part of the *[Geodetics](../../../../code/plugins/geodetics/index_cpp.md)* plugin and is obtained via the *[Converter](../../../../api/library/geodetics/geodetics_plugin/class.converter_cpp.md)* class.


## Anchor Class

### Enums

## ANCHOR_MODE

Anchoring mode defining how the current world frame was established.
| Name | Description |
|---|---|
| **ANCHOR_MODE_GEOPOSITION** = 0 | The world is anchored at a geodetic position set via the **[getGeoPosition()](../../../...md#getGeoPosition_dvec3)** property. |
| **ANCHOR_MODE_GEOCENTRIC** = 1 | Default mode: no anchor position is set, world space coincides with the geocentric (ECEF) coordinate system. |

### Members

## Anchor::ANCHOR_MODE getMode () const

Returns the current anchoring mode defining how the current world frame was established. *[ANCHOR_MODE_GEOPOSITION](#ANCHOR_MODE_GEOPOSITION)* means the world is anchored at a geodetic position, *[ANCHOR_MODE_GEOCENTRIC](#ANCHOR_MODE_GEOCENTRIC)* means no anchor position is set and world space coincides with the geocentric coordinate system.
### Return value

Current anchoring mode
## void setGeoPosition ( const Math:: dvec3 & position )

Sets a new geodetic position (latitude and longitude in degrees, altitude in meters) the world is anchored at. Setting this property re-anchors the world: an East-North-Up tangent frame is built on the WGS84 ellipsoid at the specified position and becomes the new world frame, while the previous transformations remain available via the **[getOldGeocentricToWorld()](../../../...md#getOldGeocentricToWorld_dmat4)** and **[getOldWorldToGeocentric()](../../../...md#getOldWorldToGeocentric_dmat4)** properties.
### Arguments

- *const  Math::[dvec3](../../../../api/library/math/class.dvec3_cpp.md)&* **position** - The geodetic position the world is anchored at

## Math:: dvec3 getGeoPosition () const

Returns the current geodetic position (latitude and longitude in degrees, altitude in meters) the world is anchored at. Setting this property re-anchors the world: an East-North-Up tangent frame is built on the WGS84 ellipsoid at the specified position and becomes the new world frame, while the previous transformations remain available via the **[getOldGeocentricToWorld()](../../../...md#getOldGeocentricToWorld_dmat4)** and **[getOldWorldToGeocentric()](../../../...md#getOldWorldToGeocentric_dmat4)** properties.
### Return value

Current geodetic position the world is anchored at
## Math:: dmat4 getGeocentricToWorld () const

Returns the current transformation matrix converting geocentric (ECEF) coordinates to world coordinates for the current anchor frame.
### Return value

Current geocentric-to-world transformation matrix
## Math:: dmat4 getWorldToGeocentric () const

Returns the current transformation matrix converting world coordinates to geocentric (ECEF) coordinates for the current anchor frame.
### Return value

Current world-to-geocentric transformation matrix
## Math:: dmat4 getOldGeocentricToWorld () const

Returns the current geocentric-to-world transformation matrix that was in effect before the last re-anchoring. Together with the current matrices it can be used to convert the data you keep in world coordinates to the new anchor frame.
### Return value

Current previous geocentric-to-world transformation matrix
## Math:: dmat4 getOldWorldToGeocentric () const

Returns the current world-to-geocentric transformation matrix that was in effect before the last re-anchoring. Together with the current matrices it can be used to convert the data you keep in world coordinates to the new anchor frame.
### Return value

Current previous world-to-geocentric transformation matrix
## Event<> getEventChanged () const

Returns the current event triggered each time the anchor frame is applied: when a new position is set via **[getGeoPosition()](../../../...md#getGeoPosition_dvec3)**, when the anchor is dropped via **[reset()](../../../...md#reset_void)**, and when the anchor is moved by an external driver, such as the [Cesium](../../../../code/plugins/cesium/index_cpp.md) plugin. By the time the callback runs, the new frame is already in effect: the current transformations are available via **[getGeocentricToWorld()](../../../...md#getGeocentricToWorld_dmat4)** and **[getWorldToGeocentric()](../../../...md#getWorldToGeocentric_dmat4)**, and the previous ones via **[getOldGeocentricToWorld()](../../../...md#getOldGeocentricToWorld_dmat4)** and **[getOldWorldToGeocentric()](../../../...md#getOldWorldToGeocentric_dmat4)**.
### Return value

Current event triggered when the anchor frame changes
---

## reset ( )

Resets the anchor: the world-to-geocentric and geocentric-to-world transformations become identity, so world space coincides with the geocentric (ECEF) coordinate system, and the mode switches to *[ANCHOR_MODE_GEOCENTRIC](#ANCHOR_MODE_GEOCENTRIC)*. The previous transformations remain available via the **[getOldGeocentricToWorld()](../../../...md#getOldGeocentricToWorld_dmat4)** and **[getOldWorldToGeocentric()](../../../...md#getOldWorldToGeocentric_dmat4)** properties.
